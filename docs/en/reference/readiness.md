# Readiness

## Deterministic contract of the current calculation.

Input is a list of `RequirementAssessment` objects with `requirement_temp_id`, `status`, and `applicability`. The model is strict and rejects extra fields.

Weights: `SATISFIED = 1.0`, `PARTIAL = 0.5`, `MISSING = 0.0`, `UNKNOWN = 0.0`. `NOT_APPLICABLE` items are excluded.

Classification order is significant: status `NOT_APPLICABLE` → exclude; applicability `NOT_APPLICABLE` → exclude; applicability `UNKNOWN` → pending; otherwise the item is scoreable.

When at least one item is scoreable:

`score = weighted_total / scoreable_count × 100`

When `scoreable_count = 0`, `score = null`.

`ReadinessResult` contains `score`, `scoreable_count`, `pending_applicability_count`, `excluded_not_applicable_count`, `satisfied_count`, `partial_count`, `missing_count`, and `unknown_count`.

The calculation is deterministic, has no explicit rounding rule, and currently has no per-requirement weighting. `ReadinessResult` does not contain a final `ready` field.

!!! note "Different from product API READY"
    `ProductAnalysisState.READY` belongs to the interpretation journey and only means no clarification is pending.

[States and enums](states-enums.md){ .md-button }
