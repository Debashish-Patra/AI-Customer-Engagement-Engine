# AI Decision Platform

Propensity, intent, next-best-action and decision hierarchy — turned into one action decision: engage (all actions ranked), wait, escalate, or assign to RM.

| Engine                  | Models feeding it                                                                                                                                                              | What it outputs                                                                 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Propensity Engine       | Conversion (→ likelihood to open account), Product (→ likelihood to trade/invest), Contactability (→ likelihood to respond), Churn (→ inverse signal, likelihood to disengage) | Four scored likelihoods per customer                                            |
| Customer Intent Engine  | Behavioral pattern on top of the Customer Intelligence Layer's signals (page views, research consumption, session recency)                                                     | A journey state: exploring / comparing / ready to act / needs assistance        |
| Next Best Action Engine | All of the above, plus Timing (best window) and CLV (value-weighted priority) — the two mature-stack additions                                                                 | The actual decision: engage / wait / escalate / assign to RM                    |
| Decision Hierarchy      | Every action that qualifies under "engage now," each carrying a category weight, a confidence score, and CLV                                                                   | One winning action to execute now, plus the rest ranked and queued, not dropped |

### **Propensity Engine — the scoring backbone**

- Product requirement: Four scores per customer (open-account, trade, invest, respond), refreshed continuously, not computed once at lead creation. Churn's inverse signal has to live here too even though the original doc doesn't list it explicitly — without it, the engine can score someone as high-propensity-to-invest while missing that they're actively disengaging.
- North-star metric: Correlation between top-decile scores and actual outcomes, tracked per score type separately — a platform that's well-calibrated on "likelihood to respond" but poorly calibrated on "likelihood to invest" is a real failure mode, and a single blended accuracy number will hide it.
- Build note: This engine can't ship in isolation — it's only as good as the Customer Intelligence Layer's single customer view underneath it. 

### **Customer Intent Engine — the layer most likely to be underbuilt**

- Product requirement: A journey-state classification (exploring / comparing / ready to act / needs assistance), distinct from a propensity score — a customer can have a high conversion propensity and still be in "comparing," which should trigger reassurance content, not a hard sales push.
- North-star metric: This is the hardest of the three engines to measure directly, because "intent" isn't independently observable — I'd validate it indirectly, by checking whether actions matched to each intent state (educational content for "exploring," an RM call for "ready to act") outperform mismatched actions in a holdout test.
- Roadmap risk: Teams tend to treat this engine as a nice-to-have layered onto propensity scores, since propensity alone looks sufficient on paper. Propensity score tells you who's likely to convert, not what kind of conversation they're ready for, and getting that wrong is what makes outreach feel tone-deaf even when the targeting is technically correct.

### **Next Best Action Engine — where the business risk concentrates**

- Product requirement: A four-way decision (engage / wait / escalate / assign to RM), which means this is a rules-and-model hybrid, not a pure ML output — someone has to own the decision logic that turns three sets of scores into one action, and that ownership needs to be explicit or it becomes nobody's job.
- This is where Timing and CLV earn their place: Timing decides whether "engage" should fire now or get queued; CLV decides whether "escalate to RM" is worth an RM's time for this specific customer versus a lower-touch path. Without these two, the engine can only make a binary call; with them, it can make a sequenced, value-aware one.
- North-star metric: RM time-to-value — are the leads escalated to RMs converting at a meaningfully higher rate than a random sample of "high propensity" leads would have? If not, the escalation logic isn't adding judgment beyond what the Propensity Engine already provides, and the org is paying for a decisioning layer that isn't deciding anything new.
- Governance note: This engine is the one place where a model output directly changes which customers get an RM's attention and which don't.

### **Decision Hierarchy - Identify which actions are prioritized more for the moment**

- Product requirement: When more than one action clears the "engage now" bar simultaneously, compute a priority score per candidate — category weight × model confidence × CLV — and fire exactly one. Everything else that qualified gets queued with its own score, re-evaluated on the next triggering event or a fixed cadence, and expires (or gets promoted) rather than sitting forever. Scoped only to the "engage now" branch — it has no role in wait, escalate, or assign-to-RM, which bypass it entirely.
- North-star metric: Incremental value captured triggers the relevant action. A secondary check worth tracking alongside it: queue-clearance rate — the share of queued (non-winning) actions that eventually fire within their validity window, rather than silently expiring. A near-zero clearance rate means lower-priority-but-still-real opportunities are being starved, not just deferred.
- Key detail: This is the layer where CLV does double duty — it's already an NBA Engine input (for the escalate/assign-RM worth-it call) and it's also this engine's own value-at-stake term. That's not redundant, but it does mean a change to how CLV is computed propagates into two decisions at once, which is worth flagging to whoever owns the CLV model as a dependency, not a coincidence.

-----------------------------------------------

## **Content Selection - the layer sits after the decision chain, not inside it**

The four engines (Propensity, Intent, NBA, Decision Hierarchy) are all answering some version of "what should happen" — a score, a stage, a verb, a winning action. Content Selection only starts once that chain has already produced one answer; its job is "what do we actually say," which is a categorically different question. Content Selection has its own taxonomy, variant-selection logic, its own compliance surface that the four engines don't touch.

- Product requirement: a content taxonomy per action, with variant selection driven by the same segment/propensity/journey-stage data, and every variant routed through governance independent of the action's own clearance.
- North-star metric: content-variant lift against a single-fixed-script baseline — this is the metric that catches the real failure mode, where all the sophistication lives in the four engines and this layer quietly degrades to one generic message per action. Paired with variant coverage (do actions actually have more than one compliant option to choose from).
- Key detail: content compliance is a separate risk surface from action compliance — a correctly triggered action can still carry a non-compliant message — so it needs its own audit trail, not one folded into the action's explainability record.
