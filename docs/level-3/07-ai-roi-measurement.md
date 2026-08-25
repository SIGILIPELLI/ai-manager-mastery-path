# 07 · AI ROI Measurement

"What's the ROI of AI?" is a question you will be asked by finance, by the
board, and by your own VP, usually before you have clean data to answer it
well. The honest answer requires resisting two temptations: inflating
soft benefits to justify a project that's already been approved, and
under-crediting an initiative because its savings are diffuse and hard to
attribute. This module gives you a repeatable ROI model, the discipline of
separating hard from soft benefits, and a worked calculation you can adapt.

## 1. The AI ROI components

Every AI initiative's ROI case has the same four buckets. Keep them
separate — collapsing them into one "value created" number is exactly how
ROI claims lose credibility under scrutiny.

| Component | Definition | Measurement difficulty |
|---|---|---|
| Hard cost savings | Directly measurable reduction in labor, compute, or operational spend | Low — usually has a clean before/after number |
| Revenue impact | Increased conversion, retention, or average order value attributable to the AI feature | Medium — needs a controlled comparison (A/B test or matched cohort) |
| Risk/cost avoidance | Fraud caught, compliance violations prevented, incidents avoided | Medium-high — requires a credible counterfactual estimate |
| Soft/strategic value | Improved decision speed, employee satisfaction, competitive positioning | High — rarely quantifiable with confidence; report qualitatively, don't force a dollar figure |

A credible ROI report leads with the first two buckets, includes the third
with an explicit stated assumption, and mentions the fourth without
pretending it's been quantified.

## 2. The ROI calculation template

| Field | Definition | Source |
|---|---|---|
| Build cost | One-time cost to build (loaded engineering time, data acquisition, tooling) | Finance/engineering time tracking |
| Annual run cost | Ongoing cost (compute, API/vendor fees, maintenance FTE allocation) | Cloud/vendor invoices, headcount allocation |
| Annual gross benefit | Total measured savings/revenue attributable, per component table above | Whatever hard metric the initiative targets |
| Net benefit, year 1 | Gross benefit − run cost − build cost (build cost typically hits once) | Calculated |
| Net benefit, year 2+ | Gross benefit − run cost | Calculated |
| Payback period | Time from launch until cumulative net benefit turns positive | Calculated |
| 3-year ROI | (3-year cumulative benefit − 3-year cumulative cost) ÷ 3-year cumulative cost | Calculated |

Always report **payback period measured from launch**, not from project
start — conflating build time into the payback clock understates how fast
the investment turns around once it's actually live, and overstates it if
you're trying to look impressive to a skeptical board.

## 3. Attribution discipline

The most common way ROI claims fall apart under audit is weak attribution
— crediting the AI system with a metric movement that had other causes.
Defend against this with:

- **A held-out comparison group** wherever feasible (a region, a customer
  segment, or a time-boxed A/B test) rather than simple before/after, which
  conflates the AI's effect with seasonality, marketing campaigns, or
  unrelated product changes running concurrently.
- **A stated confidence level**, not false precision — "we estimate
  $1.1–1.4M in annual savings, based on a 6-week A/B test with 95%
  confidence interval ±12%" is more credible than a single unqualified
  number, and survives scrutiny better.
- **Separating deflection from quality.** For AI systems that automate a
  task, distinguish savings from full automation (no human touch at all)
  from savings via partial efficiency gains (humans still involved, faster)
  — the confidence level and risk profile differ.

## 4. Reporting cadence and audience

| Audience | Frequency | What they need |
|---|---|---|
| Project sponsor / product lead | Monthly | Leading indicators (adoption, deflection rate) plus running cost tally |
| Finance | Quarterly | Realized hard savings vs. projected, budget variance |
| Executive/board | Quarterly or per major milestone | 3-5 line summary: cost, benefit, payback status, biggest risk to the case |

Never let the first time finance sees the ROI numbers be the quarterly
report — align on methodology (which of the four components counts, what
counterfactual is used) before the initiative launches, so the eventual
number isn't contested on methodology when it matters most.

## Worked example

A telecom company, Bramwell Communications, built an LLM-based support
system that answers common billing and plan questions directly and
shortens handle time on the tickets it still routes to human agents. Build
cost was $310,000 (loaded cost of a 5-person team over 4 months); annual
run cost (LLM API usage, monitoring infra, 1.5 FTE for prompt/eval
maintenance) was $145,000.

Against a baseline of 1.2 million tickets/year at an average fully-loaded
cost of $4.20/ticket, the system fully deflected 22% of tickets (264,000
tickets, verified via a held-out control region that kept the old flow for
6 weeks) and reduced average handle time by 15% on the remaining 936,000
tickets still reaching a human. That works out to:

- Deflection savings: 264,000 × $4.20 = **$1,108,800/year**
- Handle-time savings on the rest: 936,000 × $4.20 × 15% = **$589,680/year**
- **Total annual gross benefit: $1,698,480**

Against the $310,000 build cost and $145,000 annual run cost: year-1 net
benefit was $1,698,480 − $145,000 − $310,000 = **$1,243,480**; year 2+ net
benefit is $1,553,480/year. Payback period measured from launch (not from
project start) was **2.4 months** — ($310,000 ÷ (($1,698,480 −
$145,000)/12)). Three-year ROI, measured against total 3-year cost
(build + 3 years of run cost), was approximately **5.8x**.

The board report led with the deflection and handle-time numbers (hard,
A/B-verified), noted the risk/cost-avoidance category didn't apply here,
and mentioned — without quantifying — the qualitative benefit that support
agents reported the AI-assisted queue felt less repetitive, which the head
of support flagged as a likely (but unmeasured) contributor to a drop in
agent attrition that quarter.

## Exercise

Take an AI initiative you manage, are proposing, or a plausible one.

1. **Fill in the ROI calculation template** in section 2 with real or
   reasonable-estimate numbers. Verify your arithmetic explicitly — payback
   period and 3-year ROI should be calculated, not eyeballed.
2. **Design the attribution method** from section 3: what's your
   counterfactual (control group, matched cohort, before/after with stated
   caveats), and what confidence range would you actually report?
3. **Write the 5-line board summary** for this initiative using the
   reporting cadence in section 4 — cost, benefit, payback status, and the
   single biggest risk to the case holding up under scrutiny.
