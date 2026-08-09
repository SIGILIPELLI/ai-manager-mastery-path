# 07 · Responsible AI Frameworks

Almost every organisation now has AI principles. Fairness, transparency,
accountability, human oversight — the lists are nearly interchangeable, and
they change no decisions, because a principle without a gate attached is a
poster.

The gap between principles and practice is a *process* gap, and processes
are a manager's home ground. This module is about closing it: choosing a
framework so you're not inventing vocabulary, tiering your use cases so
effort lands where risk is, and running an actual checklist at an actual
gate with an actual person who can say no.

The test of whether your organisation does responsible AI is not whether it
has published principles. It is whether it can name something it decided
not to ship, and why.

## 1. The framework landscape

You do not need to adopt all of these, and you should not read all of them.
Know what each is *for*, and pick one as your spine.

| Framework | What it is | Best used as | Certifiable? |
|---|---|---|---|
| **NIST AI Risk Management Framework** | A voluntary US framework organised around four functions — Govern, Map, Measure, Manage | Your internal operating structure; the most practical starting point | No |
| **ISO/IEC 42001** | A management-system standard for AI, structured like ISO 27001 | Formal assurance; useful when customers demand evidence | Yes, via audit |
| **EU AI Act** | Regulation with obligations tiered by risk level | A compliance obligation if you touch the EU market — not optional | Conformity assessment for high-risk |
| **OECD AI Principles** | High-level intergovernmental principles | Vocabulary and executive framing | No |
| **Sector rules** | Financial model-risk governance, medical device regulation, employment law | Often the binding constraint, ahead of any AI-specific rule | Varies |

Two orientation points. First, most organisations get furthest fastest by
using **NIST AI RMF as the internal spine** — it is structured as
activities rather than statements, so it maps onto a delivery process —
and treating other frameworks as either compliance obligations (EU AI Act)
or optional assurance (ISO 42001). Second, **your sector's existing rules
usually bind harder than anything AI-specific**. A bank's model-risk
governance and an employer's discrimination law obligations already apply
in full; "it's AI" is not a new regime, it is a new way to breach an old
one.

Regulatory detail moves quickly. Treat the specific obligations and dates
as something to confirm with counsel each planning cycle rather than
something to memorise here.

## 2. Tier your use cases before you spend effort

Uniform process across all AI use cases guarantees the wrong outcome: it
is too heavy for the trivial cases, so people route around it, and by the
time the consequential case arrives the process has no credibility left.
Tier first.

| Tier | Definition | Examples | Process weight |
|---|---|---|---|
| **T1 — Minimal** | No effect on people; easily reversed | Internal search, meeting summaries, code assistance | Register it. That's all |
| **T2 — Moderate** | Affects work quality or customer experience; human in the loop | Draft replies, lead scoring, demand forecasting | Short checklist, ML lead signs |
| **T3 — Consequential** | Materially affects a person's money, access, or opportunity | Credit decisions, hiring screens, claims triage, pricing | Full checklist, named sign-offs, monitoring, appeal route |
| **T4 — Prohibited / prohibitive** | Legally barred, or beyond your risk appetite | Varies by jurisdiction and by company policy | Don't. Escalate to legal to confirm the boundary |

The tiering question that resolves most disputes: **"if this system is
wrong about a specific person, what happens to that person, and can they
do anything about it?"** If the answer involves lost money, a lost
opportunity, or a lost service — and no route to challenge it — it is T3,
regardless of how simple the model is. A three-line rule that denies people
credit is a higher-tier system than a neural network that summarises
meetings.

## 3. The responsible-AI checklist

This is the deliverable. Run it at a gate before launch, and re-run it
annually or whenever purpose or population changes. T2 uses the starred
rows only; T3 uses all of them.

| # | Item | Evidence required | Owner |
|---|---|---|---|
| 1 ★ | **Purpose is documented** — what decision this system informs and what it must not be used for | One-paragraph statement, approved | Product |
| 2 ★ | **Data is lawful for this purpose** (Module 04) | Purpose flag + privacy review sign-off | Legal/privacy |
| 3 ★ | **Baseline is documented** — what the current human or rule-based process achieves | Measured baseline number | AI manager |
| 4 | **Performance measured across subgroups**, not just overall | Metric table broken out by relevant group | ML lead |
| 5 | **Disparity threshold agreed in advance**, with a decision rule if breached | Written threshold, dated before results | AI manager + legal |
| 6 ★ | **Failure modes enumerated** — what a wrong output does, in both directions | Failure table with severities | ML lead + product |
| 7 | **Human oversight designed, not assumed** — who reviews what, with what time and information | Workflow spec + reviewer capacity estimate | Product + design |
| 8 | **Explanation available per decision** at a level the affected person can act on | Sample explanation, tested with a real user | Design |
| 9 | **Appeal / contest route exists and is reachable** | Documented path + owner of the queue | Operations |
| 10 ★ | **Monitoring plan in place** with thresholds and named alert recipients (Module 03) | Dashboard spec | ML lead |
| 11 | **Rollback tested** | Date of last rehearsal | Engineering |
| 12 ★ | **Residual risk stated and formally accepted** by a named person | Signed risk acceptance | Accountable executive |
| 13 | **Review date set** | Calendar entry with owner | AI manager |

Item 5 is the one that does the most work and is skipped most often.
Agreeing a disparity threshold *before* the numbers arrive is the same
mechanism as the pre-committed metric threshold in Module 01 — it prevents
the result from setting the standard. Item 12 is the one that changes
behaviour: risk that must be signed for by a named individual gets read.

## 4. Human oversight that is real

"A human reviews it" is the most-claimed and least-delivered control in
responsible AI. Three failure patterns, and the test that catches each.

| Pattern | What it looks like | Test |
|---|---|---|
| **Rubber-stamping** | Reviewer approves 99% of recommendations | What is the actual override rate? Below ~5% on a consequential system, oversight is decorative |
| **No time to review** | 90 seconds per case, 200 cases a day | Compute seconds available per case against seconds needed |
| **No information to review with** | Reviewer sees a score, not the reasoning | Can the reviewer state *why* they'd disagree? |

Override rate is the single best health metric for oversight. Track it,
publish it, and treat a collapse in it as an incident rather than as
success. A reviewer population that has stopped disagreeing has stopped
reviewing.

## 5. Evidence beats intentions

When a regulator, customer, or journalist asks, the question is never "did
you care?" — it is "show me." Decide in advance what artefact answers each
likely question.

| Question you will be asked | Artefact that answers it |
|---|---|
| What does this system do, and to whom? | Use-case register entry with tier |
| Was the data allowed to be used this way? | Privacy/purpose sign-off |
| Does it perform equally well across groups? | Subgroup metric table, dated, versioned |
| Who decided it was acceptable? | Signed residual-risk acceptance |
| What happens when it's wrong? | Failure table + appeal route + queue statistics |
| Would you notice degradation? | Monitoring spec + alert history |

A **use-case register** — one row per AI system, with tier, owner, launch
date and last review — is the cheapest high-value artefact on this list.
Most organisations cannot produce a complete list of the AI systems they
run, which makes every other control unverifiable.

## Worked example

A 3,000-person company deployed an AI screening tool to rank applicants for
high-volume customer-service roles, roughly 8,000 applications a quarter.
It was bought, not built, and had been in pilot for two months when a new
AI manager applied the tiering question.

**Tier:** T3. Wrong on a specific person means a lost job opportunity, with
no route to challenge. The pilot had been governed as T1 — registered,
nothing more — because "the recruiter makes the final call."

The checklist produced five findings.

| Item | Finding |
|---|---|
| 3 — Baseline | Nobody had measured the incumbent process. Two recruiters screening the same 200 CVs agreed on only 61% of advance/reject calls. The human baseline was far weaker than assumed — a genuine argument *for* the tool |
| 4 — Subgroup performance | The vendor supplied aggregate accuracy only. A commissioned analysis on 4,000 historical applications found advance rates 9 percentage points lower for candidates with employment gaps over six months — a proxy correlating with parental leave |
| 5 — Threshold | No threshold had ever been agreed |
| 7 — Human oversight | Recruiters had ~40 seconds per candidate and saw only a 1–100 score. Override rate was 2% |
| 9 — Appeal | No route existed; rejected candidates received a generic email |

Item 7 is the finding that mattered most. The entire governance case for
running this as low-risk rested on "the recruiter makes the final call,"
and a 2% override rate with 40 seconds and a bare score meant no
meaningful call was being made. The claimed control did not exist.

What happened next was not "stop the project."

1. **Re-tiered to T3**, with the full checklist and a named accountable
   executive (the CHRO).
2. **Agreed a disparity threshold in advance** for the re-run: no
   subgroup's advance rate more than 5 points below the overall rate,
   escalation and remediation if breached.
3. **Removed the features** driving the employment-gap effect and required
   the vendor to re-run on the company's own historical data. The gap
   narrowed to 3 points; overall ranking quality dropped slightly and was
   accepted.
4. **Redesigned the reviewer workflow.** Scores were replaced by the three
   strongest evidence points per candidate; borderline candidates were
   routed to a longer review with 4 minutes allocated. Override rate rose
   to 14%.
5. **Built an appeal route** — rejected candidates could request a human
   re-review, staffed at an estimated 60 requests a quarter.
6. **Set monitoring** on advance rates by subgroup, reviewed monthly, with
   the CHRO's chief of staff on the alert list.

And one thing was *not* shipped. The vendor offered a video-interview
scoring module assessing "communication style and enthusiasm" from
recorded answers. The team could not articulate what construct it measured,
the vendor would not explain the training data, and no defensible
disparity analysis was possible. It was declined — the answer to "name
something you decided not to ship" that this organisation had previously
lacked.

The transferable point: the checklist did not block the project. It
converted a vague sense that "HR AI is risky" into five specific,
addressable findings, four of which were fixed in six weeks. Responsible AI
done as a checklist is an engineering activity. Done as a principle, it is
an argument.

## Exercise

1. **Build a use-case register.** List every AI system your organisation
   runs or is building — you will almost certainly find you cannot complete
   it, which is itself the first finding. Assign each a tier using section
   2's table.
2. **Apply the tiering question** ("if this is wrong about a specific
   person, what happens to them, and can they do anything about it?") to
   your highest-stakes system. If the tier you get differs from how it is
   currently governed, you have found your priority.
3. **Run the section 3 checklist** against that system. For each item,
   record: satisfied / not satisfied / no evidence either way. The third
   category is usually the largest and is the real output.
4. **Test the oversight claim.** Find the actual override rate and the
   actual seconds available per case. Compare against section 4. If nobody
   measures override rate, arrange for it to be measured.
5. **Identify your accountable signer** for item 12. Name the individual —
   not a committee — who would sign the residual-risk acceptance. If you
   cannot, that gap is the most important one on the list.
6. **Write the disparity threshold** you would commit to in advance for
   this system, before looking at any subgroup results.
