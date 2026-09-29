# AI Decision Platform

Propensity, intent, and next-best-action — turned into one call: engage, wait, escalate, or assign to RM.

| Engine                  | Models feeding it                                                                                                                                                              | What it outputs                                                          |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Propensity Engine       | Conversion (→ likelihood to open account), Product (→ likelihood to trade/invest), Contactability (→ likelihood to respond), Churn (→ inverse signal, likelihood to disengage) | Four scored likelihoods per customer                                     |
| Customer Intent Engine  | Behavioral pattern on top of the Customer Intelligence Layer's signals (page views, research consumption, session recency)                                                     | A journey state: exploring / comparing / ready to act / needs assistance |
| Next Best Action Engine | All of the above, plus Timing (best window) and CLV (value-weighted priority) — the two mature-stack additions                                                                 | The actual decision: engage / wait / escalate / assign to RM             |

### **Propensity Engine — the scoring backbone**

Product requirement: Four scores per customer (open-account, trade, invest, respond), refreshed continuously, not computed once at lead creation. Churn's inverse signal has to live here too even though the original doc doesn't list it explicitly — without it, the engine can score someone as high-propensity-to-invest while missing that they're actively disengaging.
North-star metric: Correlation between top-decile scores and actual outcomes, tracked per score type separately — a platform that's well-calibrated on "likelihood to respond" but poorly calibrated on "likelihood to invest" is a real failure mode, and a single blended accuracy number will hide it.
Build note: This engine can't ship in isolation — it's only as good as the Customer Intelligence Layer's single customer view underneath it. I'd block this engine's launch on that dependency being solid, not run them in parallel and hope.

### **Customer Intent Engine — the layer most likely to be underbuilt**

Product requirement: A journey-state classification (exploring / comparing / ready to act / needs assistance), distinct from a propensity score — a customer can have a high conversion propensity and still be in "comparing," which should trigger reassurance content, not a hard sales push.
North-star metric: This is the hardest of the three engines to measure directly, because "intent" isn't independently observable — I'd validate it indirectly, by checking whether actions matched to each intent state (educational content for "exploring," an RM call for "ready to act") outperform mismatched actions in a holdout test.
Roadmap risk: Teams tend to treat this engine as a nice-to-have layered onto propensity scores, since propensity alone looks sufficient on paper. I'd push back on that — a propensity score tells you who's likely to convert, not what kind of conversation they're ready for, and getting that wrong is what makes outreach feel tone-deaf even when the targeting is technically correct.

### **Next Best Action Engine — where the business risk concentrates**

Product requirement: A four-way decision (engage / wait / escalate / assign to RM), which means this is a rules-and-model hybrid, not a pure ML output — someone has to own the decision logic that turns three sets of scores into one action, and that ownership needs to be explicit or it becomes nobody's job.
This is where Timing and CLV earn their place: Timing decides whether "engage" should fire now or get queued; CLV decides whether "escalate to RM" is worth an RM's time for this specific customer versus a lower-touch path. Without these two, the engine can only make a binary call; with them, it can make a sequenced, value-aware one.
North-star metric: RM time-to-value — are the leads escalated to RMs converting at a meaningfully higher rate than a random sample of "high propensity" leads would have? If not, the escalation logic isn't adding judgment beyond what the Propensity Engine already provides, and the org is paying for a decisioning layer that isn't deciding anything new.
Governance note, same as I flagged on CLV earlier: This engine is the one place where a model output directly changes which customers get an RM's attention and which don't. I'd insist on an audit trail — why did this customer get "escalate" instead of "wait" — before this goes live, because when a customer or regulator asks why they were or weren't contacted, "the model decided" is not an acceptable answer on its own.
