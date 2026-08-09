# 08 · Change Management for AI Adoption

The most expensive AI failure is not a model that doesn't work. It is a
model that works, ships, and is quietly ignored. The infrastructure runs,
the dashboard is green, the licence renews — and the people it was built
for keep doing the job the old way.

This failure is invisible in every artefact you have looked at so far.
Accuracy is fine. Latency is fine. Uptime is fine. The only number that
would show it is the one nobody put on the dashboard: what fraction of the
intended users actually used it this week, and whether the business metric
moved.

AI adoption is harder than ordinary software adoption for three specific
reasons, and it is worth being precise about them rather than reaching for
generic change-management language. First, **the output is probabilistic**
— a tool that is right 88% of the time asks users to develop a judgement
they have never needed before. Second, **it changes the work itself**, not
just the interface; people are being asked to become editors and reviewers
rather than authors. Third, **it carries an unspoken question about
whether the job survives**, and if you do not answer that question, people
will answer it for themselves, pessimistically.

Adoption is a budget line and a design constraint, not a launch email.

## 1. The adoption funnel

Treat adoption as a funnel with measurable stages, exactly as you would a
product. Each stage has a different failure and a different fix, and
lumping them into "adoption is low" prevents you from choosing between
them.

| Stage | Question | Typical metric | If it fails here |
|---|---|---|---|
| **Aware** | Do they know it exists and what it's for? | % of target population who can describe it | Communications problem — cheap to fix |
| **Able** | Do they have access, permission and enough skill? | % with working access; % who completed onboarding | Enablement problem — usually IT or training |
| **Activated** | Have they tried it on real work? | % with at least one genuine use | Trigger problem — it isn't in their workflow |
| **Repeating** | Do they come back unprompted? | Weekly active as % of target population | Value problem — it didn't help enough |
| **Relying** | Has the old way stopped? | % of eligible work done the new way | Trust or workflow problem |
| **Right-sized trust** | Do they accept good output and catch bad? | Override rate; error escape rate | Calibration problem — the dangerous one |

Two observations change how you read this table. **Most reported adoption
numbers are activation numbers** — someone tried it once during launch
week — and activation decays to nothing without the repeating stage. And
**the last row is not optional**. A population that accepts everything the
system says has adopted the tool and abandoned the judgement, which is
worse than non-adoption because it is silent. Module 07's override rate is
the same measurement seen from the governance side.

## 2. Diagnose resistance before you treat it

"Resistance to change" is a label, not a diagnosis. There are four
distinct causes, they look identical from a distance, and the treatment
for one makes the others worse.

| Cause | What you actually hear | What it means | Correct response |
|---|---|---|---|
| **Rational objection** | "It's wrong on the complex cases" | They are right. The tool is weaker than claimed on part of the work | Narrow the scope. This is product feedback, not resistance |
| **Capability gap** | "I never got round to it" | No time, no practice, no clarity on how it fits their day | Hands-on enablement inside working hours |
| **Incentive conflict** | "It'll hurt my quality score" | Their measurement system punishes the new behaviour | Change the measurement system first |
| **Threat** | "So what happens to us next year?" | An unanswered question about jobs, status or expertise | A direct, specific, honest answer from someone senior |

The most common management error is treating all four as irrational and
responding with more communication. Communication addresses only the
fourth cause, and only if the message is specific enough to be believed.

The most *costly* error is dismissing rational objections. When
experienced practitioners say the tool is bad on hard cases, they are
usually the best evaluation signal you have, and they are describing a
real performance boundary that your offline averages hid.

## 3. Fix the incentive conflict first

Before any rollout, run one check: **does any existing measurement,
target, or quality rubric penalise the new behaviour?** This is the
cheapest high-yield intervention in change management, and it is skipped
almost universally.

| Where to look | The conflict you're hunting |
|---|---|
| Individual performance targets | Volume or speed targets that make learning time unaffordable |
| Quality rubrics and QA scoring | Criteria that mark down assisted phrasing or templated language |
| Team-level KPIs | A metric that necessarily gets worse before it gets better |
| Compensation | Commission or bonus tied to the process being replaced |
| Career narrative | Whether the expertise being automated is what people get promoted for |

If an agent is measured on handle time and the new tool costs 90 seconds
of learning per case in week one, they will not use it — and their choice
is correct. Fix the measurement or accept the outcome.

## 4. Stage the rollout, and gate each stage

Adoption fails most often when a pilot's conditions do not survive
generalisation. A pilot runs on volunteers with the project's founder in
the room; the rollout runs on everyone else, alone. Gate the stages so you
learn that at 25 people rather than 220.

| Stage | Population | Exit criteria before proceeding |
|---|---|---|
| **Design partner** | 5–10 volunteers | The workflow is measurably faster on real work — measured, not felt |
| **Pilot** | One team, 20–40 people, including sceptics | Repeating-stage adoption above target for 3 consecutive weeks; failure boundary documented |
| **Staged rollout** | 2–3 deliberately diverse teams | Adoption holds without the project team in the room |
| **Full rollout** | All | Support load per user declining, not rising |
| **Sustain** | All, ongoing | Quarterly review of adoption and override rate |

The pilot rule worth enforcing: **include the sceptics**. A pilot of
volunteers measures enthusiasm rather than usability, and it produces an
adoption number you cannot reproduce. Sceptics generate the rational
objections from section 2, and those are the findings that make the
rollout work.

## 5. Answer the job question explicitly

Every AI rollout carries the same unspoken question. Silence is read as
the worst available answer. Take a position — approved by whoever actually
decides headcount — before the first announcement, in one of these shapes.

| Position | Say it as | Only say it if |
|---|---|---|
| **Absorb growth** | "Headcount is flat; this covers the volume increase instead of hiring" | The growth forecast is real |
| **Redeploy** | "The time goes to the backlog — to the work we never get to" | You can name that work |
| **Reduce through attrition** | "We expect a smaller team in two years, managed through attrition and reskilling" | Leadership will hold this line publicly |
| **Not decided yet** | "No decision has been made; here is when it will be, and how you'll hear" | You commit to the date and keep it |

The fourth is an acceptable answer. What is not acceptable is an
enthusiastic "this frees you up for higher-value work" with no named
higher-value work — people have heard that sentence before, and they
discount it correctly.

## Worked example

An insurance claims operation rolled out an AI drafting assistant to
**220 adjusters**. It drafted customer responses from the claim file; the
adjuster edited and sent. The business case assumed **70% weekly active
use** and **4 minutes saved on each of 12 responses per adjuster per
day** — at 240 working days and a fully loaded **$42 per hour**, worth
about **$1.24M a year**.

Eight weeks after full rollout, weekly active use was **68 of 220 —
31%** — and only **41 people** used it more than twice a week. Realised
value was running at roughly **27% of plan**, about **$331,000**
annualised. The model had not changed since the pilot, where adoption had
reached 84%.

**The diagnosis.** Thirty non-users were interviewed and their objections
sorted using section 2's four causes.

| Cause | Count | What they said |
|---|---|---|
| Capability gap | 12 | Onboarding was a 20-minute recorded video; nobody had time |
| Rational objection | 8 | Drafts needed near-total rewriting on complex liability claims |
| Incentive conflict | 6 | The QA rubric marked down "templated-sounding" language |
| Threat | 4 | Nobody had said anything about headcount |

Only the last group was resisting change in the sense the phrase usually
implies. The other 26 were responding rationally to their environment.

**What changed.** Five actions, in the order that made them work:

1. **The QA rubric was rewritten first**, with the quality team, so that
   assisted drafts could score well. Nothing else would have worked while
   using the tool cost people points.
2. **Scope was narrowed** to the three claim types where the draft was
   genuinely good — **58% of volume**. The tool was withdrawn from complex
   liability claims, which validated the objectors publicly and ended the
   "it's inaccurate" reputation within about three weeks.
3. **Onboarding moved into team meetings** — 20 minutes hands-on, on the
   adjuster's own live queue, run by their own team lead.
4. **Team leads got an adoption panel** in their weekly numbers, showing
   section 1's funnel broken out by stage rather than one percentage.
5. **The COO answered the job question** in writing: headcount flat for 24
   months, recovered time goes to the 11-day claims backlog. Position two,
   with named work.

**Where it landed.** By week 20, weekly active use was **174 of 220 —
79%** — and because the tool was now scoped to 58% of volume, realised
savings ran at about **$814,000 a year**, or **66% of the original
business case**.

That comparison is the point of the example. The team reached two-thirds
of a plan it had been achieving a quarter of, and it got there by
**deliberately removing 42% of the use cases**. The original plan was not
a target that had been missed; it was an estimate built on a false
assumption about where the model was good. Narrowing the claim made the
tool trustworthy, and trust produced the volume.

Note also that the single most valuable intervention — rewriting the QA
rubric — cost nothing, required no engineering, and would never have been
found by asking the ML team why adoption was low.

## Exercise

Take an AI system your organisation has deployed, or is about to.

1. **Build the funnel** from section 1 with real numbers. If you cannot
   fill the "repeating" and "relying" rows, that measurement gap is your
   first finding — get it instrumented before launch.
2. **Interview eight non-users or reluctant users** and classify each
   objection into one of section 2's four causes. Do not lead the
   conversation: ask what happened the last time they used it, or why they
   didn't.
3. **Hunt the incentive conflict.** Read the actual performance targets
   and quality rubric that apply to the intended users. Name one thing
   that would score worse if they adopted the tool fully.
4. **Write down the failure boundary** — the cases where the system is
   genuinely weak — and decide whether to narrow scope to exclude them.
   Estimate what share of volume you would be giving up.
5. **Draft the job answer** in one of section 5's four shapes, in under
   60 words, and identify who must approve it before it is said out loud.
6. **Set the adoption gate** for your next rollout stage: the specific
   number, sustained over a specific number of weeks, below which you do
   not proceed.
