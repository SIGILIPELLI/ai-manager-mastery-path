# 09 · Building AI Centers of Excellence

An AI Center of Excellence (CoE) is one of the most commonly mis-built
structures in AI organizations — often stood up reactively after a
governance failure or a board question, staffed with senior people pulled
from delivery work, and given a mandate so broad ("own AI standards") that
it either does nothing or becomes a bottleneck every pod resents. Done
well, a CoE is a small, high-leverage function with a narrow, explicit
mandate. This module covers how to scope one correctly and avoid the two
failure modes that kill most of them within a year.

## 1. What a CoE is (and isn't)

| It is | It isn't |
|---|---|
| A standards-and-enablement function that makes pods faster and more consistent | A second engineering team that builds AI features itself |
| A place where cross-cutting expertise (governance, evaluation, ethics review) lives once instead of per-pod | A gatekeeper that approves or blocks every pod's technical decision |
| Advisory + tooling, with narrow direct authority (e.g., final sign-off on high-risk system launches) | A catch-all for "AI stuff that doesn't fit elsewhere" |
| Measured by pod adoption and outcomes it improved | Measured by its own headcount growth or activity volume |

The clearest early warning sign of a CoE heading toward the "isn't" column:
pod leads start describing it as "the team we have to go through" rather
than "the team that helps us."

## 2. The CoE mandate — define it explicitly in writing

Ambiguity here is the single biggest cause of CoE dysfunction. Before
staffing anything, get written, VP-level sign-off on:

| Question | Example answer |
|---|---|
| What decisions does the CoE make unilaterally? | Final approval on governance sign-off for high-risk systems (per Module 2's risk tiers) |
| What decisions does it advise on but not control? | Model architecture choices, prompt design, pod-level tooling |
| What does it build/maintain directly? | Shared eval framework, model registry, governance checklist tooling |
| What is explicitly out of scope? | Feature delivery timelines, pod headcount decisions, product roadmap |
| How does a pod escalate a disagreement with the CoE? | Named escalation path to the CoE's own manager, with an SLA on response |

Publish this mandate somewhere every pod lead can see it. The most common
failure is not that the mandate was wrong — it's that it was never written
down, so every pod inferred a different (usually broader, more
resented) version of it.

## 3. Staffing and sizing

| CoE size | When it's appropriate | Composition |
|---|---|---|
| 1-2 people | Early stage, <30 AI ICs org-wide | A senior IC + a governance/compliance liaison, part-time |
| 3-6 people | Mid stage, 30-100 AI ICs, multiple pods with real duplication (Module 5) | Adds a dedicated platform engineer, an eval specialist |
| 7+ people | Large org, 100+ AI ICs, high regulatory exposure | Adds dedicated legal/compliance embed, dedicated training/enablement role |

A CoE larger than roughly 5% of the total AI headcount it serves is a
warning sign worth investigating — it usually means the CoE has started
absorbing work that should stay in the pods, or has become a status
symbol rather than a lean function.

## 4. The four functions a CoE typically owns

| Function | What it delivers | How to know it's working |
|---|---|---|
| Standards | Shared definitions (what "production-ready" means, eval report format) | Pods use the standard without being told to, each release cycle |
| Enablement | Training, onboarding materials, internal documentation, office hours | New hires ramp faster; pods stop reinventing basics |
| Governance sign-off | Final review gate for high-risk systems (Module 2) | Reviews happen on a predictable cadence, not as ad hoc fire drills |
| Shared tooling | Registry, eval framework, monitoring templates (Module 5) | Adoption rate tracked and rising, not just tools that exist |

Resist adding a fifth function ("innovation," "R&D," "AI strategy") unless
there's a specific, evidenced gap — mandate creep is how a lean CoE becomes
a bloated one within two budget cycles.

## Worked example

A regional bank, Castleton Trust, stood up an "AI Center of Excellence"
after an internal audit flagged inconsistent model documentation across
its five AI-adjacent teams (fraud, underwriting, marketing personalization,
a chatbot, and an internal analytics tool). The CoE was staffed with six
people pulled from delivery teams and given the mandate "own AI
excellence across the bank" — a phrase that appeared verbatim in the
announcement email and nowhere else more specifically.

Within four months, three pod leads had independently escalated
frustration: the CoE was requiring sign-off on decisions (like which
open-source library to use for a low-risk internal tool) that had no
governance implication, while genuinely high-risk items (the underwriting
model's quarterly bias audit) had slipped because nobody had explicitly
made that the CoE's job in writing.

The fix, driven by a new head of AI: rewrote the mandate using the template
in section 2. The CoE's unilateral authority was narrowed to governance
sign-off specifically for systems tiered medium-or-higher risk (per the
Module 2 inventory) — nothing else required its approval. Its advisory
role was made explicit and clearly optional for pods to accept or decline.
Headcount was cut from six to four, with the two reassigned engineers
returning to pod work where the audit had actually found no real gap. Pod
lead satisfaction, measured in the bank's internal quarterly survey, moved
from the CoE being the second-most-cited frustration organization-wide to
not appearing in the top ten the following quarter — while the specific
audit finding that started the whole effort (inconsistent model
documentation) was fully resolved, because the sign-off gate was now
actually enforced where it mattered instead of everywhere.

## How It Actually Works

Castleton's CoE simultaneously over-controlling trivial decisions and
missing the genuinely important one is not a coincidence — both failures
trace to the same root cause: an unwritten mandate defaults to whatever
scope feels natural to the people staffing it, and "own AI excellence" gives
no boundary at all, so the CoE expanded into whatever caught its attention
(a library choice, because someone happened to review it) while quietly
never being assigned the one thing that actually mattered (the
underwriting bias audit), because nobody had explicitly made that anyone's
job at all. An unbounded mandate isn't neutral — it's equivalent to letting
scope be decided ad hoc, case by case, which produces exactly the pattern
observed: attention flows to whatever is easiest or most visible to review,
not to whatever carries the most risk, because risk-weighting requires the
explicit tiering the Module 2 inventory provides, and nothing forced the
CoE to consult it.

The pod-lead-satisfaction outcome is also mechanically explicable, not just
a morale story: a review gate that fires on low-risk decisions imposes a
real cost (delay, friction, a sense of being second-guessed) on every pod,
every time, with zero corresponding risk-reduction benefit, since the
decision it's blocking carries no real governance exposure in the first
place — that's a pure deadweight cost, felt directly by every pod on every
cycle. Narrowing the gate to fire only on medium-plus risk systems removes
that cost from the overwhelming majority of pod interactions while
concentrating the CoE's actual leverage exactly where it has real value —
which is why satisfaction improved and the original audit finding got
fully resolved in the same move: the fix wasn't "do more governance," it
was "stop spending the CoE's authority on decisions where it produces no
risk reduction, so there's attention and credibility left for the one that
does."

## Exercise

Take your own organization's CoE (existing, planned, or the Castleton Trust
example above at month 0).

1. **Draft the mandate** using the five-question template in section 2.
   Be as specific as the bank's revised version — "sign-off on medium-plus
   risk governance," not "own AI excellence."
2. **Size it** using the table in section 3 against your actual AI
   headcount, and flag if your current or planned size exceeds the ~5%
   guideline — if so, name what would justify the excess.
3. **Pick one of the four functions in section 4** and define the single
   metric that would tell you within two quarters whether it's working or
   just active.
