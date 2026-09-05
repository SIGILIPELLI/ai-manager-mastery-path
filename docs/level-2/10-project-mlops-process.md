# 10 · Project — Design an MLOps Process for a Team

Every module in this level described one part of running AI systems in
production. This capstone makes you write the part nobody writes: the
**process document** that says how your specific team takes an idea from
experiment to production, keeps it healthy, and proves it was done
properly.

Most teams do not have this. They have tools, habits, and a shared
understanding that evaporates the moment someone leaves or the team
doubles. The symptom is familiar — every release is negotiated from
first principles, every incident is investigated by whoever happens to
remember, and every audit request becomes archaeology.

Writing it down is a manager's job, not an engineer's, for three
reasons. The document is mostly about **decision rights and thresholds**
— who may approve what, and at what number — which are management
decisions. It has to be **proportionate to risk**, and only you see the
whole portfolio. And it will be **defended in a budget conversation**,
which is your meeting, not theirs.

The deliverable is four pages covering four things: how experiments are
tracked, what gates a model passes before serving traffic, what is
monitored and who responds, and what evidence is retained. This module
gives you a template for each, then a worked example of the whole thing
on a realistic team.

## The shape of the deliverable

Resist the urge to write a policy. What is being asked for is a
short, specific operating document, and specificity is the entire value.

| Section | The question it settles | Length | Fails when |
|---|---|---|---|
| **0. Scope & tiers** | Which systems does this apply to, at what intensity? | ½ page | One process is applied to everything equally |
| **1. Experimentation** | What gets recorded, and what counts as a result? | ½ page | Recording is aspirational, not enforced |
| **2. Deployment gates** | What must be true before traffic moves? | 1 page | Gates exist but have no named approver |
| **3. Monitoring & response** | What is watched, by whom, and what happens on alert? | 1 page | Alerts route to a channel, not a person |
| **4. Governance & evidence** | What is retained, and who can produce it? | ½ page | Evidence is assembled on request rather than as a by-product |

Two rules make the difference between a document that is used and one
that is quoted ironically. **Every threshold is a number**, not an
adjective — "acceptable quality" is unenforceable, "recall ≥ 0.82 on the
held-out set" is a gate. And **every gate has a named role that can say
no**, because a gate nobody can fail is documentation, not control.

## Section 0 — Scope and tiers

Start by listing your production and near-production systems and
assigning each a tier, using Module 07's tiering and Module 03's
damage-per-week test. This is the single highest-leverage half page,
because it is what stops the process from being either too heavy for
internal tools or too light for consequential ones.

| System | Tier (Module 07) | Damage if bad for one week | Target maturity (Module 03) |
|---|---|---|---|
| | T1–T4 | | 0–4 |

The tier drives everything downstream: how many gates apply, how fast
detection has to be, who signs off, and what is retained. State plainly
that T1 systems get the light path — otherwise the process collapses
under its own weight within a quarter.

## Section 1 — Experimentation tracking

From Module 01: an experiment is a question with a pre-agreed decision
rule, not a period of work. The process document specifies what must be
recorded for a result to count as a result.

| Field | Recorded by | Why it matters later |
|---|---|---|
| Question and decision rule | ML lead, **before** starting | Prevents post-hoc reinterpretation |
| Dataset version / snapshot ID | Automatic | Without it nothing is reproducible |
| Code commit and environment | Automatic | The other half of reproducibility |
| Metric values on the fixed eval set | Automatic | Comparability across weeks |
| Outcome: promote / iterate / stop | ML lead, at review | Turns activity into decisions |
| Owner and date | Automatic | Who to ask in eleven months |

The manager-relevant rules attached to this table are short. Results
compared against **one frozen evaluation set** owned by the team, not
by an individual. A **negative result is recorded, not deleted** — the
cost of rediscovering a dead end twice is the most common invisible tax
on ML teams. And **promotion to a release candidate requires a recorded
run**, which is the one place enforcement actually needs to bite.

## Section 2 — Deployment gates

This is the heart of the document. A gate is a named check, with a
number, and a role who can refuse. Four gates cover almost every case;
which ones apply depends on the tier from section 0.

| Gate | Check | Threshold (example) | Approver | Applies to |
|---|---|---|---|---|
| **G1 — Candidate** | Beats current production model on the frozen eval set; no subgroup regression beyond tolerance | ≥ +2% primary metric; no subgroup down >1% | ML lead | All tiers |
| **G2 — Pre-deploy** | Reproducible build; rollback path tested; model card complete | Rollback exercised in the last 90 days | Platform lead | T2+ |
| **G3 — Shadow** | Runs on live traffic without serving; outputs compared to production | ≥ 7 days, disagreement rate explained | ML lead + product | T3+ |
| **G4 — Canary** | Small traffic share, watched against control | 10% for 5 days, product metric not worse | Product owner | T2+ |
| **G5 — Full rollout** | Business sign-off; monitoring live before traffic moves | Dashboard green, on-call named | AI manager (you) | T3+ |

Three design notes worth arguing for when the team pushes back. Gates
should be **passable in hours, not days**, or they get routed around;
if G1 takes a week, the problem is your eval infrastructure, not the
team's discipline. Every gate needs a documented **waiver path** with a
named waiver approver, because the alternative to a legitimate waiver is
a quiet bypass. And **the rollback rehearsal date is a gate condition**,
not a nice-to-have — an untested rollback is a belief.

## Section 3 — Monitoring and response

Module 03 gave the six panels. The capstone adds the half that teams
skip: what happens when a panel goes red.

| Signal | Threshold | Who is paged | First action | Escalates to you when |
|---|---|---|---|---|
| Input validation failures | >2% for 2 hours | Data engineering on-call | Check upstream schema | Unresolved at 8 hours |
| Output distribution shift | Class share moves >5pp week on week | ML on-call | Compare to input drift | Confirmed drift |
| Primary quality metric | Below release value − tolerance | ML lead | Assess rollback | Immediately, on T3+ |
| Product metric divergence | Product metric falls while model metric holds | Product owner | Check the evaluation set's validity | Within one review cycle |
| Inference cost per unit | >30% above plan | Platform lead | Identify the design change | At month end |

Two things to insist on. **Every row names a person or rota, never a
channel** — an alert delivered to a channel is an alert delivered to
nobody. And **the escalation column is the one you own**; it defines the
threshold at which a technical event becomes a management decision,
which is exactly the boundary that is ambiguous during a real incident.

Add a stated **detection-window target per tier** — T3 within 48 hours,
T1 within a month. That number is what your investment case is
denominated in.

## Section 4 — Governance and evidence

The test is not whether you have a policy. It is whether you can answer,
in under an hour and without a heroic effort: *which model made this
decision, on what data, approved by whom, and what has changed since?*

| Artefact | Produced when | Retained | Produced by |
|---|---|---|---|
| Model card (purpose, data, metrics, limits, subgroup results) | At G2 | Life of the system + 2 years | ML lead |
| Approval record for each gate | At each gate | Same | Automatic from the pipeline |
| Prediction log with model version | Continuously | Per retention policy (Module 04) | Automatic |
| Monitoring history and incident notes | Continuously | 2 years | Platform |
| Annual system review | Yearly | Life of the system | You |

The design principle: **evidence should be a by-product of the process,
not a task added to it.** If producing an audit trail requires anyone to
remember to do something, it will be complete for four months and then
quietly stop.

## Worked example

A mid-size insurer's AI team: **9 people** — 4 ML/data scientists, 2
data engineers, 1 platform engineer, 1 product manager, and an AI
manager. Two systems in production and five experiments running at any
time.

**Section 0 as they wrote it:**

| System | Tier | Damage if bad for one week | Target maturity |
|---|---|---|---|
| Claims triage scoring | T3 | Mis-routed claims, cycle-time penalties, regulator interest | 3 |
| Internal policy-document assistant | T1 | Mild annoyance; users notice immediately | 1 |

That split was the most contested decision and the most valuable. The
team had been applying an informal version of the same review to both,
which meant the assistant felt over-governed while triage was
under-governed — a common and precisely backwards arrangement.

**What the process had to fix.** Claims triage routed about **14,000
claims a month**. A degradation that lifted the mis-triage rate by five
percentage points put **700 claims a month** down the wrong path, at an
estimated **$210 each** in rework and cycle-time penalty — **$147,000 a
month**, or roughly **$33,900 a week**. The previous March, exactly that
had happened after an upstream change to how claim descriptions were
captured, and it ran for **six weeks** before a claims supervisor
escalated: about **$203,500**. With a 48-hour detection target the same
event costs about **$9,700**. The gap — **$194,000 per occurrence** — is
the entire business case, and it was already a fact rather than a
projection.

Separately, the team estimated **six person-weeks a quarter** lost to
re-running work whose results could not be reproduced or located: 24
person-weeks a year, about **$88,000** at their loaded cost.

**The investment they proposed:**

| Item | One-off | Annual |
|---|---|---|
| Experiment tracking + model registry, adopted for real | $38,000 | — |
| Automated eval gate (G1) wired into the pipeline | $52,000 | — |
| Monitoring panels, thresholds and on-call rota (both systems) | $61,000 | — |
| Model cards, gate approval log, retention wiring | $34,000 | — |
| Platform licences and infrastructure | — | $28,000 |
| 0.6 FTE ongoing on-call and maintenance | — | $114,000 |
| **Total** | **$185,000** | **$142,000** |

First-year cost: **$327,000**. Against it, one avoided March-scale
incident is **$194,000** and recovered rework is **$88,000** —
**$282,000** a year of recurring benefit against a **$142,000** annual
run cost, so the process pays for its own running from year one and
returns the build cost on the first prevented incident.

**The three decisions that made it work in practice.** The T1 assistant
was explicitly exempted from G3 and G5, which bought the team's
agreement to enforce all five gates on triage. G1 was rebuilt to run in
**under 20 minutes**, because the first draft took most of a day and was
already being skipped within two weeks. And the waiver path was written
down with the AI manager as sole waiver approver — three waivers were
granted in the first year, each with a recorded reason, which is roughly
the right number. Zero would have meant the gates were too loose to ever
bind; a dozen would have meant they were theatre.

**What did not work.** The first version routed all alerts to a shared
channel. During the first drift event, everybody saw the alert and
nobody owned it, costing eleven hours. The rota in the section 3 table
exists because of that, not because of good design.

The transferable lesson: an MLOps process is funded and adopted when it
is expressed as **a detection window and a set of named approvers**, and
ignored when it is expressed as a maturity ambition.

## How It Actually Works

The "everybody saw the alert and nobody owned it" failure is a textbook
instance of diffusion of responsibility interacting with an unowned
notification channel, and it's worth understanding mechanically because it
recurs in every monitoring system that routes alerts to a group rather than
a person: when an alert lands somewhere many people can see, each
individual's rational inference is that someone else — someone with more
context, or who saw it first — is already handling it, and that inference
is available to every recipient simultaneously, so it produces a stable
equilibrium where everyone waits and nobody acts. This isn't a training or
attitude problem; it's a structural property of shared-visibility channels
with no designated owner, which is exactly why the fix was a rota (a
rotating single named owner) rather than "remind the team to be more
proactive" — the rota removes the ambiguity that made the diffusion
possible in the first place, by making it unambiguous whose job it is to
act on any given alert regardless of who else can see it.

The three-waivers-being-the-right-number observation reflects a genuine
calibration signal about gate design: a gate that is never waived is
indistinguishable, from the outside, between "the gate is perfectly
calibrated to real risk" and "the gate is so loosely enforced or so easy to
satisfy that it never actually binds on anything" — zero waivers carries no
information about which. A gate waived constantly signals the opposite
failure: the threshold is set somewhere unrealistic relative to how the
team actually needs to operate, so the gate is being routed around rather
than respected. A small, non-zero, individually-justified waiver count is
the only pattern consistent with a gate that's genuinely binding on real
edge cases some of the time — which is why tracking the waiver count and
its reasons is itself a monitoring signal on the governance process, not
just an administrative log.

## Exercise

Produce the four-page process document for a team you run, work
alongside, or could plausibly describe — ideally the same project you
charted in Level 1's capstone.

1. **Write section 0 first.** List every production and
   near-production system, tier each one, and state a target maturity
   level. If everything lands in the same tier, you have not tiered.
2. **Fill the experiment table** and decide the one enforcement point:
   what may not happen without a recorded run.
3. **Define your gates.** For each of G1–G5, write the check, the
   number, the approver by role, and which tiers it applies to. Delete
   any gate you cannot name an approver for.
4. **Complete the monitoring table**, replacing every channel with a
   person or rota, and set a detection-window target per tier.
5. **Test the evidence section** against the audit question: pick a real
   decision your system made last month and try to answer it end to end.
   Time yourself; the gap you find is the section 4 backlog.
6. **Price it** using Module 09's structure — one-off and annual,
   separately — and state the benefit as a detection-window reduction
   against a quantified failure you have already experienced.

## Stretch goals

- **Run it as a tabletop.** Walk your team through a fictional Tuesday
  where the quality panel goes red at 09:00, using only the document.
  Every question it cannot answer is a defect; fix those before
  publishing.
- **Rehearse the rollback for real** on the highest-tier system, and
  record the date in the G2 gate condition. Most teams discover
  something in the first attempt.
- **Reconcile it with Module 07's checklist and Module 04's access
  tiers**, so a T3 system's governance obligations appear once, in one
  place, rather than in three documents that will drift apart.
- **Write the one-paragraph version** you would send to your sponsor —
  scope, detection targets, cost, and what gets worse if it is not
  funded. If you cannot compress it to a paragraph, the underlying
  thinking is not finished.
