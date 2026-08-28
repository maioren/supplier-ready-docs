# Resolve clarifications

## Turn an unknown condition into an explicit decision.

A clarification is planned when a requirement is conditional, its applicability is `UNKNOWN`, and there is an explicit condition to resolve.

> **When Supplier Ready does not know, it should not guess. It should ask.**

The current product journey presents pending clarification questions and accepts `YES` or `NO`: `YES → APPLICABLE`, `NO → NOT_APPLICABLE`.

Use `POST /v0/product/analyses/{analysis_id}/clarifications/{clarification_id}/answer` to answer within the integrated journey. The response returns the updated product analysis. When the last pending clarification is answered, its product state becomes `READY`—meaning interpretation has no pending clarification, not that customer requirements have been satisfied.

Repeating the same answer is idempotent; changing an already recorded answer produces `CLARIFICATION_CONFLICT`.

[Track Readiness →](track-readiness.md){ .md-button .md-button--primary }
