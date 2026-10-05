# Café demonstration

This folder is a self-contained teaching example for a presentation or first use of the Skill. The data is synthetic: it illustrates the workflow and must never be represented as evidence about a real café.

## Files

- `cafe_transactions.csv` is long-format transaction data. Each `transaction_id` is one basket and each `item` is an item bought in it.
- `cafe-demo-report.md` is a worked consulting report generated from the data. Its figures provide a check that the demonstration was understood correctly.
- `PRESENTATION_GUIDE_zh-TW.md` is a Traditional Chinese script, slide plan, and live-demo checklist.

## Run the demonstration

1. Install or make the `association-rule-consultant` Skill available to Codex.
2. Attach `cafe_transactions.csv`.
3. Send this prompt:

   ```text
   Use $association-rule-consultant to analyze cafe_transactions.csv. I manage a small café and want to decide which items to test as bundles. Produce a plain-language consulting report and clearly distinguish association from causation.
   ```

4. Confirm that the response first identifies the data as 40 transaction baskets, then explains its data checks and produces a report. Compare the selected rule metrics with `cafe-demo-report.md`; minor presentation differences are fine.

## What the example is designed to teach

The example has a clear basket definition, so it should pass the consultation gate. It also contains a deliberately sparse salad/juice tail, which lets you explain why the Skill does not elevate every high-lift, low-count pattern. The report should prioritize a few rules with both usable support and an interpretable possible action.
