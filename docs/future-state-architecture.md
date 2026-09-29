# Future State Architecture

The AI Customer Engagement Engine acts as an intelligent orchestration layer between Lead Generation and Relationship Manager (RM) engagement.

The platform continuously captures customer intent signals, determines the next-best action, engages customers through AI-powered conversations, and routes qualified prospects to the right RM at the right time.

This transforms a traditionally reactive sales process into a proactive, always-on engagement ecosystem.

<img width="673" height="1077" alt="image" src="https://github.com/user-attachments/assets/b412b273-8b05-47bc-ba94-ad645c37e6ba" />

----------------------------------------------------------------------------------------------------------------------------------------------------
## Layer 1: Lead Sources Layer

The focus is to capture customer interest from all acquisition channels. But the objective is not lead collection, it is customer intent capture.

Sources include - 
- Digital Advertising
- Website
- Landing Pages
- Referral Programs
- Offline Events
- Branch Walk-ins
- Partner Ecosystem
- Franchise Network
----------------------------------------------------------------------------------------------------------------------------------------------------
## Layer 2: Customer Intelligence Layer

It works in two distinct steps, not one — capture and enrichment are different jobs:

**Capture** — raw signals get logged the moment they happen, per channel: a form fill or ad click (lead source, campaign history), a page visited or time spent on it (website behavior), a message sent or ignored (WhatsApp interactions), notes from a call (previous RM conversations), a fund or stock viewed (product interest), an order placed (trading behavior). At this stage it's just events — timestamped, tagged to a channel, nothing interpreted yet.

**Enrichment** — this is where the layer turns raw events into something the AI Decisioning Platform can actually use:

Identity resolution — stitching together signals that came in through different channels (a WhatsApp click and a website visit) into the same customer record, rather than treating them as separate people.
Derived signals — turning raw behavior into something interpretable: three visits to the SIP page isn't just "three page views," it's an intent signal; a demographic profile plus trading behavior becomes a product-affinity signal.
Recency and pattern — not just what they did, but when and how often, since a customer who went quiet after being active is a different signal than one who's steadily engaging.



Data Captured - 
- Demographics
- Lead Source
- Campaign History
- Website Behaviour
- WhatsApp Interactions
- Previous RM Conversations (if any)
- Product Interests
- Trading Behaviour
