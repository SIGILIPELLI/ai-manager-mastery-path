---
title: "AI Manager Cheat Sheet: Quick Reference, Beginner to Advanced"
description: "A free AI Manager cheat sheet: 40 quick-reference tables from every level of the AI Manager Mastery Path, each linked to its full lesson."
---

# AI Manager Cheat Sheet

Quick-reference tables from **40 lessons** of the free AI Manager Mastery Path, in course order from beginner to advanced. Each section links to the full lesson with explanations and runnable examples.

## Level 1 · Entry

### [01 · What Is AI Management?](level-1/01-what-is-ai-management.md)

*What an AI manager actually does*

| Activity | What it looks like day to day |
|---|---|
| **Scoping** | Translating a vague ask ("can we use AI to reduce churn?") into a specific, testable problem statement with a target metric |
| **Team leadership** | Managing or coordinating data scientists, ML engineers, MLOps engineers, and the product/design/legal partners around them |
| **Risk & governance** | Making sure the model's failure modes, data sources, and compliance exposure are understood *before* launch, not discovered after |
| **Delivery & iteration** | Running the project through experimentation, deployment, and the ongoing tuning that AI systems need after they ship |

### [02 · AI/ML Fundamentals for Managers](level-1/02-ai-ml-fundamentals-for-managers.md)

*The three flavors of "AI" you'll manage*

| Category | What it is | Example | Typical build cost/time |
|---|---|---|---|
| **Classical machine learning** | Statistical models trained on structured, tabular data to predict a number or category | Predicting customer churn from account history | Weeks; often the cheapest and most reliable option |
| **Deep learning / computer vision / traditional NLP** | Neural networks trained on unstructured data (images, audio, text) for a narrow task | Detecting defects in product photos | Months; needs labeled data and specialized talent |
| **Large language models (LLMs) / GenAI** | Massive pre-trained models adapted via prompting, fine-tuning, or retrieval, for open-ended language tasks | A chatbot, a document summarizer, a coding assistant | Days to weeks to prototype, but much longer to make reliable enough for production |

### [03 · Understanding AI Project Lifecycles](level-1/03-ai-project-lifecycles.md)

*The AI project lifecycle, stage by stage*

| Stage | Purpose | Typical duration | Manager's key decision |
|---|---|---|---|
| **1. Problem framing** | Turn a business ask into a specific, measurable ML/AI problem | Days to 2 weeks | Is this even a good fit for AI, or is a simpler rule-based solution sufficient? |
| **2. Data discovery** | Figure out what data exists, where it lives, and whether it's usable | 1–4 weeks | Do we have enough data, or does this become a "collect data first" project? |
| **3. Feasibility / proof of concept** | A quick, throwaway-quality experiment to test if the approach can work at all | 2–6 weeks | Go/no-go: does the early signal justify further investment? |
| **4. Model development** | Iterative building, training, and evaluation of candidate models | Weeks to months | Have we hit the pre-agreed quality bar, or do we need another iteration (or to reset scope)? |
| **5. Integration & productionization** | Wrapping the model in real infrastructure: APIs, monitoring, fallback logic | Weeks to months (often underestimated) | Is this ready for real users, or does it need a staged/limited rollout first? |
| **6. Launch** | Releasing to real users, often gradually | Days to weeks | What's the rollback plan if something goes wrong? |
| **7. Monitoring & iteration** | Ongoing tracking of live performance, retraining as needed | Indefinite — this never "finishes" | Is the model still meeting the bar, or has drift eroded it? |

### [04 · Managing Data Science &amp; ML Teams](level-1/04-managing-data-science-ml-teams.md)

*The roles on a typical AI/ML team*

| Role | What they own | Common misconception to avoid |
|---|---|---|
| **Data scientist** | Exploring data, building and evaluating candidate models, statistical rigor | Not the same as a data analyst — the job is building predictive systems, not just reporting on past data |
| **ML engineer** | Turning a validated model into reliable, scalable production code | Distinct skill set from data science — strong data scientists are not automatically strong production engineers |
| **MLOps / platform engineer** | Infrastructure for training, deployment, monitoring, and versioning of models | Often the most understaffed role relative to its importance — see Level 2 for the dedicated module |
| **Data engineer** | Building and maintaining the pipelines that feed clean data to everyone else | The unsung foundation — a weak data engineering function silently caps everyone else's output |
| **Domain / subject-matter expert (SME)** | Providing the business context that keeps the model solving the right problem | Frequently left out of the loop after the kickoff meeting — a costly mistake |

### [05 · AI Ethics &amp; Responsible AI Basics](level-1/05-ai-ethics-responsible-ai-basics.md)

*Core responsible-AI principles, in plain terms*

| Principle | What it means in practice | The management question to ask |
|---|---|---|
| **Fairness** | The model doesn't produce systematically worse outcomes for particular groups | "Have we tested performance broken out by relevant subgroups, not just in aggregate?" |
| **Transparency** | People affected by a model's decision can find out that AI was involved and get a basic explanation | "Can we tell an affected user *why* they got this outcome, in plain language?" |
| **Accountability** | A specific person or team owns the model's real-world consequences | "If this model causes harm, whose job is it to respond, and how fast?" |
| **Privacy** | Data used to train and run the model respects consent and minimizes exposure | "Did the people whose data trained this model agree to this use, even indirectly?" |
| **Safety** | The system fails in a contained, recoverable way rather than a catastrophic one | "What's the worst plausible thing this model could do, and is there a circuit breaker?" |

### [06 · Setting AI Project Expectations](level-1/06-setting-ai-project-expectations.md)

*Why AI timelines are inherently uncertain*

| Traditional estimate | AI project estimate |
|---|---|
| "This feature takes 3 weeks" | "The proof of concept takes 3 weeks; whether it's viable to proceed is the outcome of those 3 weeks, not a given" |
| Effort scales roughly linearly with scope | Effort can be dominated entirely by one unknown (data quality, achievable accuracy) that no amount of extra headcount fixes |
| Missing a deadline usually means "not done yet" | Missing a quality bar can mean "not achievable with this approach," which is a different conversation entirely |

### [07 · AI Vendor &amp; Tool Evaluation Basics](level-1/07-ai-vendor-tool-evaluation.md)

*Categories of AI vendors you'll evaluate*

| Category | What they provide | Example decision you'll make |
|---|---|---|
| **Foundation model / API providers** | Access to a pre-trained LLM or other model via an API | Which provider's model, and which specific model tier, fits our latency/cost/quality needs |
| **ML platform vendors** | Infrastructure for training, deploying, and monitoring your own models | Build this infrastructure in-house vs. buy a managed platform |
| **Data labeling vendors** | Human or hybrid human/AI labeling of training data | In-house labeling team vs. outsourced vendor, and how to verify their quality |
| **Point-solution AI vendors** | A complete, pre-built AI feature (e.g., a chatbot platform, a fraud-detection product) | Buy a complete solution vs. build a custom model |

### [08 · Communicating AI Concepts to Non-Technical Stakeholders](level-1/08-communicating-ai-to-stakeholders.md)

*The translation table: technical concept → business language*

| Technical concept | Business translation |
|---|---|
| "Model accuracy is 87%" | "Out of 100 typical cases, the system gets about 87 right — we'll walk through what the other 13 look like and how we handle them" |
| "We're seeing model drift" | "The system's real-world performance has started slipping as customer behavior has shifted since we trained it — we're refreshing it" |
| "The model hallucinates sometimes" | "The system can occasionally state something confidently that isn't true — here's exactly where we've built in a human check for that" |
| "We need more labeled data" | "We need more examples of correct answers to teach the system from — here's the specific gap and what it'd take to close it" |
| "Precision vs. recall tradeoff" | "We can tune this to catch more real cases (at the cost of more false alarms) or fewer false alarms (at the cost of missing more real cases) — here's the mix we'd recommend and why" |

### [09 · AI Risk Basics](level-1/09-ai-risk-basics.md)

*The core AI risk categories*

| Risk category | What it looks like | Where it tends to originate |
|---|---|---|
| **Bias / unfair outcomes** | Systematically worse results for particular groups | Training data, problem framing (see Module 5) |
| **Hallucination** (LLM-specific) | Confidently generated but false or fabricated output | Inherent to how generative models work — not fully eliminable, only mitigated |
| **Security / adversarial risk** | Inputs deliberately crafted to manipulate the model's output (prompt injection, data poisoning, model extraction) | Anywhere the model accepts untrusted input, especially user-facing LLM features |
| **Privacy leakage** | The model reveals sensitive information from its training data or from other users' inputs | Training on insufficiently anonymized data, or shared context across users |
| **Overreliance / automation complacency** | Humans stop critically reviewing AI output because it's usually right | Any system without a deliberate human-in-the-loop check for consequential decisions |
| **Model drift** | Performance degrades silently as real-world data shifts | Absence of ongoing monitoring after launch |

### [10 · Project — AI Project Charter &amp; Risk Assessment](level-1/10-project-ai-charter-risk-assessment.md)

*Problem statement &amp; success metric*

| Field | Your entry |
|---|---|
| Business problem (one sentence, no jargon) | |
| AI/ML category (classical ML / deep learning / LLM-GenAI — Module 2) | |
| Primary success metric | |
| Minimum acceptable threshold | |
| Baseline (what a simple non-AI approach would achieve) | |

## Level 2 · Intermediate

### [01 · Managing ML Experimentation &amp; Iteration](level-2/01-managing-ml-experimentation.md)

*What an experiment actually is*

| Weak framing (avoid) | Strong framing (use) |
|---|---|
| "Improve the churn model" | "Adding 90-day support-ticket history as a feature raises recall at fixed precision by ≥3 points" |
| "Try the new embedding model" | "Swapping to the new embedding model improves retrieval hit-rate@5 by ≥5 points on our 400-query eval set" |
| "Explore whether an LLM could help" | "An LLM classifies inbound email into our 12 routing categories at ≥85% agreement with a human labeler on 300 held-out emails" |
| "Reduce hallucinations" | "Adding retrieval grounding cuts unsupported-claim rate from 14% to ≤6% on the 200-item factuality eval" |

### [02 · AI Product Metrics](level-2/02-ai-product-metrics.md)

*The three layers of AI metrics*

| Layer | Example metrics | Who watches it | Update frequency |
|---|---|---|---|
| **Model metrics** | Precision, recall, AUC, hit-rate@k, agreement with human labels | ML team | Every experiment |
| **Product metrics** | Suggestion-acceptance rate, override rate, time-to-resolution, task completion | Product + AI manager | Weekly |
| **Business metrics** | Revenue retained, cost avoided, fraud losses, headcount hours saved | Sponsor, finance | Monthly / quarterly |

### [03 · MLOps Fundamentals for Managers](level-2/03-mlops-fundamentals-for-managers.md)

*The seven jobs MLOps covers*

| Job | The question it answers | Who feels it when it's missing |
|---|---|---|
| **Data pipelines** | Does the model get fresh, correct data on a schedule? | Everyone, eventually |
| **Reproducibility** | Can we rebuild the exact model that's in production today? | Auditors, and anyone debugging |
| **Versioning** | Which model, data, and code combination is live right now? | Incident responders |
| **Deployment** | How does a new model reach users, and how fast can it be undone? | Product, during a bad release |
| **Monitoring** | Would we notice if quality dropped? How quickly? | Customers, first |
| **Retraining** | What triggers a refresh, and who approves it? | Finance, via slow decay |
| **Governance & audit** | Can we show who approved what, and why? | Legal and compliance |

### [04 · Data Governance Basics](level-2/04-data-governance-basics.md)

*The five questions governance answers*

| Question | Concretely | Symptom when unanswered |
|---|---|---|
| **Who owns it?** | A named person who can approve access and is accountable for quality | Requests bounce between teams for weeks |
| **Who may use it, for what?** | Documented purposes; a route to request new ones | Everyone gets everything, or nobody gets anything |
| **Where did it come from?** | Source system, collection basis, transformations applied | Nobody can explain a number to an auditor |
| **How good is it?** | Agreed thresholds for completeness, freshness, accuracy | Silent model degradation |
| **How long may we keep it?** | Retention period and deletion mechanism per category | Data hoarding, and deletion requests that can't be honoured |

### [05 · Managing Cross-Functional AI Teams](level-2/05-managing-cross-functional-ai-teams.md)

*The five parties and what each is really optimising*

| Function | Optimising for | Their nightmare | Their clock |
|---|---|---|---|
| **Data science / ML** | Model quality on a defined metric | Shipping something that doesn't work and being blamed for it | Weeks per experiment; irregular |
| **Engineering / platform** | Reliability, latency, maintainability | Being handed a notebook and told to productionise it by Friday | Sprints; predictable |
| **Product** | User outcome and business metric | Building something correct that nobody uses | Roadmap quarters |
| **Legal / compliance / privacy** | Defensibility; no unacceptable exposure | Finding out after launch | Reactive; slow when surprised, fast when warned |
| **Design / UX** | Comprehensible, appropriately trusted experience | A confident-sounding system that misleads users | Ahead of build |

### [06 · AI Procurement &amp; Build-vs-Buy Decisions](level-2/06-ai-procurement-build-vs-buy.md)

*There are four options, not two*

| Option | What it means | Best when |
|---|---|---|
| **Buy** | Commercial product handles the capability end to end | The capability is undifferentiated and a mature market exists |
| **Build** | You develop and operate it | The capability *is* your differentiation, or your data makes it uniquely feasible |
| **Buy and wrap** | Vendor model or API underneath; your orchestration, data, evaluation, and UX on top | Very common in practice — the model is a commodity, the integration is not |
| **Don't** | Solve it with a rule, a process change, or not at all | More often than anyone admits |

### [07 · Responsible AI Frameworks](level-2/07-responsible-ai-frameworks.md)

*The framework landscape*

| Framework | What it is | Best used as | Certifiable? |
|---|---|---|---|
| **NIST AI Risk Management Framework** | A voluntary US framework organised around four functions — Govern, Map, Measure, Manage | Your internal operating structure; the most practical starting point | No |
| **ISO/IEC 42001** | A management-system standard for AI, structured like ISO 27001 | Formal assurance; useful when customers demand evidence | Yes, via audit |
| **EU AI Act** | Regulation with obligations tiered by risk level | A compliance obligation if you touch the EU market — not optional | Conformity assessment for high-risk |
| **OECD AI Principles** | High-level intergovernmental principles | Vocabulary and executive framing | No |
| **Sector rules** | Financial model-risk governance, medical device regulation, employment law | Often the binding constraint, ahead of any AI-specific rule | Varies |

### [08 · Change Management for AI Adoption](level-2/08-change-management-ai-adoption.md)

*The adoption funnel*

| Stage | Question | Typical metric | If it fails here |
|---|---|---|---|
| **Aware** | Do they know it exists and what it's for? | % of target population who can describe it | Communications problem — cheap to fix |
| **Able** | Do they have access, permission and enough skill? | % with working access; % who completed onboarding | Enablement problem — usually IT or training |
| **Activated** | Have they tried it on real work? | % with at least one genuine use | Trigger problem — it isn't in their workflow |
| **Repeating** | Do they come back unprompted? | Weekly active as % of target population | Value problem — it didn't help enough |
| **Relying** | Has the old way stopped? | % of eligible work done the new way | Trust or workflow problem |
| **Right-sized trust** | Do they accept good output and catch bad? | Override rate; error escape rate | Calibration problem — the dangerous one |

### [09 · Budgeting for AI Projects](level-2/09-budgeting-for-ai-projects.md)

*Where the money actually goes*

| Cost category | What it covers | Typical share | Behaves like |
|---|---|---|---|
| **People — build** | ML, data and platform engineering; product; design | 45–65% | Fixed, for the period |
| **People — run** | Maintenance, retraining, on-call, improvement | 15–25% | Fixed, forever |
| **Data work** | Sourcing, cleaning, labelling, annotation vendors | 5–20% | Lumpy; recurs on every refresh |
| **Evaluation** | Building and refreshing the eval set; human review of outputs | 2–8% | Recurring, underestimated |
| **Training / experiment compute** | Runs during development | 1–10% | Bursty, capped by discipline |
| **Inference / serving** | Per-call model fees or hosted infrastructure | 1–15% | **Variable with usage** |
| **Platform & MLOps** | Tracking, registry, monitoring, orchestration (Module 03) | 3–8% | Fixed, plus per-system |
| **Vendor & licence** | Third-party products, per-seat or per-unit | 0–30% | Contractual |
| **Governance** | Legal, privacy, bias analysis, audit, review forums (Module 07) | 2–6% | Per-system, tier-dependent |
| **Change management** | Enablement, training, comms, adoption support (Module 08) | 3–10% | One-off, then a trickle |

### [10 · Project — Design an MLOps Process for a Team](level-2/10-project-mlops-process.md)

*The shape of the deliverable*

| Section | The question it settles | Length | Fails when |
|---|---|---|---|
| **0. Scope & tiers** | Which systems does this apply to, at what intensity? | ½ page | One process is applied to everything equally |
| **1. Experimentation** | What gets recorded, and what counts as a result? | ½ page | Recording is aspirational, not enforced |
| **2. Deployment gates** | What must be true before traffic moves? | 1 page | Gates exist but have no named approver |
| **3. Monitoring & response** | What is watched, by whom, and what happens on alert? | 1 page | Alerts route to a channel, not a person |
| **4. Governance & evidence** | What is retained, and who can produce it? | ½ page | Evidence is assembled on request rather than as a by-product |

## Level 3 · Advanced

### [01 · Scaling AI Teams](level-3/01-scaling-ai-teams.md)

*The three scaling thresholds*

| Threshold | Symptom that tells you you're there | Structural fix |
|---|---|---|
| ~8-10 ICs, one team | Standup runs long; people learn about each other's work in standup, not before | Split into 2 pods by problem area, keep one manager |
| ~25-30 ICs, multiple pods | Pods duplicate infrastructure (two feature stores, two eval harnesses) | Stand up a platform/enablement function |
| ~60+ ICs, platform exists | Platform team becomes a bottleneck; pods route around it with shadow tooling | Platform shifts from "build for pods" to "build with pods"; embed platform liaisons |

### [02 · AI Governance &amp; Compliance](level-3/02-ai-governance-compliance.md)

*The regulatory landscape, at manager altitude*

| Regime | Applies to | What it requires in practice |
|---|---|---|
| EU AI Act | Any AI system used in or affecting the EU market, tiered by risk | High-risk systems (hiring, credit, health) need conformity assessment, documentation, human oversight, logging |
| US sectoral rules (e.g., ECOA, FCRA, HIPAA, EEOC guidance) | Credit, employment, health, insurance decisions in the US | Adverse-action explanations, non-discrimination testing, data handling per sector rules |
| State AI laws (e.g., Colorado AI Act, NYC Local Law 144) | Automated employment decisions, consumer-facing high-risk AI in that state | Bias audits (often annual, third-party), notice to affected individuals |
| GDPR / state privacy laws | Any system processing personal data of covered individuals | Lawful basis for processing, right to explanation for automated decisions, data minimization |
| Sector-specific supervisory guidance (e.g., banking regulators on model risk) | Regulated financial institutions | Formal model risk management (validation, ongoing monitoring, documented limitations) |

### [03 · Managing LLM/GenAI Initiatives](level-3/03-managing-llm-genai-initiatives.md)

*What's actually different about LLM initiatives*

| Dimension | Classical ML project | LLM/GenAI project |
|---|---|---|
| Where the capability comes from | Usually trained in-house on your data | Usually a third-party foundation model, adapted via prompting or fine-tuning |
| Cost structure | Mostly fixed (compute for training), predictable | Variable, per-token, scales with usage — can spike unexpectedly |
| Output space | Bounded (a class, a score, a ranked list) | Open-ended text/code/image — infinite failure surface |
| Evaluation | Fixed metric on a frozen holdout | Harder to define "correct"; often needs human or LLM-judge grading |
| Failure mode | Wrong prediction | Wrong prediction *plus* hallucination, prompt injection, unsafe/off-brand output |
| Vendor dependency | Usually low (your model, your infra) | Often high (model version changes, deprecations, and price changes are outside your control) |
| Time to first demo | Weeks (needs data + training) | Hours (a good prompt looks like a product) — creating a "it's basically done" illusion |

### [04 · AI Talent Strategy](level-3/04-ai-talent-strategy.md)

*The AI role taxonomy*

| Role | Core skill | Where they add value | Common mis-hire |
|---|---|---|---|
| Research scientist | Novel modeling, published or publishable work | Genuinely new capability, competitive differentiation | Hired for a role that's really "apply an existing off-the-shelf model" |
| Applied ML engineer | Adapting known techniques to your data and product | Most day-to-day model-building work | Expected to also do research-level innovation on a production timeline |
| ML/MLOps engineer | Production infrastructure, deployment, monitoring | Making models reliable and observable in production | Treated as "just DevOps," under-involved in model design decisions |
| Data engineer | Pipeline reliability, data quality at scale | The unglamorous 60% of most AI projects' actual effort | Understaffed relative to ML headcount, becomes the bottleneck |
| AI/LLM product engineer | Prompt engineering, eval design, product integration | GenAI features specifically — a distinct skill from classical ML | Assumed to be interchangeable with a general software engineer |

### [05 · Cross-Team AI Platform Strategy](level-3/05-cross-team-ai-platform-strategy.md)

*The build-a-platform decision framework*

| Signal | Threshold worth acting on | How to verify it's real, not anecdotal |
|---|---|---|
| Duplicated infrastructure | 2+ teams independently building the same capability (feature store, eval harness, model registry) | Audit actual tooling in use across teams, not what's on a slide |
| Duplicated vendor spend | 2+ teams separately licensing overlapping tools | Pull vendor contracts, check for overlap in capability, not just vendor name |
| Inconsistent standards causing incidents | An incident traced to one pod's practice not matching another's (see Module 6) | Root-cause reports citing "no shared standard" as a contributing factor |
| Onboarding friction | New hires or transfers report re-learning tooling per pod | Exit/transfer interview data, not just complaints in a hallway |

### [06 · Managing AI Incidents &amp; Model Failures](level-3/06-managing-ai-incidents.md)

*AI-specific failure modes*

| Failure mode | What it looks like | Typical detection lag if unmonitored |
|---|---|---|
| Data/concept drift | Model accuracy degrades gradually as real-world patterns shift away from training data | Weeks to months |
| Silent input schema change | An upstream data source changes format; model runs but consumes garbage | Days to weeks |
| Feedback loop degradation | Model's own outputs pollute the data it's later trained or evaluated on | Months |
| Hallucination / factual error (LLM) | Confidently wrong output, no error thrown | Immediate to never, depending on whether anyone checks |
| Bias/fairness regression | Disparate outcome across a protected group emerges post-launch | Months, often only found by external audit |
| Prompt injection / jailbreak (LLM) | Adversarial input causes the model to ignore its instructions | Immediate if logged, otherwise indefinite |
| Vendor-side model change | Foundation model provider updates the model; behavior shifts without your code changing | Days, if output monitoring exists |

### [07 · AI ROI Measurement](level-3/07-ai-roi-measurement.md)

*The AI ROI components*

| Component | Definition | Measurement difficulty |
|---|---|---|
| Hard cost savings | Directly measurable reduction in labor, compute, or operational spend | Low — usually has a clean before/after number |
| Revenue impact | Increased conversion, retention, or average order value attributable to the AI feature | Medium — needs a controlled comparison (A/B test or matched cohort) |
| Risk/cost avoidance | Fraud caught, compliance violations prevented, incidents avoided | Medium-high — requires a credible counterfactual estimate |
| Soft/strategic value | Improved decision speed, employee satisfaction, competitive positioning | High — rarely quantifiable with confidence; report qualitatively, don't force a dollar figure |

### [08 · Vendor &amp; Partner Management for AI](level-3/08-vendor-partner-management.md)

*Build vs. buy vs. partner — the decision framework*

| Factor | Favors build | Favors buy (vendor product) | Favors partner (co-development) |
|---|---|---|---|
| Differentiation | Core to competitive advantage | Commodity capability, not a differentiator | Strategic but you lack in-house depth |
| Data sensitivity | Highly sensitive data that can't leave your environment | Vendor has strong compliance posture, contractually verified | Depends entirely on the specific data-sharing terms |
| Time to value | You can tolerate a longer build timeline | Need capability in weeks, not quarters | Willing to trade some timeline for shared IP/cost |
| Total cost of ownership over 3 years | In-house team cost is lower than vendor fees at your scale | Vendor's economies of scale beat your build+maintain cost | Shared cost, shared (and negotiated) upside |
| Long-term flexibility needed | High — you expect requirements to diverge significantly from any vendor roadmap | Low — a standard capability with well-understood requirements | Medium — negotiate roadmap input as part of the deal |

### [09 · Building AI Centers of Excellence](level-3/09-building-ai-centers-of-excellence.md)

*What a CoE is (and isn't)*

| It is | It isn't |
|---|---|
| A standards-and-enablement function that makes pods faster and more consistent | A second engineering team that builds AI features itself |
| A place where cross-cutting expertise (governance, evaluation, ethics review) lives once instead of per-pod | A gatekeeper that approves or blocks every pod's technical decision |
| Advisory + tooling, with narrow direct authority (e.g., final sign-off on high-risk system launches) | A catch-all for "AI stuff that doesn't fit elsewhere" |
| Measured by pod adoption and outcomes it improved | Measured by its own headcount growth or activity volume |

### [10 · Project — An AI Governance Framework for an Organization](level-3/10-project-ai-governance-framework.md)

*System-of-record inventory*

| System | Risk tier | Rationale | Owner | Last reviewed |
|---|---|---|---|---|
| Demand-forecasting model | Medium | Informs customer business decisions but with human review before action; no protected-class decision | Pod A lead | New — first review this cycle |
| Anomaly-detection alerts | Low-Medium | Flags for human review, doesn't act autonomously | Pod A lead | New |
| Sales-lead scoring | Low | Internal only, no customer-facing decision, no protected category | Pod B lead | New |
| LLM support assistant | Medium-High | Customer-facing, EU exposure, handles account data, could give incorrect operational guidance | Pod B lead | New (pre-launch review overdue — flagged) |

## Level 4 · Master

### [01 · Executive AI Strategy](level-4/01-executive-ai-strategy.md)

*The AI strategy positioning matrix*

| | Low differentiation potential | High differentiation potential |
|---|---|---|
| **Core to your business model** | Efficiency play — automate to reduce cost, match industry baseline (e.g., AI-assisted customer support for most companies) | Strategic bet — this is where competitive advantage is actually won or lost; deserves disproportionate investment and executive attention |
| **Peripheral to your business model** | Buy, don't build — commodity vendor tools, minimal internal investment | Selective build — only if a peripheral capability could become core later (rare; verify before over-investing) |

### [02 · Org Design for AI-First Companies](level-4/02-org-design-ai-first-companies.md)

*Three org design archetypes*

| Archetype | Structure | Best fit | Main risk |
|---|---|---|---|
| Centralized AI org | One AI org reporting to a CAIO/CTO, serving all business units as an internal service | Company where AI capability needs to be consistent and shared across many similar use cases | Slower response to business-unit-specific needs; can become a bottleneck |
| Embedded model | AI talent distributed into business units, reporting to unit leaders, with a thin central standards function | Company where AI use cases are highly differentiated by business unit | Duplicated effort, inconsistent standards, harder to build shared platform (Level 3 Module 5) |
| Hybrid ("hub and spoke") | Central hub owns platform/standards/governance; embedded "spokes" own business-unit-specific application | Most large, multi-business-unit companies past a certain scale | Requires genuinely clear division of authority (see Level 3 Module 9) or it collapses into either pure model under pressure |

### [03 · AI Portfolio Management](level-4/03-ai-portfolio-management.md)

*Risk-adjusted value — the core comparison tool*

| Project | Projected annual value | Estimated success probability | Risk-adjusted value |
|---|---|---|---|
| A: Support deflection (LLM) | $1.7M | 90% (proven technique, similar to Level 3 Module 7's worked example) | $1.53M |
| B: Personalization engine | $4.2M | 50% (high upside, unproven at this company's data scale) | $2.10M |
| C: Fraud detection upgrade | $2.1M | 80% (incremental improvement to existing system) | $1.68M |
| D: Generative design tool | $3.0M | 30% (novel application, no internal precedent) | $0.90M |

### [04 · Leading Through AI Disruption](level-4/04-leading-through-ai-disruption.md)

*The disruption honesty spectrum*

| Failure mode | What it looks like | Why it backfires |
|---|---|---|
| False reassurance | "AI will only augment your work, no jobs are at risk" — stated as certainty when it isn't | Loses all credibility the first time a role is affected; people stop believing anything leadership says about AI afterward |
| Premature alarm | Announcing broad AI-driven restructuring before specific plans exist | Triggers a talent exodus of your best people (who have the most external options) before you've decided anything, often worse than the disruption itself |

### [05 · AI Regulation &amp; Policy at Scale](level-4/05-ai-regulation-policy-at-scale.md)

*Multi-jurisdiction exposure mapping*

| Jurisdiction | Current posture (as of 2026) | Key obligation for high-risk AI |
|---|---|---|
| EU | Comprehensive, risk-tiered (AI Act), phased implementation | Conformity assessment, documentation, human oversight for high-risk categories |
| United States (federal) | Sectoral, no single comprehensive federal AI law; agency guidance (FTC, EEOC) plus executive orders that shift with administrations | Existing sectoral law (credit, employment, health) applies to AI decisions the same as any decision |
| US states | Increasingly active — comprehensive state AI laws (e.g., Colorado) and narrower ones (e.g., NYC automated employment decision tools) | Varies significantly; often requires bias audits and consumer notice |
| China | Algorithm registration and content requirements, especially for generative AI | Registration with regulators, content moderation obligations |
| Other major markets (UK, Canada, Japan, Brazil) | Mixed — ranging from principles-based guidance to emerging comprehensive frameworks | Varies; monitor actively rather than assuming parity with EU/US |

### [06 · Board-Level AI Reporting](level-4/06-board-level-ai-reporting.md)

*The standing AI board report structure*

| Section | Content | Length |
|---|---|---|
| Strategic positioning | Where AI stands relative to the positioning matrix (Module 1) and portfolio allocation (Module 3); material changes since last report | 1 slide/page |
| Performance | Realized ROI vs. projection for the top 3-5 initiatives (Level 3 Module 7), portfolio risk-adjusted value trend | 1 slide/page |
| Risk and governance | Governance inventory summary (Level 3 Module 2), any incidents since last report (Level 3 Module 6), regulatory exposure changes (Module 5) | 1-2 slides/pages |
| Forward look | Upcoming decisions needing board input, key risks to watch | 1 slide/page |

### [07 · Building AI Culture](level-4/07-building-ai-culture.md)

*The culture-practice gap diagnostic*

| Question | What a "yes" reveals |
|---|---|
| Do people report bad results (a failed experiment, a governance red flag) as readily as good ones? | Psychological safety around negative findings — the single highest-leverage culture indicator |
| Would a junior engineer feel comfortable escalating a senior engineer's skipped eval step? | Whether hierarchy suppresses safety-relevant dissent |
| Do teams under deadline pressure skip governance steps, and does anyone notice when they do? | Whether governance is a genuine practice or theater that collapses under pressure |
| Can someone describe a time leadership visibly changed a decision because of an AI risk finding? | Whether risk-flagging has ever actually mattered, or is treated as symbolic |

### [08 · M&amp;A and AI Capability Integration](level-4/08-ma-ai-capability-integration.md)

*AI-specific technical diligence*

| Diligence item | What to check | Red flag |
|---|---|---|
| Data rights and provenance | Does the target actually have rights to the data its models were trained on, including for the acquirer's intended future use? | Data licensed for the target's original narrow use case, not transferable or expandable |
| Model reproducibility | Can the target's team retrain their key model from scratch with documented data and process? | "Only one person knows how to do this" or training pipeline undocumented |
| Technical debt in the eval/monitoring layer | Does real production monitoring exist, or does the demo represent best-case performance never validated at scale? | No production monitoring; quality claims based only on offline eval |
| Vendor dependency | Is the target's core capability actually built on a foundation model or vendor API that could be replicated without the acquisition? | The "proprietary AI" is a thin wrapper around a widely available API, with no real moat |
| Governance and compliance history | Has the target been through any AI-specific regulatory scrutiny, and what does its (Level 3 Module 2-style) governance inventory actually look like? | No governance inventory exists; target can't produce documentation for its highest-risk systems |

### [09 · Career Growth: AI Manager to Chief AI Officer](level-4/09-career-growth-ai-manager-to-caio.md)

*The progression map*

| Level | Primary accountability | What changes from the level below | Where people get stuck |
|---|---|---|---|
| AI Manager | One team's delivery and technical quality | — | Staying too hands-on technically as team grows past ~8 people |
| Senior Manager / Director of AI | Multiple teams/pods, cross-team standards | Shift from "review the work" to "set the standard others review against" | Failing to build the platform/governance functions (Level 3 Modules 5, 9) that scale beyond personal oversight |
| VP of AI | Portfolio-level resource allocation, exec-team visibility | Shift from "run the work" to "decide what work gets funded" (Module 3) | Continuing to advocate for own pet projects rather than allocating impartially across the portfolio |
| Chief AI Officer | Company-wide AI strategy, board accountability | Shift from "manage the function" to "represent AI as a business strategy to the board and market" (Modules 1, 6) | Staying too deep in technical/operational detail instead of strategic positioning and external communication |

### [10 · Capstone — Full AI Strategy, Governance &amp; Org Design](level-4/10-capstone-ai-strategy-governance-org-design.md)

*Strategic positioning (Module 1)*

| Capability | Business unit | Quadrant | Rationale |
|---|---|---|---|
| Credit-risk underwriting model | Consumer lending | Core, high-differentiation | Direct driver of loss rates and approval speed; genuine competitive lever in this market |
| Personalized wealth-advisory recommendations | Wealth management | Core, high-differentiation | Client retention and AUM growth tied directly to recommendation quality |
| Fraud detection | All units | Core, low-differentiation | Table-stakes; every competitor has comparable capability | 
| Internal document processing automation | Small-business banking | Peripheral, low-differentiation | Efficiency play; buy, don't build |
| LLM-based client chat support | Wealth management | Core, medium-differentiation | Emerging; not yet proven as a differentiator but core to the client relationship if it works |

---

Go deeper with the full [AI Manager Mastery Path](index.md) curriculum or test yourself with the [interview questions](interview-questions.md).
