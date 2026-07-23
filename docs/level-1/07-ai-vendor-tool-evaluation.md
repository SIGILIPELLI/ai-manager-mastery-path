# 07 · AI Vendor & Tool Evaluation Basics

Very few AI managers build every capability in-house — most decisions
involve evaluating an LLM API provider, an ML platform, a labeling vendor, or
a pre-built AI feature to buy rather than build. This is a distinct skill
from general software vendor evaluation, because AI vendors sell you
something with probabilistic, hard-to-verify-in-a-demo quality claims. This
module gives you a structured way to evaluate AI vendors and tools without
needing to independently reproduce their benchmarks.

## 1. Categories of AI vendors you'll evaluate

| Category | What they provide | Example decision you'll make |
|---|---|---|
| **Foundation model / API providers** | Access to a pre-trained LLM or other model via an API | Which provider's model, and which specific model tier, fits our latency/cost/quality needs |
| **ML platform vendors** | Infrastructure for training, deploying, and monitoring your own models | Build this infrastructure in-house vs. buy a managed platform |
| **Data labeling vendors** | Human or hybrid human/AI labeling of training data | In-house labeling team vs. outsourced vendor, and how to verify their quality |
| **Point-solution AI vendors** | A complete, pre-built AI feature (e.g., a chatbot platform, a fraud-detection product) | Buy a complete solution vs. build a custom model |

## 2. A structured evaluation framework

Don't evaluate an AI vendor purely on a sales demo — demos are, by design,
run on the vendor's best-case examples. Use a structured framework instead:

| Dimension | What to check | Red flag |
|---|---|---|
| **Accuracy on your data** | Ask to run a pilot or evaluation on a *sample of your own data*, not just their published benchmark | Vendor resists or can't support testing on your own data before purchase |
| **Cost model at your scale** | Get pricing at your actual expected volume, not the entry tier | Pricing that scales unpredictably or requires a large volume commitment before you've validated fit |
| **Data handling & privacy** | Where is your data processed/stored, is it used to train their models for other customers | Vague or evasive answers about whether your data trains their shared models |
| **Latency & reliability** | Real p95/p99 latency numbers and uptime SLA, not just "fast" | No SLA offered, or an SLA with no meaningful penalty for breach |
| **Lock-in risk** | How hard is it to switch away later (proprietary formats, exclusive contracts) | No clear data-export path if you need to leave |
| **Support & roadmap transparency** | Access to a real support channel, and visibility into upcoming breaking changes | Support only via a ticket queue with no SLA, or a history of undocumented breaking API changes |

## 3. Build vs. buy: the questions that actually decide it

"Should we build this or buy it" is one of the most consequential AI
management decisions, and it's frequently made on gut feeling. Ground it in
specifics instead (the full build-vs-buy decision process is covered in
Level 2's dedicated module — this is the entry-level version):

| Question | Leans toward Buy | Leans toward Build |
|---|---|---|
| Is this capability core to our competitive advantage? | No — it's a commodity capability (e.g., generic text summarization) | Yes — it's the thing that differentiates our product |
| Does a vendor already do this well at our required quality bar? | Yes, verified on our own data | No — vendors underperform on our specific data/use case |
| Do we have the in-house talent to build and maintain this? | No, and hiring for it is slow/expensive | Yes, and we already have adjacent expertise |
| What's the total cost over 2–3 years, not just year one? | Vendor cost is lower or comparable at our real scale | Vendor cost compounds expensively at our scale; build amortizes better |

## Worked example

A customer-support team is evaluating whether to buy a third-party AI
chatbot platform or build a custom one on top of a foundation-model API. The
AI manager runs the vendor's platform against a sample of 200 real,
anonymized past support tickets (not the vendor's demo script) and finds it
correctly resolves 61% without escalation — below the vendor's advertised
85%, because the advertised number was measured on a curated FAQ-style
ticket set that doesn't match this company's actual ticket mix. Pricing at
the company's real monthly ticket volume also turns out to be 3x the entry
quote once true volume is applied. Combined with the build-vs-buy table
showing support quality as a genuine differentiator for this company (its
tickets are unusually technical), the manager recommends building a custom
solution on a foundation-model API instead — a decision made possible only
because the evaluation used the company's own data and real volume rather
than trusting the vendor's headline numbers.

## Exercise

Pick an AI vendor or tool your organization is considering (or a plausible
one — an LLM API provider, a labeling vendor, a chatbot platform). Fill out
the six-dimension evaluation table from section 2 with real or best-guess
answers for each row, explicitly marking any row as "unknown — need to ask
the vendor." Then answer the four build-vs-buy questions from section 3 for
the same capability, and state your recommendation in one sentence.
