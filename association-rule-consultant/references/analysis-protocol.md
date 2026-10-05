# Association-rule analysis protocol

Use this protocol after the consultation gate has found a defensible basket definition. Its aim is reliable decision support, not the largest possible set of rules.

## 1. Build the analysis table

Record the original shape, column meanings, time coverage, and every assumption. Convert the data into a binary transaction–item table only after deciding the transaction boundary.

| Input shape | Normalization |
| --- | --- |
| Long transaction lines | Group distinct item labels by transaction ID; retain quantity only if it has a pre-agreed itemization rule. |
| Wide binary table | Verify that each row is one basket and that values truly mean present/absent. |
| Repeated event log | Define a session or time window from the business process; disclose it in the report. |

Before mining, measure transaction count, unique items, basket-size distribution, duplicate baskets, missingness, invalid labels, and single-item prevalence. Remove exact duplicate item records *within the same basket* after recording the count. Do not remove duplicate baskets: they are repeated observations. Resolve missingness according to its meaning; “not recorded” is not automatically “not present.”

Exclude identifiers, timestamps, comments, and near-unique labels from the item universe unless they are the explicit subject of the question. Collapse spelling variants only with evidence and retain a mapping. Report exclusions and their rationale.

## 2. Choose a mining strategy and honest filters

Use an established frequent-itemset implementation such as Apriori or FP-growth. Choose based on data scale and density; the choice rarely changes the meaning of the report. Set a minimum support that corresponds to a meaningful minimum number of baskets, and report both the percentage and the count.

Generate candidate rules and evaluate at least:

- **Support:** fraction and count of all baskets containing both sides.
- **Confidence:** fraction of baskets with the antecedent that also contain the consequent.
- **Lift:** confidence divided by the consequent’s overall rate. Values above one signal positive co-occurrence relative to baseline.
- **Leverage:** observed joint rate minus the rate expected if the two sides were independent, when it helps distinguish common-item artifacts.

Use confidence and lift together. A high confidence with lift near one is usually a common consequent, while a striking lift with very few baskets is fragile. Prefer short, readable antecedents unless longer combinations materially improve usefulness. Remove rules that merely restate a simpler rule without a meaningful gain in lift, support, or decision value.

Do not present the filters as universal cutoffs. Start from a support floor tied to enough baskets for the decision, examine the support/confidence/lift trade-off, and log the selected values. If the dataset is small or exploratory, say so instead of manufacturing precision.

## 3. Check robustness

For material decisions, assess whether highlighted rules are robust. Use a time-based holdout when data has natural order; otherwise use a random split or bootstrap resampling. Recalculate support, confidence, and lift and label rules as stable, variable, or insufficiently checked. Do not claim statistical significance solely because a rule clears a mining threshold.

If a formal inferential claim is requested, state that rule search creates a multiple-comparisons problem. Use an explicitly justified confirmatory analysis or recommend a prospective A/B test rather than retrofitting causal language to mined rules.

## 4. Produce useful evidence

For each selected rule, retain its antecedent and consequent, support count/rate, confidence, consequent baseline rate, lift, leverage when used, and stability result. Include the number of rules considered and the filtering route, not only winners. Create only visuals that answer a decision question: a ranked rule table, support-versus-lift scatter, or a small rule network are usually enough. Avoid dense network diagrams that cannot be read.

## Defaults when the user has not specified them

Use these as starting points, then adapt to sample size and decision risk:

- Focus on itemsets of two or three items and state any extension.
- Require a support count large enough for a reader to judge the result; avoid highlighting a rule supported by only a handful of baskets.
- Rank candidates with a balance of support, lift, clarity, and plausible actionability rather than one metric alone.
- Treat the output as exploratory unless it was validated on held-out or future data.

The report must state every default that materially affects findings.
