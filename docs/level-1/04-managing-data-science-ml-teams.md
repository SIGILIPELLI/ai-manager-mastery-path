# 04 · Managing Data Science & ML Teams

Data scientists and ML engineers are often managed by people coming from a
general software engineering or product background who unconsciously apply
standard engineering-management habits — sprint velocity, story points,
"done means shipped" — to a discipline where those habits actively backfire.
This module covers the specific adjustments to team structure, planning
rhythm, and performance evaluation that make AI/ML teams effective, plus how
to structure the roles so nothing falls through the cracks.

## 1. The roles on a typical AI/ML team

| Role | What they own | Common misconception to avoid |
|---|---|---|
| **Data scientist** | Exploring data, building and evaluating candidate models, statistical rigor | Not the same as a data analyst — the job is building predictive systems, not just reporting on past data |
| **ML engineer** | Turning a validated model into reliable, scalable production code | Distinct skill set from data science — strong data scientists are not automatically strong production engineers |
| **MLOps / platform engineer** | Infrastructure for training, deployment, monitoring, and versioning of models | Often the most understaffed role relative to its importance — see Level 2 for the dedicated module |
| **Data engineer** | Building and maintaining the pipelines that feed clean data to everyone else | The unsung foundation — a weak data engineering function silently caps everyone else's output |
| **Domain / subject-matter expert (SME)** | Providing the business context that keeps the model solving the right problem | Frequently left out of the loop after the kickoff meeting — a costly mistake |

A team of "just data scientists" without ML engineering and data engineering
support is a common early-stage mistake: the data scientists end up doing
production engineering and pipeline maintenance badly and reluctantly,
because nobody else is doing it, while their actual specialty — modeling —
stalls.

## 2. Planning rhythm: sprints don't work the same way

Standard two-week sprints built around fixed, well-scoped tickets fight
against how ML work actually happens — an experiment's outcome (and thus
the next step) often isn't known until the experiment is run. A better
rhythm:

| Element | Standard engineering sprint | Adapted ML team rhythm |
|---|---|---|
| Planning unit | A ticket with a clear "done" state | A hypothesis to test ("does adding feature X improve recall?") with a time-box, not a guaranteed outcome |
| Commitment | "We will ship these 8 tickets" | "We will have run these 3 experiments and know their results" |
| Standup content | Blockers on known tasks | Blockers *and* early experiment results that might change the plan |
| Retro focus | Process improvements | Process improvements *and* which hypotheses turned out to be dead ends, and why |

Keep sprint-style time-boxing for the surrounding work (data pipeline
tickets, infrastructure, integration code) where it fits naturally — the
adaptation is specifically for the exploratory modeling work itself.

## 3. Evaluating performance and progress fairly

A data scientist whose three best-designed experiments all disprove a
hypothesis has often done excellent work — the alternative was building on
a false assumption. Standard "velocity" or "tickets closed" metrics
misjudge this kind of contribution badly.

| Don't measure | Measure instead |
|---|---|
| Number of models trained | Quality of experimental design (were the tests set up to give a real answer?) |
| Whether every experiment "succeeded" | Whether negative results were documented and shared, preventing repeated dead ends |
| Lines of code | Whether findings were communicated clearly enough for the team (and you) to act on them |
| Time to first prototype | Time to a *trustworthy* evaluation of that prototype |

## 4. A lightweight team operating structure

A structure that scales from a 3-person team to a multi-team org:

| Layer | Cadence | Purpose |
|---|---|---|
| Daily standup | 15 min | Surface blockers and any experiment results that change near-term plans |
| Weekly model/results review | 30–45 min | The team presents current experiment results to each other, with the manager as a sanity-checking participant, not just an audience |
| Bi-weekly stakeholder sync | 30 min | Translate current status into business terms for the sponsor (see Module 8) |
| Monthly retrospective | 45–60 min | Review what worked in the *process* (planning rhythm, evaluation criteria), separate from model results themselves |

## Worked example

A newly-hired AI engineering manager at a healthcare startup inherited a team
of four data scientists being run on standard two-week sprints with story
points. Six months in, morale was low and stakeholders were frustrated by
"missed sprint commitments." The manager found the actual problem: the team
was being asked to commit to specific *model accuracy improvements* as if
they were tickets, when experiment outcomes weren't knowable in advance.
Switching to hypothesis-based planning (committing to *running* three
specific experiments per sprint, not to a guaranteed accuracy gain) fixed
the stakeholder-expectation mismatch within one sprint cycle — the team
hit their (now honest) commitments consistently, and stakeholders got
clearer, more truthful updates on real progress instead of sandbagged
estimates.

## How It Actually Works

Sprint commitments fail specifically for modeling work because of what a
"ticket" implicitly assumes: that the path from start to done is mostly
known, and remaining uncertainty is about execution speed, not about
whether the destination exists at all. An experiment's outcome is
determined by properties of the data and the problem that are not visible
until the experiment actually runs — there is no amount of up-front analysis
that substitutes for training the model and checking recall on held-out
data, because the relationship between a feature and the target is a
statistical fact about the world, not a design decision a team can simply
choose to satisfy by working harder. Committing to "improve recall by 5
points" is therefore a commitment to a fact about reality that hasn't been
observed yet — which is why it reliably produces either sandbagging (padding
estimates to guarantee the number lands) or missed commitments, and neither
outcome reflects the team's actual productivity. Committing to "run these
three specific, well-designed experiments" is achievable because running an
experiment competently *is* within the team's control, even when its result
isn't.

This is also the mechanical reason a negative result counts as real
progress rather than a wasted sprint: each disproved hypothesis removes one
branch from the space of things that could explain the target variable,
which narrows where the *next* experiment should look. A team with no
negative results after months of work has either gotten extraordinarily
lucky on its very first guesses, or — far more commonly — isn't running
experiments rigorous enough to actually falsify anything, which is a
warning sign, not a good one. Evaluating "quality of experimental design"
over "number of models trained" follows directly: a sloppy experiment (a
leaky train/test split, an unrepresentative sample, a metric that doesn't
match the real objective) can produce a positive-looking result that tells
you nothing true, while a rigorous experiment that disproves the hypothesis
has still generated real information — the first is a false positive
disguised as output, the second is the process working as intended.

## Exercise

Map your current (or a plausible) AI/ML team against the five roles in
section 1. Identify any role that's missing or being informally absorbed by
someone else (e.g., a data scientist doing ML-engineering work by default).
Then rewrite one upcoming sprint's plan using the hypothesis-based format
from section 2 — list 3 hypotheses to test, each with its time-box and the
specific evidence that would count as a clear result, instead of a list of
guaranteed deliverables.
