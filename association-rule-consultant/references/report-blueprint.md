# Report blueprint

Create the report in this order. Use short paragraphs, descriptive headings, and tables whose numbers agree with the analysis artifact.

## 1. Executive answer

Answer the consulting question in plain language within the first page. State whether the data was suitable, how many baskets were analyzed, the two to five most useful patterns, and the recommended next action. Include one sentence that association is not causation.

## 2. Question, data, and scope

State the user’s decision question, intended audience, source files, period covered, unit of analysis, transaction/session definition, and item definition. Say what question this analysis does not answer. List exclusions, transformations, and missing-data handling in a compact audit table.

## 3. Data quality and readiness

Give the transaction count, unique-item count, typical basket size, important data-quality findings, and their practical implications. If the data was unsuitable, end the analytical portion here and give the recommended alternative method and data needed to proceed.

## 4. Method in everyday language

Explain that the process searched for item combinations occurring together more often than expected from their individual frequencies. Define support, confidence, and lift with the report’s own numbers. State the algorithm, key selection criteria, redundancy handling, validation approach, and the exploratory or confirmatory status.

## 5. Findings and interpretation

Use a ranked table for selected rules:

| Pattern | Joint baskets | Confidence | Usual rate of outcome | Lift | Robustness | Plain-language reading |
| --- | ---: | ---: | ---: | ---: | --- | --- |

For each highlighted rule, give one short paragraph connecting the numbers to a possible operational use. Explain both the observed relationship and the appropriate restraint. If the rule could be driven by a common item, a promotion, seasonality, selection bias, or a chosen session boundary, say so.

## 6. Recommended actions

Separate actions into:

1. A low-risk pilot or operational check, including target population, owner/decision context, and success measure.
2. A validation step if the finding will influence a material decision.
3. Data improvements that would make a future analysis stronger.

Avoid recommendations that treat a rule as proof that adding the antecedent will cause the consequent.

## 7. Limitations and conclusion

State the limits that actually apply: observational data, basket/session choice, missing data, sparse support, unstable rules, limited time coverage, and unmeasured confounders. Close with a direct sentence on whether the original question was answered and what remains unknown.

## Appendix: reproducibility record

Record software/libraries and versions if available, file names and hashes where appropriate, preprocessing steps, item inclusion/exclusion rules, thresholds, candidate-rule count, final-rule count, validation design, and where the analysis code or commands live. Keep secrets and row-level sensitive data out of the appendix.
