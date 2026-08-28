# States and enums

## Closed values in the current contract.

This page lists the current Supplier Ready `v0` domain and product-API enums. Values are shown exactly as they appear in the contract.

## Analysis

`AnalysisStatus`: `RECEIVED`.

`RequirementSourceType`: `TEXT`.

## Product journey state

`ProductAnalysisState`: `NEEDS_CLARIFICATION`, `READY`.

!!! warning "`READY` is not Readiness"
    `ProductAnalysisState.READY` only means there is no pending interpretation clarification. It is not produced by the readiness calculation and does not state that the company satisfies every customer requirement.

## Requirements

`RequirementCategory`: `CORPORATE`, `TAX`, `LABOR`, `FINANCIAL`, `TECHNICAL`, `LICENSING`, `BANKING`, `COMPLIANCE`, `DECLARATION`, `IDENTITY`, `OTHER`.

`RequirementType`: `DOCUMENT`, `DATA`, `DECLARATION`, `CERTIFICATION`, `POLICY`, `ACCEPTANCE`, `CAPABILITY`, `OTHER`.

## Applicability

`Applicability`: `APPLICABLE`, `NOT_APPLICABLE`, `UNKNOWN`.

## Interpretation uncertainty

`UncertaintyReason`: `AMBIGUOUS`, `MISSING_CONTEXT`, `UNSUPPORTED_DETAIL`, `OTHER`.

## Clarifications

`ClarificationAnswer`: `YES` → `APPLICABLE`; `NO` → `NOT_APPLICABLE`.

## Requirement assessment

`AssessmentStatus`: `SATISFIED` (1.0), `PARTIAL` (0.5), `MISSING` (0.0), `UNKNOWN` (0.0), `NOT_APPLICABLE` (excluded).

## Funnel telemetry

`FunnelEventName`: `landing_viewed`, `analysis_started`, `requirement_submitted`, `analysis_completed`, `result_viewed`, `requirement_expanded`.

A final domain `Ready` state, formal gap states, and source types such as PDF, spreadsheet or email are not part of the current contract.

[API v0](api-v0.md){ .md-button }
