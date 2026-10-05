# Café bundle opportunity: demonstration report

> **Teaching-only example.** The 40 transactions in this report are synthetic. The findings demonstrate how the Skill communicates association rules; they are not advice about a real business.

## Executive answer

This dataset is suitable for association-rule analysis because every transaction ID defines one purchase basket. The clearest patterns are tea with cake, soup with sandwich, and coffee with croissant. A café manager could test small bundle displays or offers for these pairs, then measure whether the pilot improves basket value or margin. These patterns show items occurring together; they do **not** prove that placing one item in a basket causes the other purchase.

## Question, data, and scope

**Decision question:** Which item combinations are reasonable candidates for a small café bundle pilot?

The data contains 40 synthetic purchase baskets and eight distinct item labels. Each record is one item within one transaction. There are no missing item labels, no duplicate item labels within a transaction, and no dates or customer identifiers. Because the data has no time sequence or outcome such as profit, this analysis cannot tell us whether a bundle would increase sales or which customer group would respond.

## Method

The analysis groups records by `transaction_id` and searches for items that occur together more often than their separate purchase frequencies would imply. It uses:

- **Support:** how many of all baskets contain both items.
- **Confidence:** among baskets containing the first item, how often the second is also present.
- **Lift:** how much more often the second item appears than its usual rate. A lift above 1 indicates positive co-occurrence.

The report highlights short pairs with usable support. It does not treat the two one-off items, salad and juice, as findings: a rare pattern can look dramatic but is not sufficiently supported for a decision.

## Findings

| Pattern | Joint baskets | Confidence | Usual rate of outcome | Lift | Plain-language reading |
| --- | ---: | ---: | ---: | ---: | --- |
| tea → cake | 7 / 40 (17.5%) | 7 / 8 (87.5%) | 8 / 40 (20.0%) | 4.38 | Tea baskets include cake far more often than cake occurs overall. |
| soup → sandwich | 6 / 40 (15.0%) | 6 / 6 (100.0%) | 9 / 40 (22.5%) | 4.44 | Every soup basket in this small sample also contains a sandwich. |
| coffee → croissant | 12 / 40 (30.0%) | 12 / 20 (60.0%) | 12 / 40 (30.0%) | 2.00 | Coffee baskets contain croissants twice as often as croissants appear overall. |

The reverse-direction rules have the same support and lift but answer a different operational question. For example, croissant → coffee has 100% confidence because all 12 croissant baskets include coffee; this makes it useful for deciding what to display alongside croissants. The report avoids listing both directions as separate headline findings when one explanation is enough.

## Recommended action

1. Pilot one clear pair at a time: coffee–croissant, tea–cake, or sandwich–soup. Display the complementary item together or test a modest bundle offer.
2. For two to four weeks, compare basket value, unit margin, and bundle uptake against a comparable period or store condition. Assign a manager to record the offer exposure.
3. Collect date/time and price/discount fields before the next analysis. This enables a time-based validation and helps separate recurring behavior from a short promotion effect.

## Limitations and conclusion

The dataset is small, synthetic, and observational. It has no timing, price, or customer context, so the rules are exploratory co-occurrences only. The original demonstration question is answered: three pairs are plausible bundle candidates, but a controlled pilot is needed to decide whether any one increases value.

## Reproducibility record

- Source: `cafe_transactions.csv`
- Unit of analysis: transaction basket (`transaction_id`)
- Transactions: 40; unique items: 8
- Item prevalence: coffee 20, croissant 12, tea 8, cake 8, sandwich 9, soup 6, salad 1, juice 1
- Rule metrics: support, confidence, and lift; highlighted pairs have at least 6 joint baskets
- Validation: none; teaching data has no time field or held-out sample
