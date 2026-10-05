---
name: association-rule-consultant
description: "Assess transaction or co-occurrence data for association-rule mining, then deliver an interpretable statistical-consulting report with actionable, non-causal findings. Use for market baskets, service bundles, symptom/item co-occurrence, and binary categorical event data; not for clustering, supervised prediction, causal claims, or primarily continuous data."
---

# Association Rule Consultant

Turn a vague question and a dataset into either a clear referral or a complete, decision-ready association-rule analysis. The analysis is useful when each row or group represents a *basket* of items that can occur together; its output describes co-occurrence, never cause and effect.

## Consultation gate

Start by inspecting the supplied data and the user’s stated decision. Establish the unit of analysis, transaction identifier (if any), item identity, time window, and whether repeated rows are meaningful. State in plain language what the data can answer and what it cannot. Ask only for information that changes the analysis materially; if a defensible default is available, record it and continue.

Classify fit before mining:

- **Proceed:** transaction–item records or binary item indicators, with a plausible action that could follow a co-occurrence finding.
- **Proceed with a declared transformation:** numeric values need meaningful bins, event logs need a defensible session/window, or an entity has repeated transactions. Seek approval only when the choice could change the user’s decision; otherwise choose a conservative default and document it.
- **Refer or reframe:** the request is prediction, customer segmentation, hypothesis/causal inference, a trend over time, or the data lacks a defensible basket definition. Explain the better method and offer an association-rule analysis only for the part that truly has co-occurrence structure.

Never silently turn IDs, free text, dates, or continuous measurements into items. Do not mine direct identifiers or sensitive attributes unless their use is necessary, authorized, and safe to include in the report.

## Complete the analysis after fit is established

When the gate permits analysis, carry it through without making the user choose algorithm settings. Use the workflow in [analysis-protocol.md](references/analysis-protocol.md). It requires data-quality checks, transparent preprocessing, threshold selection based on usable counts, stability checks when feasible, and de-duplication of redundant rules.

Use appropriate local tools and libraries for the data format. Preserve a reproducible analysis artifact: source file(s), assumptions, transformation logic, software/library versions when available, and the code or commands needed to regenerate results. Keep raw sensitive data out of report folders and Git repositories.

If no rules survive sensible quality criteria, treat that as a result: report it, show the tested coverage and thresholds, and suggest what data or reframing would make the question answerable. Do not relax thresholds until attractive rules appear.

## Deliver a report people can use

Create a polished Markdown report and, when the environment supports it, a rendered HTML or PDF counterpart. Follow [report-blueprint.md](references/report-blueprint.md) exactly enough that every report includes its required sections, plain-language interpretation, and limitations. Put a concise executive answer first; put technical detail and the reproducibility record after it.

For every highlighted rule, translate `A → B` into a frequency comparison: how often B occurs among baskets containing A, how often it occurs overall, the number of supporting baskets, and why the result may or may not be operationally useful. Describe lift as an association relative to baseline, not an effect of changing A. Prefer a small set of stable, non-redundant rules over a long ranked dump.

End with prioritized next actions that distinguish a low-risk pilot from an observation, name an owner or decision context when known, and specify what outcome should be measured next. Include an explicit statement of whether the original consulting question was answered.

## Communication standard

Write the executive summary for a reader with no statistical background. Define each unavoidable term beside its first use, use counts as well as percentages, and make uncertainty visible. Preserve the user’s language in the report when practical. The technical appendix may be more formal, but must remain traceable to the data and decisions described above.

## Demonstrations

When the user is learning, presenting, or asks for a worked example, use the self-contained café dataset and walkthrough in [examples/README.md](examples/README.md). Identify it as synthetic teaching data, keep its results separate from real findings, and use it to demonstrate the consultation gate before showing rule metrics.
