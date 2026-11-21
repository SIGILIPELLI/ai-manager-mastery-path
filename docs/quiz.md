---
title: "Final Quiz"
description: "Test what you have learned across all four levels of AI Manager Mastery Path with a 20-question final quiz."
---

# Final Quiz

20 questions drawn from all four levels of this course. You need **70% (14 out of 20)** to pass —
you can retake it as many times as you like. Your best result is saved in this browser.

<div id="mp-quiz-root"></div>

<script type="application/json" id="mp-quiz-data">
[
  {
    "question": "Your CEO asks for a firm delivery date for a new ML feature at kickoff. What should you give?",
    "options": [
      "The vendor's date",
      "No answer",
      "One firm date",
      "A range tied to explicit checkpoints (e.g. feasibility in 3 weeks) that narrows as evidence arrives"
    ],
    "correctIndex": 3,
    "explanation": "AI duration depends on questions only answered by doing the work."
  },
  {
    "question": "A proof of concept shows the approach can't reach the quality bar. How should you treat it?",
    "options": [
      "As a failure to hide",
      "As a reason to add staff",
      "Ignore it",
      "As the project doing its job: it prevented a far more expensive production failure; apply the kill criteria"
    ],
    "correctIndex": 3,
    "explanation": "Budget kill criteria at the end of stages 1–3."
  },
  {
    "question": "The vendor's demo is impressive. What do you do before buying?",
    "options": [
      "Run a pilot on a sample of your own data and check cost at your scale, data handling, p95/p99 latency, SLA and lock-in",
      "Sign based on the demo",
      "Ask for a bigger demo",
      "Trust the benchmark"
    ],
    "correctIndex": 0,
    "explanation": "Demos run on best-case examples."
  },
  {
    "question": "A dashboard shows accuracy, latency and uptime all green, yet users have stopped using the tool. What's missing?",
    "options": [
      "An adoption metric: weekly active use of the intended population and whether the business metric moved",
      "More accuracy",
      "More servers",
      "Fewer features"
    ],
    "correctIndex": 0,
    "explanation": "The costliest failure is a model that works and is ignored."
  },
  {
    "question": "Offline model accuracy improved but engagement dropped. Where's the gap?",
    "options": [
      "In the cloud",
      "Between the model and product metric layers: the team optimised a number that doesn't move the outcome",
      "Nowhere",
      "In the data warehouse"
    ],
    "correctIndex": 1,
    "explanation": "Every project needs a metric per layer and how movement propagates."
  },
  {
    "question": "Project A: $1.7M at 90%. B: $4.2M at 50%. C: $2.1M at 80%. D: $3.0M at 30%. Which has the highest risk-adjusted value?",
    "options": [
      "C at $2.1M",
      "A at $1.7M",
      "B at $2.10M (A $1.53M, C $1.68M, D $0.90M)",
      "D at $3.0M"
    ],
    "correctIndex": 2,
    "explanation": "Value × probability of success. Verified by calculation."
  },
  {
    "question": "Which cost line do AI budgets most often under-plan?",
    "options": [
      "Model research",
      "Usage-driven and non-modelling costs, since modelling is usually the smallest line; use staged funding",
      "Office space",
      "Travel"
    ],
    "correctIndex": 1,
    "explanation": "Commit money in tranches tied to decision points."
  },
  {
    "question": "A model is retrained on customer data collected only to deliver a service. What governance question is breached?",
    "options": [
      "Purpose: data collected for one purpose isn't automatically usable for training and may need a different legal basis",
      "Latency",
      "Cost",
      "Retention only"
    ],
    "correctIndex": 0,
    "explanation": "It's the most common reason a finished model can't ship."
  },
  {
    "question": "A hiring manager says 'we need more research scientists to ship faster'. What's your diagnosis?",
    "options": [
      "Likely the wrong ratio: most orgs need far more applied, MLOps and data engineering capacity than research",
      "Hire managers",
      "Correct, hire researchers",
      "Buy GPUs"
    ],
    "correctIndex": 0,
    "explanation": "Anchor hiring to what the role does."
  },
  {
    "question": "Two pods built separate eval harnesses. What's the first move?",
    "options": [
      "Ignore it",
      "Merge pods",
      "Build a platform immediately",
      "Introduce a shared standard (e.g. one eval report format) before a full platform, and check the duplication is measured"
    ],
    "correctIndex": 3,
    "explanation": "A platform comes when measured duplication justifies it."
  },
  {
    "question": "A deployed model quietly degrades: no errors, uptime 100%. Which monitoring catches it?",
    "options": [
      "Uptime alerts",
      "Disk alerts",
      "CPU alerts",
      "Quality monitoring for drift, input schema changes and outcome metrics, not just latency and errors"
    ],
    "correctIndex": 3,
    "explanation": "Most AI failures trip no conventional alert."
  },
  {
    "question": "A foundation-model vendor updates the model and your outputs change. What contract/term would have helped?",
    "options": [
      "A longer demo",
      "Version pinning and a minimum deprecation notice period",
      "A discount",
      "A logo"
    ],
    "correctIndex": 1,
    "explanation": "Model behaviour can change without a version bump you control."
  },
  {
    "question": "A customer-facing LLM assistant sells into the EU and handles account data. What tier is sensible?",
    "options": [
      "Same as internal tools",
      "Higher risk (e.g. medium-high): customer-facing, EU exposure, account data; run governance intake before production",
      "Not applicable",
      "Low"
    ],
    "correctIndex": 1,
    "explanation": "Treat decisions touching protected categories or EU/state AI laws as high-risk."
  },
  {
    "question": "The board asks for an AI update. What should the report contain?",
    "options": [
      "Only accuracy numbers",
      "A short standing report: strategic positioning, performance vs projection, risk and governance, and forward look",
      "Only good news",
      "A 45-minute technical deep dive"
    ],
    "correctIndex": 1,
    "explanation": "Choose what's board-worthy versus management-level."
  },
  {
    "question": "Leaders announce 'AI will never cost jobs' before plans exist. What's the failure mode?",
    "options": [
      "Good practice",
      "Neutral",
      "False reassurance (the opposite is premature alarm); be honest about what's known and give a dated commitment",
      "Premature alarm"
    ],
    "correctIndex": 2,
    "explanation": "Neither builds trust."
  },
  {
    "question": "Reviews and promotions reward only shipped features. What happens to responsible-AI practices?",
    "options": [
      "They erode, because incentives beat statements; add explicit quality, safety and governance criteria",
      "They improve",
      "They're mandatory",
      "Nothing"
    ],
    "correctIndex": 0,
    "explanation": "Incentive alignment is the most underused lever."
  },
  {
    "question": "You're acquiring an AI startup based on its demo. What two things must you verify?",
    "options": [
      "Logo and website",
      "Sales slides",
      "Office lease",
      "Model reproducibility and data rights/provenance"
    ],
    "correctIndex": 3,
    "explanation": "They're the items most likely to make the capability worth less than represented."
  },
  {
    "question": "A CoE is described by pod leads as 'the team we have to go through'. What's wrong?",
    "options": [
      "It has drifted into an approval gate; refocus on a written narrow mandate, advisory tooling and pod outcomes",
      "Nothing",
      "It needs more staff",
      "It needs more authority"
    ],
    "correctIndex": 0,
    "explanation": "Ambiguity of mandate is the biggest cause of CoE dysfunction."
  },
  {
    "question": "Which is the right first sequence when a platform is justified?",
    "options": [
      "Dashboard first",
      "Model/experiment registry, then shared eval framework, then deployment/serving",
      "Serving first",
      "Hiring first"
    ],
    "correctIndex": 1,
    "explanation": "Sequence by leverage, not technical interest."
  },
  {
    "question": "A company runs 11 AI systems across three business units and drifts from one central AI team. What structure often fits at scale?",
    "options": [
      "One team per model",
      "Fully centralised forever",
      "No structure",
      "Hybrid hub-and-spoke: a central hub for platform, standards and governance with embedded spokes"
    ],
    "correctIndex": 3,
    "explanation": "Past ~3–4 business units with distinct needs, most drift to hybrid."
  }
]
</script>
