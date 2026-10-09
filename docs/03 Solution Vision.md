# Product Vision

The vision: Every customer who shows interest is met with the right message, at the right time, through the right channel, with the right human touch, and the business can prove it worked.

Today, leads are generated from many sources but are not effectively converted, because of gaps in assignment, visibility and engagement. A lead is assigned, the RM makes contact two days later, the customer's interest has gone, and there is no conversion. 

The solution closes those gaps with one connected system, built as six layers.

Design principles
1. One customer, one journey. A customer is recognised once, and one continuous conversation follows them across channels and across the handoff to an RM.
2. AI for the routine, people for the advice. The aim is to fix the allocation of RM time, not to shrink headcount or replace advisors. Advice always goes to a human.
3. One owner per decision. Each decision (when, how, what, who) belongs to one layer, so layers do not contradict each other.
4. Consent and governance built in. Permission, explainability and fairness checks are part of the flow, not added afterwards.
5. Measured, and proven. Every layer reports into a common set of measures, and gains are shown against a comparison group, not assumed.

<p align="center"><img width="852" height="592" alt="image" src="https://github.com/user-attachments/assets/8732b722-b852-4a59-979e-ef09366aecef" />

The AI Decisioning Layer acts as the digital front door between lead generation and relationship management, where the system decides what happens to each customer. The four shared identifiers (customer_id, decision_id, journey_id, touch_id) let any outcome be traced back to the decision and the messages that produced it.

| Layer                      | What it does?                                                  | Frameworks                                                                                                                                                     | Hands to               |
|----------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| 1 Lead Sources             | Take in every lead cleanly and decide whether it can be worked | Lead intake, data quality and consent gate, enrichment, scoring, source attribution, routing eligibility                                                       | Layer 2                |
| 2 Customer Intelligence    | Know the customer: one profile and what they want              | Identity resolution, Customer 360, behavioural taxonomy, segmentation, intent detection                                                                        | Layer 3                |
| 3 AI Decisioning           | Decide the next best action and keep the AI governed           | Propensity engine (conversion, product, contactability, churn), customer intent engine, next best action, decision hierarchy, content selection, AI governance | Layer 4                |
| 4 Engagement Orchestration | Turn a decision into a sequenced conversation                  | Trigger, frequency governance, channel strategy, sequencing, agentic AI workflow, grounded answers (RAG), RM handoff package, continuous learning              | Layer 5                |
| 5 Human Engagement         | Put the right RM on the right customer, ready to help          | AI-to-human handoff, advisor workbench, RM capacity and assignment, RM prioritization, service levels, engagement initiation, feedback loop                    | Layer 6                |
| 6 Business Outcomes        | Prove it worked and say what to change                         | North Star, engagement, advisor and AI metrics, reporting and feedback loops, incrementality testing                                                           | Back to Layers 1, 3, 5 |

## AI Engagement Layer

The AI engagement layer is the digital front door — it sits between the systems that generate leads and the RMs who close them, and it's built to do six things continuously: 

<img width="1283" height="290" alt="image" src="https://github.com/user-attachments/assets/fc481145-2fcf-42a6-bfeb-113127bb0149" />


1. Engage every lead instantly — no lead sits untouched waiting for a human to pick it up; the moment it's created, something responds
2. Capture and enrich intent signals — every interaction (what they clicked, asked, or ignored) gets logged and used to build a fuller picture of what the customer actually wants — not every lead deserves the same urgency; this ranks them by how likely and how ready they are to convert
3. Prioritize by propensity — routine questions, basic qualification, status updates — handled without needing an RM's time
4. Automate the low-value back-and-forth — routine questions, basic qualification, status updates — handled without needing an RM's time
5. Route high-intent prospects to RMs — once a lead is qualified and warm, it's handed to a human at the right moment, not too early (wasting RM time) or too late (losing momentum)
6. Keep the experience consistent across channels — whether the customer is on WhatsApp, in-app, or on a call, the context and tone carry over rather than resetting




