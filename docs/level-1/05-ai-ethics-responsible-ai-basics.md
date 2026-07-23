# 05 · AI Ethics & Responsible AI Basics

AI ethics is frequently treated as an academic afterthought or a legal
checkbox, bolted onto a project after the model already exists. Handled that
way, it catches almost nothing that matters. Handled as a management
discipline built into the project from the start, it prevents the specific,
recurring, expensive failure modes covered in this module: biased outcomes,
inappropriate use cases, and a lack of accountability when something goes
wrong. You do not need a philosophy background — you need a short list of
concrete questions asked at the right moments.

## 1. Core responsible-AI principles, in plain terms

| Principle | What it means in practice | The management question to ask |
|---|---|---|
| **Fairness** | The model doesn't produce systematically worse outcomes for particular groups | "Have we tested performance broken out by relevant subgroups, not just in aggregate?" |
| **Transparency** | People affected by a model's decision can find out that AI was involved and get a basic explanation | "Can we tell an affected user *why* they got this outcome, in plain language?" |
| **Accountability** | A specific person or team owns the model's real-world consequences | "If this model causes harm, whose job is it to respond, and how fast?" |
| **Privacy** | Data used to train and run the model respects consent and minimizes exposure | "Did the people whose data trained this model agree to this use, even indirectly?" |
| **Safety** | The system fails in a contained, recoverable way rather than a catastrophic one | "What's the worst plausible thing this model could do, and is there a circuit breaker?" |

## 2. Where bias actually comes from

Bias is not something a data scientist "adds" through carelessness — it's
usually baked into the data or the problem framing before modeling even
starts. Knowing the common sources lets you ask about them early.

| Source | Example | Where it's caught |
|---|---|---|
| **Historical bias** | Training data reflects past discriminatory decisions (e.g., historical hiring data that favored one group) | Problem-framing stage — ask "does this data encode a past pattern we don't want to repeat?" |
| **Sampling bias** | Training data isn't representative of the real population the model will affect | Data-discovery stage — ask "who is underrepresented in this dataset?" |
| **Label bias** | The "correct answers" used for training reflect the biases of whoever labeled them | Data-preparation stage — ask "who labeled this, and what guidance did they follow?" |
| **Feedback-loop bias** | The model's own past decisions influence the data it's later trained on, amplifying an initial skew | Monitoring stage — ask "is this model training on outcomes it previously influenced?" |

## 3. A responsible-AI review checklist for managers

A lightweight checklist to run before a model reaches production, not a full
audit framework — the full frameworks are covered in Level 2's Responsible
AI Frameworks module.

| Check | Pass condition |
|---|---|
| Subgroup performance | Model performance has been measured separately for known-relevant subgroups (not just overall) |
| Use-case appropriateness | The use case has been explicitly reviewed against "should this decision be automated at all," not just "can it be" |
| Human-in-the-loop | A human can review or override the model's decision for consequential outcomes |
| Data consent | The training data's provenance and consent basis is documented, not assumed |
| Escalation path | There is a named owner and a defined process for handling a reported harm |
| Explainability | Someone affected by a decision can get a plain-language reason, even if the underlying model is complex |

## Worked example

A lending company builds a model to recommend loan approval likelihood. The
proof-of-concept shows strong aggregate accuracy. Before advancing to
integration, the AI manager runs the checklist above and requires the team
to break out performance by applicant zip code as a proxy check (direct
demographic data isn't used in the model, but zip code correlates with
protected characteristics in this market). The breakout reveals the model
underperforms — flags more false declines — for applicants from a cluster of
lower-income zip codes, traced back to those applicants being underrepresented
in the historical approval data used for training (a case of historical
bias feeding into sampling bias). The team is sent back to development to
either collect more representative data or adjust the modeling approach,
rather than launching a model that would have systematically disadvantaged
that group — a discovery made *before* launch specifically because the
subgroup-performance check was a gate, not an afterthought.

## Exercise

Take an AI project (real or plausible) from your own context. Run it through
the six-item checklist in section 3, writing one or two sentences for each
item on where the project currently stands (pass, fail, or unknown). For any
item marked "unknown," write the specific question you would ask the team
this week to resolve it, and who you'd need to ask.
