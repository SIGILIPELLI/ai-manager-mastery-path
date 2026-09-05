# 01 · Scaling AI Teams

The management problems of a five-person ML team and a fifty-person AI
organization are not the same problems at a larger size — they are
*different* problems. A single team can run on shared context: everyone
knows the model, the data, and each other's judgment. Past roughly eight to
ten people, that shared context breaks down silently, and the symptoms show
up as things that look unrelated — duplicated feature work, incompatible
eval sets, a platform team nobody asked for building things nobody uses.
This module gives you the structural decisions to make deliberately, before
growth forces them on you badly.

## 1. The three scaling thresholds

AI orgs tend to hit the same three inflection points regardless of industry.
Each one requires a structural change, not just "hire more people onto the
same team."

| Threshold | Symptom that tells you you're there | Structural fix |
|---|---|---|
| ~8-10 ICs, one team | Standup runs long; people learn about each other's work in standup, not before | Split into 2 pods by problem area, keep one manager |
| ~25-30 ICs, multiple pods | Pods duplicate infrastructure (two feature stores, two eval harnesses) | Stand up a platform/enablement function |
| ~60+ ICs, platform exists | Platform team becomes a bottleneck; pods route around it with shadow tooling | Platform shifts from "build for pods" to "build with pods"; embed platform liaisons |

Treat these as ranges, not hard numbers — a org with unusually high task
similarity across pods can push the first threshold later; one with highly
divergent problem domains (e.g., fraud modeling and content recommendations
under one umbrella) can hit it earlier.

## 2. Pod design patterns

When you split a single team, the axis you split on determines what
breaks later. There is no universally correct axis — only trade-offs.

| Split axis | What it optimizes for | What it costs |
|---|---|---|
| By product surface (search, recs, support) | Fast iteration, clear ownership, easy stakeholder mapping | Duplicated infra; inconsistent modeling practices across pods |
| By ML lifecycle stage (research, applied, MLOps) | Deep technical specialization, reusable platform | Slow handoffs between stages; research work loses product context |
| By customer segment (SMB, enterprise) | Tight alignment with go-to-market | Small pods per segment may lack enough problem variety to retain senior talent |

Most orgs that scale successfully start split by product surface (it maps
cleanly to who's asking for the work) and layer in a lifecycle-stage
platform team only once duplication becomes measurably expensive — not
preemptively, since a platform team built before there's real duplication
to eliminate tends to build the wrong abstractions.

## 3. The manager-to-IC ratio, and when to add a layer

A single AI manager can effectively run 6-8 ICs when the work is
similar and the manager still has technical context. Add a second layer
(pod leads reporting to a manager of managers) when either of two things is
true: the manager can no longer review technical decisions personally, or
the manager's calendar is more than 50% cross-team coordination rather than
team leadership.

| Org size | Recommended structure | Common mistake at this size |
|---|---|---|
| 1-8 ICs | 1 manager, flat | Hiring a "senior IC lead" as a shadow manager instead of naming the role |
| 9-25 ICs | 2-3 pods, 1 pod lead each, 1 manager over pod leads | Manager keeps doing hands-on technical review, becomes the bottleneck |
| 26-60 ICs | Pods + platform team, manager of managers | Platform team formed reactively, with no clear internal customer commitment |
| 60+ ICs | Multiple manager-of-manager layers, dedicated AI program management | No single owner of cross-pod technical standards (eval practices, model registry, incident process) |

## 4. What must stay centralized even after you split

Splitting into pods is necessary but creates a specific failure mode: each
pod re-derives its own answer to questions that should have one
organization-wide answer. Decide these centrally and document them,
regardless of how many pods exist.

- **Evaluation standards.** What "production-ready" means (minimum eval
  coverage, required bias/safety checks) should not vary by pod, or you
  cannot compare risk across the portfolio.
- **Incident process.** One severity taxonomy, one escalation path — not one
  per pod (see Module 6).
- **Model/experiment registry.** A pod that can't see what another pod
  already tried will re-run failed experiments (see Level 2, Module 1).
- **Vendor and tooling contracts.** Two pods independently licensing
  overlapping LLM API tools is a recurring, avoidable cost leak.

## Worked example

Meridian Health, a healthcare-analytics company, grew its AI org from 9 to
34 people over 14 months as it added three new product lines (readmission
risk, staffing forecasting, and a clinician-facing LLM assistant). The VP of
AI kept a single flat team through month 10, run by one manager who had
built the original readmission model personally.

By month 10 the symptoms were unmistakable: the LLM assistant pod had built
its own retrieval eval harness because nobody knew the readmission team's
harness existed; two people were independently negotiating with the same
vendor for overlapping contract terms; and the manager was spending most
Fridays in status-sync meetings rather than technical review.

The restructure, executed over one quarter:

1. Split into three pods by product line (readmission, staffing, clinician
   assistant), each with a promoted pod lead — all three were the most
   senior IC already doing informal technical leadership in that area.
2. Created a two-person platform pair (not a full team yet) owning the
   model registry, one shared eval framework, and the incident severity
   taxonomy — deliberately small, to avoid over-building before demand was
   proven.
3. The VP moved to managing the three pod leads plus the platform pair,
   stepping back from personal code review.

Within two quarters, the vendor-contract duplication was caught and
consolidated (saving roughly $180K/year in overlapping API commitments),
and a near-miss incident on the clinician assistant was caught by the new
shared severity process before reaching a P1 — the pod lead recognized the
symptom pattern from the readmission team's documented incident, something
that would not have been visible before the registry existed.

## How It Actually Works

The reason shared context breaks down specifically around eight to ten
people is a direct combinatorial fact, not a soft cultural observation: the
number of pairwise relationships in a group grows as n(n-1)/2, so a team of
8 has 28 pairs of people who might need to informally sync, while a team of
15 has 105 — a team roughly twice the size has nearly four times the
coordination surface. Below the threshold, one person (the manager, or
whoever's most central) can plausibly hold enough of those pairwise
relationships in their own head to substitute for explicit process; above
it, the number of connections outstrips what any single person can track,
and coordination failures (duplicated infrastructure, incompatible eval
sets) are the direct symptom of information that used to travel through
informal channels no longer reaching everyone who needs it. This is exactly
why the fix at each threshold in section 1 is structural — splitting pods,
adding a platform layer — rather than "communicate more": no volume of
extra communication scales linearly to cover a coordination surface that's
growing quadratically.

The centralization list in section 4 follows a specific logic: each item on
it is a *shared reference point* whose value comes precisely from being
singular — an eval standard, an incident taxonomy, a model registry only
functions as a comparison tool if every pod uses the same one, because the
entire point is to let one pod's result be meaningfully compared against
another's. The moment two pods maintain separate versions, the artifact
stops answering cross-pod questions at all — a registry a pod can't see
into isn't a smaller version of the shared registry, it's a different kind
of object that happens to look similar, because "has anyone tried this
before" is a question only answerable against a genuinely shared record.
This is why platform teams that centralize these specific things pay for
themselves quickly (Meridian's $180K vendor-contract catch, the near-miss
caught via a shared severity taxonomy) while platform teams built
preemptively, before real duplication exists to eliminate, tend to guess
wrong about which abstractions matter — there's no duplication yet to
observe and centralize against.

## Exercise

Take your own AI org (or Meridian Health, above, at month 9) and do three
things.

1. **Identify which threshold you're at** using the table in section 1, and
   name the specific symptom (not a hypothetical one) that proves it.
2. **Choose a pod split axis** using the table in section 2, and write two
   sentences justifying the trade-off you're accepting, not just the
   benefit you're gaining.
3. **List the four centralization items in section 4** and mark each
   currently: centralized / pod-specific / doesn't exist yet. For anything
   not centralized, name who should own making it so and by when.
