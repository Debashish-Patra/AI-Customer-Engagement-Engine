# Future State Architecture

The AI Customer Engagement Engine acts as an intelligent orchestration layer between Lead Generation and Relationship Manager (RM) engagement.

The platform continuously captures customer intent signals, determines the next-best action, engages customers through AI-powered conversations, and routes qualified prospects to the right RM at the right time.

This transforms a traditionally reactive sales process into a proactive, always-on engagement ecosystem.

<img width="1224" height="1285" alt="image" src="https://github.com/user-attachments/assets/2fba15a6-21eb-411f-bc17-4b2e69093942" />

----------------------------------------------------------------------------------------------------------------------------------------------------
## Layer 1: Lead Sources Layer

The objective of this layer is to create a unified lead pool and ensure every prospect enters the engagement journey with sufficient context. But the objective is not lead collection, it is customer intent capture.

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

It works in two distinct steps, not one — capture and enrichment are different jobs:

**Capture** — raw signals get logged the moment they happen, per channel: a form fill or ad click (lead source, campaign history), a page visited or time spent on it (website behavior), a message sent or ignored (WhatsApp interactions), notes from a call (previous RM conversations), a fund or stock viewed (product interest), an order placed (trading behavior). At this stage it's just events — timestamped, tagged to a channel, nothing interpreted yet.

**Enrichment** — this is where the layer turns raw events into something the AI Decisioning Platform can actually use:

- Identity resolution — stitching together signals that came in through different channels (a WhatsApp click and a website visit) into the same customer record, rather than treating them as separate people.
- Derived signals — turning raw behavior into something interpretable: three visits to the SIP page isn't just "three page views," it's an intent signal; a demographic profile plus trading behavior becomes a product-affinity signal.
- Recency and pattern — not just what they did, but when and how often, since a customer who went quiet after being active is a different signal than one who's steadily engaging.

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

The propensity and intent engines produce signals; the Next Best Action engine is what converts those signals into a decision. From a product standpoint, this is the layer that turns raw customer data into something the business can actually act on — everything upstream (Customer Intelligence Layer) is about knowing the customer, everything here is about deciding what to do about it.

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
