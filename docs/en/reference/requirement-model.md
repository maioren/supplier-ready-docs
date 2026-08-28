# Requirement model

## Current structure of an interpreted requirement.

The Interpreter represents each identified requirement as a `RequirementCandidate`.

| Field | Type | Nullable | Current rule |
| --- | --- | :---: | --- |
| `temp_id` | string | no | Temporary identifier. |
| `name` | string | no | Interpreted name. |
| `canonical_name` | string | yes | Canonical name when available. |
| `category` | `RequirementCategory` | no | Semantic category. |
| `type` | `RequirementType` | no | Structural type. |
| `mandatory` | boolean | no | Whether the source establishes it as mandatory. |
| `blocking` | boolean | yes | Blocking indication when determinable. |
| `conditional` | boolean | no | Whether it depends on a condition. |
| `condition` | string | yes | Condition text. |
| `applicability` | `Applicability` | no | `APPLICABLE`, `NOT_APPLICABLE`, or `UNKNOWN`. |
| `issuer` | string | yes | Issuer/entity when identifiable. |
| `source_quote` | string | no | Non-empty supporting source excerpt. |
| `confidence` | float | no | Between 0.0 and 1.0 inclusive. |

Invariant: `conditional = true` requires non-empty `condition`; `conditional = false` requires `condition = null`.

The model uses strict validation and rejects extra fields. `source_quote` is required for traceability; confidence never replaces source evidence and is not a probability of customer approval.

The product API's `RequirementView` is intentionally smaller than this domain model.

[States and enums](states-enums.md){ .md-button }
