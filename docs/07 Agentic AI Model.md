# Agentic AI: Operating Model 

Agents execute inside decisions that Layer 3 (AI Decisioning) makes, on two parallel tracks: customer-facing agents in non-advisory stages, and copilots that 
prepare advisors. Autonomy starts low and rises only with evidence. This is a proposed design, to be confirmed with compliance, technology and the business before 
build.

The layers and journey steps in brief
The architecture has six layers. Agents work mainly in Layers 3 to 5 and depend on Layer 2, so it helps to see what each layer does before reading how agents fit.

| Layer                      | What it does                                                   | Role for agents                 |
|----------------------------|----------------------------------------------------------------|---------------------------------|
| 1 Lead Sources             | Brings leads in from every channel                             | None directly                   |
| 2 Customer Intelligence    | Builds one customer record, keyed by customer_id               | Source of facts the agent reads |
| 3 AI Decisioning           | Decides whether, when and what to offer, logged as decision_id | Gives the agent its task        |
| 4 Engagement Orchestration | Sequences the journey across channels (journey_id, touch_id)   | Runs customer-facing agents     |
| 5 Human Engagement         | RMs and advisors take over, and own handoff thresholds         | Hosts advisor copilots          |
| 6 Business Outcomes        | Measures results, with holdout testing                         | Judges whether agents work      |

## Where Agents fit 
<p align="center"><img width="900" height="346" alt="image" src="https://github.com/user-attachments/assets/f7ba92fd-32a1-4d08-bc88-fa69eac2a89a" />

An agent plans and carries out multi-step tasks with tools, instead of only generating text. In this design it sits in Layer 4 (Engagement Orchestration) and in the 
advisor workbench of Layer 5 (Human Engagement), and it acts only on decisions Layer 3 (AI Decisioning) has made. That keeps the principle of one owner per decision:
agents never decide whether or when to contact a customer.

The customer journey has six steps, and agents are mapped to them:
1.	Awareness: the customer first hears about us.
2.	Consideration: the customer compares options and asks questions.
3.	Application and Verification: the customer applies and completes KYC.
4.	Activation and Funding: the account is opened and funded.
5.	First Trade and Engagement: the customer places a first trade. Conversion is counted as funded and traded.
6.	Ongoing Engagement and Growth: the customer keeps investing and grows with us.

<p align="center"><img width="900" height="315" alt="image" src="https://github.com/user-attachments/assets/b196b1cc-2ead-47a3-be25-9187be12c5b1" />

The customer-facing track helps customers finish routine steps, and stays out of advice. The advisor track gives RMs the context and drafts to act faster. 
Both draw on the same customer record and the same decisions from Layer 3 (AI Decisioning), so a customer never gets two different stories. The agent names are 
working names.

| Track    | Agent                           | Stage                    | What it does                                                                            |
|----------|---------------------------------|--------------------------|-----------------------------------------------------------------------------------------|
| Customer | Fee and product Q&A             | Awareness, Consideration | Answers fee and product questions from approved content only                            |
| Customer | KYC resume assistant            | Application              | Reminds and guides customers to finish stalled KYC steps                                |
| Customer | Funding guide                   | Activation               | Explains how to fund the account and checks where the customer is stuck                 |
| Customer | First-trade guide               | First Trade              | Walks the customer through placing a first order, with no recommendation of what to buy |
| Customer | Servicing and SIP prompts       | Ongoing                  | Nudges on SIP set-up and routine servicing                                              |
| Advisor  | Lead brief and priority         | Consideration            | Summarises a lead and ranks who to call first                                           |
| Advisor  | Assisted KYC helper             | Application              | Drafts the follow-up for a customer stuck in KYC                                        |
| Advisor  | Stuck-account alerts            | Activation               | Flags funded-but-idle and unfunded accounts with a drafted message                      |
| Advisor  | First-trade outreach brief      | First Trade              | Prepares the RM for a first-trade conversation                                          |
| Advisor  | Check-in prep, high-AUM clients | Ongoing                  | Prepares context ahead of a periodic review                                             |

## Agent Architecture

<p align="center"><img width="900" height="340" alt="image" src="https://github.com/user-attachments/assets/188be7ef-a7d3-47bd-a59c-4f0788c23ffa" />

Every agent has a ceiling set in advance, and moves up one step only after review of its results. Customer-facing agents start in shadow mode, where answers are 
checked but not sent, before acting within limits. Moving to the last step needs evidence and a compliance sign-off, and is not planned for launch.

<p align="center"><img width="900" height="399" alt="image" src="https://github.com/user-attachments/assets/665e8f9d-3714-42f6-9427-98aa031f33b6" />

  An agent is not a new layer. It receives a decision from Layer 3 (AI Decisioning), reads the customer record from Layer 2 (Customer Intelligence), sends through 
  Layer 4 (Engagement Orchestration), and hands over to people through Layer 5 (Human Engagement). It can use only the tools it has been given, and every step is 
  traceable through the shared identifiers.

  Agent results are measured separately from the rest of the programme, so a problem in an agent is not hidden inside a blended number. 

  | Area               | Measure                                                                                                  |
|--------------------|----------------------------------------------------------------------------------------------------------|
| Task completion    | Share of conversations where the customer finished the task, by journey stage                            |
| Quality            | Grounded-answer rate, and errors found in sampled review                                                 |
| Handoff            | Correct handoff on advisory questions, and RM rating of handoff quality                                  |
| Trust and fairness | Complaints, opt-outs, and fairness checks across customer groups                                         |
| Cost               | Cost per resolved conversation                                                                           |
| Business impact    | Funded-and-traded conversion against the holdout                                                         |
| Advisor copilots   | Time to first contact, RM time spent on ready customers, share of copilot suggestions accepted or edited |

