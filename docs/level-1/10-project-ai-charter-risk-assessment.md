# 10 · Project — AI Project Charter & Risk Assessment

This capstone pulls together every module in Level 1 into the single
document an AI manager should produce before real work begins on any new AI
initiative: a **project charter with an embedded risk assessment**. This is
not a theoretical exercise — the template below is the same shape you'd use
on a real project, and by the end of this module you'll have filled one out
completely for a project of your own choosing.

## Why a charter, and why now

A charter forces the scoping (Module 1), fundamentals (Module 2), lifecycle
planning (Module 3), team structure (Module 4), ethics review (Module 5),
expectation-setting (Module 6), vendor decisions (Module 7), stakeholder
communication (Module 8), and risk assessment (Module 9) decisions to happen
*before* the team starts building, when they're cheap to change, rather than
being discovered mid-project when they're expensive to change. A one-page
charter that takes half a day to write can save weeks of rework later.

## The charter template

Work through each section in order — later sections build on earlier ones.

### 1. Problem statement & success metric

| Field | Your entry |
|---|---|
| Business problem (one sentence, no jargon) | |
| AI/ML category (classical ML / deep learning / LLM-GenAI — Module 2) | |
| Primary success metric | |
| Minimum acceptable threshold | |
| Baseline (what a simple non-AI approach would achieve) | |

### 2. Roles & ownership

| Role (Module 1 & 4) | Name | Accountable for |
|---|---|---|
| Executive sponsor | | Final go/no-go, budget |
| AI/Project manager | | Day-to-day delivery, this charter |
| Data science / ML lead | | Model quality and approach |
| Domain SME | | Business-context validation |
| Incident owner (Module 9) | | Response if the model causes harm post-launch |

### 3. Lifecycle plan & checkpoints (Module 3 & 6)

| Stage | Target date | Gate criteria to proceed |
|---|---|---|
| Feasibility checkpoint | | |
| Development checkpoint | | |
| Launch readiness checkpoint | | |

State the range you'll communicate to stakeholders at kickoff, per Module
6's range-and-checkpoint framework, rather than a single fixed date.

### 4. Build vs. buy decision (Module 7)

| Question | Answer |
|---|---|
| Is this capability core to our differentiation? | |
| Does a vendor already meet our bar, verified on our own data? | |
| Recommendation | Build / Buy / Hybrid |

### 5. Ethics & responsible-AI review (Module 5)

| Checklist item | Status (Pass / Fail / Unknown) | Notes |
|---|---|---|
| Subgroup performance reviewed | | |
| Use-case appropriateness reviewed | | |
| Human-in-the-loop defined | | |
| Data consent documented | | |
| Escalation path defined | | |
| Explainability plan | | |

### 6. Risk assessment (Module 9)

| Risk category | Applies? | Impact (Low/Med/High) | Reversibility (Low/Med/High) | Mitigation |
|---|---|---|---|---|
| Bias / unfair outcomes | | | | |
| Hallucination | | | | |
| Security / adversarial | | | | |
| Privacy leakage | | | | |
| Overreliance | | | | |
| Model drift | | | | |

### 7. Stakeholder communication plan (Module 8)

| Audience | Cadence | Format |
|---|---|---|
| Executive sponsor | | |
| Cross-functional partners | | |
| End users (if applicable) | | |

## Worked example (filled charter, abbreviated)

A worked excerpt for "AI-assisted first-response drafting for a customer
support team":

- **Problem statement**: Reduce average first-response time on support
  tickets by drafting suggested replies for agents to review and send.
  **Category**: LLM/GenAI. **Metric**: agent-reported "usable without major
  edit" rate. **Threshold**: 70%. **Baseline**: 0% (no drafting assist
  today).
- **Roles**: Sponsor = VP Support; AI PM = charter author; ML lead = senior
  ML engineer; SME = 2 veteran support agents; Incident owner = AI PM.
- **Lifecycle**: Feasibility (3 weeks, gate: 60%+ usable-without-edit on a
  100-ticket sample) → Development (5 weeks, gate: 70%+ on held-out tickets)
  → Launch readiness (gate: human-review-before-send confirmed working,
  escalation path tested).
- **Build vs. buy**: Not core differentiation → lean Buy; foundation-model
  API selected over a full third-party platform after vendor evaluation
  showed the platform's out-of-box accuracy on this company's ticket style
  was below bar (see Module 7's worked example for this exact scenario).
- **Ethics review**: Human-in-the-loop = pass (agent always reviews before
  send); explainability = pass (draft always shown alongside, never
  auto-sent); subgroup performance = unknown, flagged for feasibility stage.
- **Risk assessment**: Hallucination = applies, impact medium (agent catches
  most errors before sending), mitigation = agent review is mandatory, never
  optional, plus logging of edit-rate as an ongoing quality signal.
  Overreliance = applies, impact medium, mitigation = periodic manual audit
  of a sample of sent replies to confirm agents are still reading drafts
  critically, not rubber-stamping.
- **Communication plan**: VP Support gets a bi-weekly status using the
  Module 8 template; support agents get a short async update after each
  checkpoint.

## How It Actually Works

A charter functions as a coordination mechanism specifically because it
forces every ambiguity that would otherwise surface piecemeal — one
stakeholder disagreement per week, spread across the whole project — to
surface all at once, before any work has been sunk into a particular
direction. Each of the seven sections corresponds to a decision that, left
unwritten, defaults silently to whoever speaks last in whatever meeting the
topic happens to come up in: without a written success metric, "is this
good enough" gets decided by whoever's most persuasive near the deadline;
without written roles, an incident gets responded to by whoever notices it
first, not whoever's actually accountable. Writing the charter doesn't
create new information the team didn't have — it relocates decisions that
would otherwise be made implicitly and inconsistently to a single moment
where they're made explicitly and are then referenceable by everyone,
including people who join the project later and would otherwise have to
reconstruct these decisions from institutional memory.

The reason "Unknown — need to ask [specific person]" is more valuable than
a vague or invented answer is a direct consequence of what a charter is
*for*: it's meant to be the single artifact anyone — a new team member, an
auditor, a future version of you six months in — can read to understand the
project's real state. A blank field looks like an oversight; a plausible-
sounding but made-up answer looks like settled fact and will be trusted as
one, which is far more dangerous than an acknowledged gap, because it
removes the very signal (visible uncertainty) that would prompt someone to
go verify it before relying on it.

## Exercise (the deliverable)

Choose a real AI project from your own organization, or a plausible one if
you don't currently have access to one. Fill out all seven sections of the
charter template above completely — every field, not just the easy ones.
Where you genuinely don't know an answer, write "Unknown — need to ask
[specific person]" rather than leaving it blank; a charter that honestly
surfaces open questions is more valuable than one that fakes completeness.
This filled-out charter is your Level 1 capstone deliverable — keep it, since
Level 2's capstone (an MLOps process design) builds directly on the same
project.
