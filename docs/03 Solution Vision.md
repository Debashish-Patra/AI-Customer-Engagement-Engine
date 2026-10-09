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

### The solution at a glance -  six layers, one by one

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

### One customer, end to end - Take a customer who messages "I want to start investing". 

The same path applies to any lead or customer action.

<p align="center"><img width="847" height="430" alt="image" src="https://github.com/user-attachments/assets/c6c0487d-ffb7-4a0a-ba43-d815ef6dacb1" />

1. Event arrives. The message, a form, an app install or a started account-opening journey is the trigger.
2. Safety checks. Is there live consent? Is a journey already running for this customer? Would this clash with another message? Only then does Layer 3 act.
3. Decide. The decision layer scores readiness and picks one of four actions: engage, wait, escalate or assign to an RM. The last two both lead to the RM branch in the picture.
4. Engage or wait. Engage starts an AI conversation that asks the goal and what is needed to open an account, with answers grounded in approved content. Wait is a timed pause that ends when the customer acts. On any material change the decision is made again.
5. To an RM. When the customer is ready, or asks for advice such as "Should I invest ₹20L?", the RM gets the customer with a summary of the goal, interest, history and a recommended next action, and must act within a service level for that customer type.
6. Outcome measured. The result is tied back to the decision and the messages that produced it, and tunes the earlier layers.

| Identifier  | Created by                    | What it lets you do                                                              |
|-------------|-------------------------------|----------------------------------------------------------------------------------|
| customer_id | Layer 2 (identity resolution) | Recognise the same person across systems and channels                            |
| decision_id | Layer 3                       | Tie every action to the decision that caused it                                  |
| journey_id  | Layer 4                       | Keep one continuous conversation across channels and across the handoff to an RM |
| touch_id    | Layers 4 and 5                | Identify each message or call, so results are traced to a single touch           |

### Outcomes and how they are proven
The solution is judged in three tiers, and a result counts only if a comparison with customers the system left alone shows the system caused it.

| Tier      | Outcomes                                                                                                                 |
|-----------|--------------------------------------------------------------------------------------------------------------------------|
| Customer  | Faster responses, personalized experiences, reduced friction, higher satisfaction                                        |
| Business  | Higher engagement, higher conversion, lower lead leakage, improved RM productivity, reduced acquisition cost             |
| Strategic | An AI-augmented sales model, scalable customer engagement, a consistent customer experience, a data-driven growth engine |

Measures
• North Star: net new AUM is proposed, driven by lead-to-funded conversion, retention and revenue per active customer. Opt-outs and complaints sit beside it as guardrails.
• Engagement: journey completion, reply rate, first response time, opt-out rate and satisfaction. Open and click rates are diagnostics only.
• Advisor productivity: share of RM time on ready customers, time to first contact, service-level attainment, conversion per RM adjusted for the quality of leads received.
• AI effectiveness: prediction lift and calibration, recommendation precision and recall, automation rate paired with resolution quality, fallback escalation rate, grounded-answer rate, fairness and drift.
• Reporting: one metric dictionary, with reports by audience and a map from each metric to the setting that moves it.

### Guardrails & Risks

The solution acts on customers' behalf in a regulated business, so the guardrails below apply in every layer and are checked in the flow, not afterwards. The risks that follow show what each guardrail protects against.

| Risk                                                             | How it is handled                                                                                     | Guardrail it relies on                    |
|------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|-------------------------------------------|
| Wrong or non-compliant AI answers                                | Approved content only; advice always goes to an RM                                                    | Grounded answers; advice goes to a human  |
| Models drift or treat some customer segments unfairly            | Bias thresholds by segment and regular drift review                                                   | Fairness and drift; explainable decisions |
| Customers contacted without permission, or customer data misused | Consent captured at intake and checked again before every send; each step uses only the data it needs | Consent                                   |
| Over-contact irritates customers                                 | Combined contact ceiling; opt-out rate watched as a warning sign                                      | Contact limits; consent                   |
| Poor source data and duplicate records                           | Data quality and consent gate at intake; review of uncertain identity merges                          | Consent (intake gate)                     |
| The decision layer fails or is slow                              | A simple channel table and a no-response sequence keep journeys running                               | Fallback                                  |
| Advisors see alerts and priority as extra work or surveillance   | Involve RM leads in setting service levels; show the workbench saves context-gathering time           | Service levels                            |
| Gains credited to the market or a campaign                       | Holdout comparison before any claim of impact                                                         | Fair testing                              |
| Franchise and offline channels left outside the flow             | Include them in intake and the advisor workbench from the first phase                                 | Build sequence (below)                    |

