# 09 · Budgeting for AI Projects

Software budgeting is mostly a headcount exercise: decide how many people
for how long, add tooling, done. AI budgeting breaks that model in two
places. Part of the cost is **usage-driven** and scales with success
rather than with staffing. And the front of the project is **genuinely
unpredictable** — you are buying an answer to "is this feasible at
acceptable quality," and no amount of planning discipline turns that into
a fixed-price estimate.

Both problems have the same root: teams are asked to commit to a
twelve-month number at the moment they know least. They produce one, it is
wrong, and the resulting credibility loss is far more damaging than the
variance itself.

The way out is not better forecasting. It is **staged funding** —
committing money in tranches tied to decision points — plus honest unit
economics so that finance understands which costs grow when the product
succeeds. This module gives you a cost taxonomy, a staged funding
structure, an estimate-range convention, and the two numbers finance will
actually ask for.

## 1. Where the money actually goes

The most common budgeting error is building the plan around modelling
work, which is usually the smallest line. Model each of these
explicitly — a line at zero is a decision, an omitted line is a surprise.

| Cost category | What it covers | Typical share | Behaves like |
|---|---|---|---|
| **People — build** | ML, data and platform engineering; product; design | 45–65% | Fixed, for the period |
| **People — run** | Maintenance, retraining, on-call, improvement | 15–25% | Fixed, forever |
| **Data work** | Sourcing, cleaning, labelling, annotation vendors | 5–20% | Lumpy; recurs on every refresh |
| **Evaluation** | Building and refreshing the eval set; human review of outputs | 2–8% | Recurring, underestimated |
| **Training / experiment compute** | Runs during development | 1–10% | Bursty, capped by discipline |
| **Inference / serving** | Per-call model fees or hosted infrastructure | 1–15% | **Variable with usage** |
| **Platform & MLOps** | Tracking, registry, monitoring, orchestration (Module 03) | 3–8% | Fixed, plus per-system |
| **Vendor & licence** | Third-party products, per-seat or per-unit | 0–30% | Contractual |
| **Governance** | Legal, privacy, bias analysis, audit, review forums (Module 07) | 2–6% | Per-system, tier-dependent |
| **Change management** | Enablement, training, comms, adoption support (Module 08) | 3–10% | One-off, then a trickle |

Three lines are omitted most often, in this order: **run cost**,
**evaluation**, and **change management**. Each is the subject of an
earlier module for the same reason — they are where projects that passed
their demo go to fail. A budget with no run line is not a budget for a
product; it is a budget for a prototype.

Note also that percentage shares vary enormously by project shape. A
buy-and-wrap build has almost no training compute and a large vendor line;
a from-scratch model has the reverse. Use the table as a checklist of
categories, not as an allocation guide.

## 2. Fund in stages, not in one commitment

Ask for one number covering discovery through production and you will
either pad it (and lose the project) or lowball it (and lose your
credibility in month seven). Split the ask.

| Stage | Purpose | Typical size | The decision it buys | Estimate accuracy |
|---|---|---|---|---|
| **Discovery** | Is it feasible? Is the data adequate? | 3–8% of expected total | Go / no-go on the whole thing | ±10% — it's time-boxed |
| **Prototype** | Does the quality clear the pre-agreed bar? (Module 01) | 10–20% | Whether to productionise | ±25% |
| **Build & pilot** | Ship to a limited population | 40–55% | Whether to roll out (Module 08) | ±30% |
| **Rollout** | Full deployment, enablement, hardening | 15–25% | — | ±20% |
| **Run** | Steady-state operation | Annual, forever | Whether to keep it alive | ±15% |

The framing that gets this approved: **each stage is an option, not a
commitment.** You are asking for the cost of removing the biggest current
uncertainty, and explicitly reserving the right to stop. Finance
departments are comfortable with options — they are far less comfortable
with a project that cannot be stopped because the money is already
committed.

Two rules make staged funding honest. **Discovery must be time-boxed, not
outcome-boxed** — "six weeks to find out" is fundable; "however long it
takes to hit 90%" is not. And **the kill criterion is written before the
stage starts**, not negotiated after the results arrive.

## 3. State estimates as ranges, and say why

A single number implies a precision you do not have. Present ranges with
the range narrowing by stage, and the reason for the width stated.

| At this point | Quote the total as | Because the open question is |
|---|---|---|
| Before discovery | An order of magnitude ("$0.5M–$1.5M") | Whether the data supports it at all |
| After discovery | ±40% | Quality is unproven |
| After prototype | ±25% | Integration and edge cases |
| After pilot | ±15% | Adoption rate and usage volume |
| In run | ±10% | Volume growth and vendor repricing |

Managers resist this because ranges feel weak. In practice a stated range
with a stated cause reads as competence, and a single confident number
that later moves 60% reads as either incompetence or manipulation. You
only get to be wrong quietly once.

## 4. Unit economics: the number finance will ask for

Total cost answers "can we afford it." Unit cost answers "should we scale
it," and it is the question that arrives second and matters more.

> **Cost per unit of value = total annual cost ÷ units of value delivered
> per year**

Choose the denominator from Module 02's business layer, not the model
layer: deflected tickets, documents processed, applications screened,
incremental conversions. Then compare it to the cost of the thing it
replaces. This one line does more persuasive work than any accuracy
number, because it is denominated in the same currency as everything else
finance looks at.

The trap specific to AI is **the variable line that grows with success**.
Fixed-cost software gets cheaper per unit as you scale; usage-priced
inference does not. Before scaling, run a three-point sensitivity:

| Scenario | What you're testing |
|---|---|
| Volume at 3× plan | Does the unit economics still work, or does the variable line eat the margin? |
| Tokens or calls per interaction at 5× | Multi-step and retrieval-heavy designs consume far more than single-call ones |
| Vendor reprices upward 30% | How much of your business case depends on a price you don't control |

The second row catches the failure most teams walk into. A design change
from one model call per interaction to a ten-step agentic flow is invisible
in the architecture review and multiplies the usage line by an order of
magnitude.

## 5. What not to promise

Four commitments that reliably damage AI managers, and what to say
instead.

| Don't promise | Say instead |
|---|---|
| A specific accuracy figure before discovery | "Discovery tells us the achievable range by 15 March" |
| ROI in year one on a build project | "Payback in month 20–26; here's the sensitivity" |
| That the run cost is small | "Run cost is $X a year, forever; that's the real commitment" |
| Headcount savings you can't control | Cost avoidance against a specific growth forecast |

The third deserves emphasis. The decision you are really asking for is not
the build cost — it is the **perpetual annual run cost**. Presenting that
number early, unprompted, is the single strongest credibility move
available in an AI budget conversation.

## Worked example

A B2C software company received **480,000 support contacts a year** and
wanted an AI assistant to resolve common questions before they reached an
agent. Fully loaded cost of an engineer: **$190,000**. Fully loaded cost of
a human-handled contact: **$6.40**. Target: **22% deflection**.

The design was buy-and-wrap (Module 06): a hosted model, with the
company's own retrieval, guardrails and evaluation on top.

**The three-year budget.**

| Year 1 — build | Amount |
|---|---|
| Discovery — 2 people × 6 weeks | $44,000 |
| Build — 3.5 FTE × 5 months | $277,000 |
| Knowledge-base cleanup — 0.5 FTE × 4 months + contractor | $57,000 |
| Evaluation set construction + human labelling | $18,000 |
| Model usage fees (4 months live, partial year) | $2,000 |
| Platform & infrastructure | $22,000 |
| Governance, legal & privacy review | $15,000 |
| Change management, training & comms | $30,000 |
| **Year 1 total** | **$465,000** |

| Years 2–3 — run, each year | Amount |
|---|---|
| Maintenance & improvement — 1.2 FTE | $228,000 |
| Model usage fees — 288,000 conversations at ~$0.031 each | $9,000 |
| Platform & infrastructure | $26,000 |
| Eval refresh & re-labelling | $12,000 |
| Vendor management — 0.1 FTE | $19,000 |
| Annual governance review | $8,000 |
| **Annual run cost** | **$302,000** |

Three-year total: **$1,069,000**.

**The finding that reframed the conversation.** Model usage fees across
all three years came to **$20,000 — under 2% of the programme.** The
project had been discussed internally for months as "the AI cost
question," and every debate had been about per-call pricing. It was
noise. **Ninety-one percent of the three-year cost was people**, and the
single largest commitment was the $302,000 annual run line that nobody had
put on a slide.

**The value side.** At 22% deflection, **105,600 contacts** a year avoid a
human at **$6.40** each — **$675,840** of gross annual value. Against the
$302,000 run cost:

- **Cost per deflected contact: $2.86**, versus $6.40 handled by an agent.
- Net **$3.54** saved per deflected contact.
- Year 1 was net negative by about **$322,000** (four months live, at a
  ramping 14% deflection). Year 2 returns about **$374,000**. Cumulative
  break-even lands around **month 22**.

The claim was written as cost avoidance, not headcount reduction: support
volume was forecast to grow 9% a year, so deflection absorbed growth
rather than removing people. That is position one from Module 08's table,
and it made the same number defensible to both finance and the support
organisation.

**The sensitivity that changed the design.** During build, the team
proposed a multi-step agentic flow, escalating retrieval until confident.
Run against section 4's second scenario, usage on all 480,000 contacts at
roughly nine times the token volume came to about **$91,000 a year** — up
from $9,000, and now **23% of run cost** instead of 3%. Still not the
dominant line, but no longer noise, and it would have arrived as an
unbudgeted overrun in month 14. The design shipped with a per-conversation
step cap, and the usage line got its own monitoring panel.

The transferable lesson: the loudest cost in AI budget discussions is
usually the smallest, and the cost that actually decides the project is
the annual run line. Find the real distribution before the argument, not
after it.

## How It Actually Works

The multi-step agentic flow's nine-fold usage jump is a direct consequence
of how token-metered pricing composes across steps: a single-call design
pays for one prompt-plus-response per interaction, while an escalating-
retrieval flow that calls the model repeatedly (retrieve, re-rank, draft,
critique, revise) pays the same per-token rate multiple times per
interaction, and each additional step doesn't just add a fixed increment —
it compounds against whatever context (retrieved documents, prior turns) is
carried into that step. A step that re-sends the accumulated conversation
history as part of its prompt pays for that history's tokens again on every
call, which is why architectural choices invisible in a design review (how
many model calls per interaction, how much context each call carries)
translate directly and nonlinearly into the usage-fee line — the per-call
price didn't change, but the number of billable calls per unit of business
value did, by an order of magnitude the team didn't measure until it was
running.

The $2.86-vs-$6.40 unit-cost comparison is the right lens specifically
because it holds the *denominator* fixed to a business-meaningful unit
(a deflected contact) rather than a model-internal one (a token, an
inference call), which is the same discipline as Module 02's insistence on
translating model metrics into dollars. A cost-per-token number can look
alarmingly large in isolation while being a rounding error against the
value delivered, or the reverse — cheap per call but delivering so little
value per call that the unit economics never clear the baseline. Only
computing cost divided by the actual unit of value (not the unit of
compute) lets the two be compared on the same footing as the alternative
being displaced, which is exactly the arithmetic that reframed "the AI cost
question" from a debate about $0.031-per-conversation pricing into the real
question: the $302,000 people-heavy run line that actually decided whether
the project was worth funding.

## Exercise

Take one AI project you are running, planning, or could plausibly propose.

1. **Fill in every row** of section 1's cost table, including zeros. Any
   row you cannot estimate is a research task, not a rounding error.
2. **Split it into stages** using section 2 and write the kill criterion
   for the first stage, in advance, in one sentence.
3. **Isolate the annual run cost** and state it separately from the build
   cost. Ask yourself whether you would still propose the project if that
   number were the only one on the slide.
4. **Compute cost per unit of value**, using a denominator from the
   business layer. Compare it to the current cost of the same unit.
5. **Run the three sensitivities** in section 4. Note which one, if it
   happened, would break the business case — that is the number to
   monitor, and it belongs on the dashboard from Module 03.
6. **Rewrite your headline number as a range** with the reason for its
   width, and check the range against section 3's convention for your
   current stage.
