# Future State Architecture

The AI Customer Engagement Engine acts as an intelligent orchestration layer between Lead Generation and Relationship Manager (RM) engagement.

The platform continuously captures customer intent signals, determines the next-best action, engages customers through AI-powered conversations, and routes qualified prospects to the right RM at the right time.

This transforms a traditionally reactive sales process into a proactive, always-on engagement ecosystem.

<img width="1224" height="1285" alt="image" src="https://github.com/user-attachments/assets/2fba15a6-21eb-411f-bc17-4b2e69093942" />

----------------------------------------------------------------------------------------------------------------------------------------------------
## Layer 1: Lead Sources Layer

First step is to create a unified lead capture system and ensure every prospect enters the engagement journey with sufficient context. But the objective is not lead collection, it is customer intent capture.

Sources include - 
- Digital Advertising
- Website
- Landing Pages
- Referral Programs
- Offline Events
- Branch Walk-ins
- Partner Ecosystem
- Franchise Network

| Framework                      | Description                                                                        | Details                                                                                                                                                                                                                                                                |
|--------------------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lead Intake                    | Add the lead details in a central repository                                       | Add per-source mandatory field table and validation rules per field; add a deduplication key; add mandatory consent/DND capture                                                                                                                                        |
| Data Quality & Consent Gate    | Evaluate whether the lead has the requisite details for further consideration      | Add a binary gate: Pass (proceeds to scoring) or Held (returned to source for correction, never silently dropped) to the rest of the data                                                                                                                              |
| Lead Enrichment                | Add the details for the lead from different sources (internal as well as external) | Add Third-party/external enrichment for income proxies, credit bureau signals, PIN-code-level demographic data, firmographic data as well as Behavioral enrichment like UTM parameters, device type, referring page                                                    |
| Lead Quality Scoring Framework | Calculate the lead score based on initial details                                  | Lead marked as Hot/Warm/Cold based on details received for further processing                                                                                                                                                                                          |
| Source Attribution Framework   | Attribute lead to the source for business impact                                   | Choose Multi Touch with a stated decay window (recent touches weighted more than distant ones); name the lookback window (e.g., 90 days), and treat First/Last Touch as reporting views available to stakeholders, never as the system of record for budget allocation |
| Routing Eligibility Rules      | Identify the team for servicing based on initial consideration                     | Define Segment-based classification and routing framework                                                                                                                                                                                                              |

----------------------------------------------------------------------------------------------------------------------------------------------------
## Layer 2: Customer Intelligence Layer

Focus is on one continuous profile per person, running from first lead touch through active customer and beyond — not a separate lead system and a separate customer system. It works in two distinct steps, not one — capture and enrichment are different jobs:

**Capture** — raw signals get logged the moment they happen, per channel: a form fill or ad click (lead source, campaign history), a page visited or time spent on it (website behavior), a message sent or ignored (WhatsApp interactions), notes from a call (previous RM conversations), a fund or stock viewed (product interest), an order placed (trading behavior). At this stage it's just events — timestamped, tagged to a channel, nothing interpreted yet.

**Enrichment** — this is where the layer turns raw events into something the AI Decisioning Platform can actually use.

The entire focus is on merging the details into actionable input. This includes - 
- Identity resolution — stitching together signals that came in through different channels (a WhatsApp click and a website visit) into the same customer record, rather than treating them as separate people.
- Derived signals — turning raw behavior into something interpretable: three visits to the SIP page isn't just "three page views," it's an intent signal; a demographic profile plus trading behavior becomes a product-affinity signal.
- Recency and pattern — not just what they did, but when and how often, since a customer who went quiet after being active is a different signal than one who's steadily engaging.

| Framework                    | Description                                                                                                                      | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Customer Identity Resolution | Establish rules to identify customer across channels                                                                             | Generates the single golden customer ID with a deterministic match layer (PAN, mobile no, email). Also a probabilistic match layer for the harder cases is defined — same device fingerprint, overlapping name plus location, near-matching contact details. Lastly, policy for the ambiguous cases                                                                                                                                                                     |
| Customer 360 Data Model      | Define the customer data model with all the relevant information; for a prospect, most of it will be sparse                      | Add Profile / Financial / Behavioral / Engagement details with defined refresh cadence, source-of-record, and a confidence (completeness) flag per group; state which fields materialize into the feature store                                                                                                                                                                                                                                                         |
| Behavioral Taxonomy          | Add customer actions into an organized scheme for further consideration                                                          | Add app event, trade event, lead event set; define short-half-life (searches, sessions) versus long-half-life (SIP started, first trade), and polarity per event; add a negative/friction event set for churn signals                                                                                                                                                                                                                                                   |
| Segmentation Framework       | Categorize customer based on net worth, engagement behavior and stage of engagement ("Prospect → Activated → Engaged → Dormant") | Create 3 independent axes — Wealth, Behavior, Lifecycle for consideration, identify recompute cadence per axis (Wealth: monthly on AUM refresh; Behavior: weekly; Lifecycle: event-triggered); state axes combine (not replace - Lifecycle governs eligibility for outreach and Wealth/Behavior governing kind of outreach); define Lifecycle transition triggers explicitly; Wealth needs provisional (lead-stage, from enrichment) vs. confirmed (post-KYC, real AUM) |
| Intent Detection Logic       | Identify customer's actual state of engagement based on all the collected data and categorization                                | Generate tiered, windowed score (Low/Medium/High or a 0–100 score) for intent rather than standalone decision; State the window on every input signal, and add one exclusion rule: check Intent against Lifecycle/complaint status before firing                                                                                                                                                                                                                        |


Data Captured - 
- Demographics
- Lead Source
- Campaign History
- Website Behaviour
- WhatsApp Interactions
- Previous RM Conversations (if any)
- Product Interests
- Trading Behaviour

----------------------------------------------------------------------------------------------------------------------------------------------------------
## Layer 3: AI Decisioning Platform

This layer's job is to decide what happens next for each customer, via three engines working together:

- Propensity Engine — scores likelihood across four outcomes: opening an account, trading, investing, and responding to outreach.
- Customer Intent Engine — classifies where the customer is in their journey: exploring, comparing, ready to act, or needing assistance.
- Next Best Action Engine — takes both inputs and makes the call: engage now, wait, escalate, or assign to an RM.
- Decision Hierarchy - One winning action to execute now for engage now, plus the rest ranked and queued, not dropped

The propensity and intent engines produce signals; the Next Best Action engine is what converts those signals into a decision. From a product standpoint, this is the layer that turns raw customer data into something the business can actually act on — everything upstream (Customer Intelligence Layer) is about knowing the customer, everything here is about deciding what to do about it.

Once the action is identified, focus is on relevant content selection for further consideration.

| Framework               | Description                                                                                                                                                              | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Propensity Engine       | Scores Likelihoodness of different outcomes to act as well as the prediction horizon per outcome, and the refresh cadence                                                | 4 models are identified explicitly - Conversion (likelihood to open an account), Product (likelihood to trade or invest), Contactability (likelihood to respond to outreach), and Churn (an inverse signal — likelihood to disengage); Compute Upgrade as investing propensity × Wealth-axis proximity rather than a separate model; tie Conversion propensity to Lead Management's Lead Quality Score as one engine; Product Propensity should consume the Intent Detection score as one input feature and extend it with financial/firmographic data and is one blended trade/invest score &  journey stage is what recovers that distinction; Churn Propensity explicitly build on Customer Intelligence's Lifecycle segment already with Dormant stage; add horizon, and refresh cadence per outcome |
| Customer Intent Engine  | Define the behavioral thresholds that move someone between stages, and make sure this consumes Customer Intelligence's Intent Detection score rather than re-deriving it | Create Four-stage journey classification - exploring, comparing, ready to act, needing assistance built on page views, research consumption, session recency and define stage-transition thresholds; build on Intent Detection's score rather than beside it; Split Needing Assistance into a cross-cutting flag that can co-occur with any of the other three stages as it describes a friction state and needs urgent intervention                                                                                                                                                                                                                                                                                                                                                                     |
| Next Best Action Engine | Identify the best action - engage now / wait / escalate / assign to RM, then — specify action from the state-to-action table                                             | Generate two-level decision: verb (engage now / wait / escalate / assign RM - computed from the Propensity and Customer Intent engines' outputs) then state-to-action table informed by timing & CLV; Define how long "wait" is re-evaluated on and Define what "wait" re-evaluates on using Timing's window; distinguish escalate from assign-to-RM using CLV; enumerate all eligible actions per state; add cooldown and fallback                                                                                                                                                                                                                                                                                                                                                                      |
| Decision Hierarchy      | Define the decision hierarchy based and sequence the actions                                                                                                             | Calculate the flat ranking with a weighted score - category (Ex. Retention = 1.5, Advisory = 1.2, Upsell = 1.0) × confidence (propensity/intent score itself, 0–1, straight from the Propensity Engine or NBA Engine's trigger) × CLV for "engage now" branch; Define decision hierarchy based on the ranking output only and within-category tie-breaks; cap concurrent actions with explicitly one primary action live per customer at a time, with the rest queued, not dropped (If Advisory is primary, then retention and upsell actions go in queue, not discarded)                                                                                                                                                                                                                                |
| Content Selection       | Build the content taxonomy per action (which message variants are valid for "Re-engagement," etc.) and the variant-selection logic                                       | Create the taxonomy and variant selection the "action, content, channel" scope calls for - For each action Next Best Action can trigger, identify the set of valid message templates or offer types available to fill it; Content should route through the content governance framework                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| AI Governance           | Set per-category confidence thresholds, scope bias checks to advisory-recommendation parity, and own the monthly drift-review cadence plus the RM-escalation SLA         | Make thresholds configurable per action category; scope bias checks to advisory-recommendation parity (recommendation parity across customer segments); add a Add a monthly model-performance review cadence; add an SLA and fallback for unreviewed escalations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |


--------------------------------------------------------------------------------------------------------------------------------------------------------------

## Layer 4: Engagement Orchestration Layer

The Engagement Orchestration Layer is the central nervous system responsible for determining when, why, how, and through which channel a customer should be engaged across the acquisition journey.

Five core capabilities:

1. Trigger Management — listens for customer events (lead submitted, app installed, KYC incomplete, website visit, etc.) and decides whether engagement is required right now. Without this, engagement stays batch-driven and reactive.
2. Journey Orchestration — decides what happens next once a trigger fires (WhatsApp message, email, push, AI conversation, RM assignment, or wait). This is where the flow — welcome message → response → intent assessment → qualification → product recommendation → RM handoff → RM follow-up — is stitched into one continuous conversation rather than disjointed touches.
3. Conversational Intelligence (Agentic WhatsApp) — the difference between a traditional chatbot (question → predefined answer) and an agentic one (understand intent → retrieve context → reason → generate response → take action). The AI qualifies the lead through conversation rather than just answering it.
4. RAG-Based Response Automation — grounds every response in real knowledge sources (product FAQs, brokerage plans, KYC policies, compliance guidelines) instead of letting the LLM answer generically. The product outcome: a grounded, compliant response instead of a hallucinated one — critical in financial services.
5. RM Collaboration Layer — AI handles engagement, RM handles relationships. Before handoff, the RM receives a full package: customer profile, intent summary, conversation history, lead score, recommended next action, product interest — so they walk in with context, not a cold lead.

Plus a Continuous Learning Layer running underneath all five: every conversation outcome, RM feedback, and conversion result feeds back into the propensity models, decision engine, and recommendation models — making the system self-improving rather than static.

The key architectural distinction the doc makes: the Agentic WhatsApp Journey is not the Engagement Orchestration Layer — it's one capability inside it.

- Orchestration layer decides WHEN to engage
- WhatsApp agent decides HOW to engage
- RAG engine decides WHAT to say
- RM handoff engine decides WHO acts next
----------------------------------------------------------------------------------------------------------------------------------------------------------------
# Layer 5: Human Engagement Layer

Relationship Managers (RMs) time is the scarcest, most expensive resource in the funnel, and today it's spent unevenly — hunting for the right customer to call, re-establishing context that already exists somewhere in the system, and working leads that were never going to convert. This layer's job is to fix the allocation, not shrink the headcount.

The Human Engagement Layer ensures that AI-driven customer engagement transitions seamlessly into high-quality human interactions when advisory expertise, trust-building, or conversion support is required.

The objective is not to replace RMs, but to maximize their effectiveness by providing complete customer context, intent intelligence, and recommended actions.

The Human Engagement Layer operates through three steps:
- Identify: The AI Engagement Layer continuously evaluates customer behavior, intent, and readiness. When a predefined threshold is reached, the customer is considered ready for human engagement.
  High Purchase Intent → Callback Requested → Complex Product Query → High-Value Customer → KYC Completed
- Prepare: Before assigning the customer, the platform generates a complete engagement context.
  Customer Profile → Intent Summary → Product Interest → Conversation History → Recommended Next Action
- Engage: The platform routes the customer to the most appropriate RM and initiates the human conversation.
  Customer Ready → Best RM Selected → Context Shared → RM Engagement → Conversion

  -----------------------------------------------------------------------------------------------------------------------------------------------------------
  # Layer 6: Business Outcomes Layer

  This is the layer that proves the other five actually worked. The outcomes need to be valued across three tiers:

  - Customer outcomes — faster responses, personalized experiences, reduced friction, higher satisfaction
  - Business outcomes — higher engagement, higher conversion, lower lead leakage, improved RM productivity, reduced acquisition cost
  - Strategic outcomes — an AI-augmented sales model, scalable customer engagement, a consistent customer experience, a data-driven growth engine
