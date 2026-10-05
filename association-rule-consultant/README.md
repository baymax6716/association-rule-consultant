# Association Rule Consultant

`association-rule-consultant` is a Codex Skill for statistical consultation using association-rule learning, a branch of unsupervised learning. It turns transaction or co-occurrence data into an interpretable report, while first checking whether association rules are actually the right method.

## What it is for

Use it with data such as shopping baskets, service bundles, concurrent symptoms, feature selections, or categorical events that can meaningfully occur together. It can:

- assess whether a dataset and decision question fit association-rule mining;
- cleanly define transactions and item sets, with an auditable record of choices;
- mine and filter rules using support, confidence, lift, and (when useful) leverage;
- check robustness when the decision warrants it; and
- produce a plain-language report that explains findings, limits, and next steps.

It is intentionally not a clustering, prediction, causal-inference, or time-series skill. A rule such as `A → B` describes co-occurrence; it does not show that A causes B.

## Install

Copy the `association-rule-consultant` directory into your Codex skills directory (normally `~/.codex/skills/`), then restart or reload Codex if needed. Invoke it with:

```text
Use $association-rule-consultant to analyze [my dataset] for [my decision question].
```

Attach the data file and state the decision you are trying to make. The Skill inspects the data before asking only the questions that could materially change the analysis.

## How the Skill is designed

The central design choice is a **consultation gate**. It prevents a common failure in unsupervised learning: treating every table as though it were a market-basket dataset. The gate checks the unit of analysis, basket definition, item definition, and intended decision. It then either proceeds, performs a documented transformation, or recommends a better method.

Once the analysis is appropriate, the Skill completes the workflow rather than offloading routine choices to the user. It records defaults and assumptions, uses interpretable quality checks, and produces a report with a non-technical executive answer first and reproducibility details last.

## Repository layout

```text
association-rule-consultant/
├── SKILL.md                         # Invocation and operational workflow
├── agents/openai.yaml               # Codex user-interface metadata
└── references/
    ├── analysis-protocol.md         # Data, mining, and validation guidance
    └── report-blueprint.md          # Required report structure
```

## Presentation outline

1. **Problem:** Association-rule output is easy to over-interpret; many datasets do not contain defensible baskets.
2. **Solution:** The consultation gate establishes fit before analysis.
3. **Method:** The protocol converts data to transactions, evaluates support/confidence/lift, removes redundant rules, and checks robustness.
4. **Communication:** The report explains findings as frequency comparisons, labels exploration honestly, and avoids causal claims.
5. **Value:** A non-statistical stakeholder receives both a practical next step and enough traceability for review.

## License

MIT. See [LICENSE](LICENSE).
