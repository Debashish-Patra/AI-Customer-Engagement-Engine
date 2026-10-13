# Customer Journey map

A new investor moves through six stages, from realising the need to invest to growing with the broker. The journey is weakest at Application & Verification, and an account only creates value once it is funded and traded. <br>
- Six stages: Awareness, Consideration, Application & Verification, Activation & Funding, First Trade & Engagement, Ongoing Engagement & Growth.
- Lowest point: Application & Verification, where the customer feels overwhelmed by the process (document upload failures, KYC errors, delayed approval). This is a working hypothesis, to be validated with data.
- Value is created after the account opens: funding, the first trade and continued activity drive AUM. We therefore propose measuring conversion as funded and traded, not as lead to account opened.

## The journey in one picture

<p align="center"><img width="827" height="335" alt="image" src="https://github.com/user-attachments/assets/23ad38f4-d25e-41bc-8902-639442a4ad25" />

The six stages run from first discovering the need to invest to growing with the broker. The pains cluster into three kinds: trust and clarity early on, process failures in the middle, and a guidance gap once the customer is trading.

## How customers feel
<p align="center"><img width="886" height="477" alt="image" src="https://github.com/user-attachments/assets/b7f68997-ddb5-48ed-992b-ed8afdd4c7e1" />

Customers start doubtful, dip to their lowest point at Application & Verification, peak at the first trade, then settle into being invested but unsure what to do next. The arc is a relative, qualitative view from a design exercise, not measured sentiment; the section on what we still need to validate says how to test it.
Two moments carry the most risk: the dip at Application, where the process itself is the problem, and the fall after the first trade, where guidance is the problem.

## Where value is created

<p align="center"><img width="800" height="327" alt="image" src="https://github.com/user-attachments/assets/22d7fffa-0fd6-43c9-9d08-64f575face21" />

## How the journey maps to the six layers
<p align="center"><img width="827" height="385" alt="image" src="https://github.com/user-attachments/assets/e24099e9-31a2-4fdd-9508-5902b148a88a" />

Every pain point follows the same path: the system detects a signal, decides and orchestrates an action, brings in a person where it matters, and measures the result. The full page maps all six stages this way.

The table below sets out the same mapping for every stage.

| Stage                       | Pain point                                             | Signal detected (Layers 1-2)                                           | AI and orchestration action (Layers 3-4)                                                 | Human role (Layer 5)                                                                                        |
|-----------------------------|--------------------------------------------------------|------------------------------------------------------------------------|------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| Awareness                   | Information overload                                   | Lead source and campaign; content viewed; fee-calculator use           | Send jargon-free comparison content matched to the interest shown                        | None by default                                                                                             |
| Consideration               | Hidden charges, confusing fees, negative reviews       | Repeat visits to pricing pages; fee comparison activity                | Show upfront fee disclosure; offer live chat; raise the lead's priority                  | Advisor call for high-intent leads                                                                          |
| Application & Verification  | Upload failures, KYC failures, delayed approval        | Application stalled at a step; time since last step; repeated failures | Nudge on the right channel to resume at the exact step; offer video KYC                  | Assisted completion for stalled or repeatedly failing applicants; operations escalation for approval delays |
| Activation & Funding        | Payment gateway failures                               | Account approved but unfunded; failed payment event                    | Instant UPI prompt; guided in-app walkthrough; zero-balance readiness prompt             | Call to high-value prospects; support for repeated failures                                                 |
| First Trade & Engagement    | Confusing order UI, unresponsive support               | Funded account with no first order                                     | Tooltips; first-trade reward; educational webinar invite                                 | RM or support outreach to customers who are stuck                                                           |
| Ongoing Engagement & Growth | Uncertainty on next step, inconsistent recommendations | Portfolio and behaviour data; product gaps; drop in activity           | Personalised insights; SIP and goal-based prompts; rebalancing nudges, within guardrails | RM check-ins for high-AUM clients, with the same recommendation context the system holds                    |

## Measuring the journey
Each stage gets one conversion metric and one friction metric, so a loss can be traced to the stage where it happens. Together they roll up to the proposed North Star in Layer 6, net new AUM. Baselines are not yet captured and are needed before any target is set.

| Stage                       | Conversion metric                                                      | Friction metric                                                          |
|-----------------------------|------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Awareness                   | Visitors who start an enquiry or application                           | Drop-off after first visit                                               |
| Consideration               | Enquiries that become applications                                     | Time spent on fee and pricing pages without action                       |
| Application & Verification  | Applications that complete KYC                                         | Drop-off by step; document upload and KYC failure rate; time to approval |
| Activation & Funding        | Approved accounts that are funded                                      | Payment failure rate; time from approval to first funding                |
| First Trade & Engagement    | Funded accounts that place a first order                               | Time from funding to first trade; support response time                  |
| Ongoing Engagement & Growth | Active customers adding SIPs or new products; net new AUM per customer | Inactivity rate; advisor check-in coverage for high-AUM clients          |

