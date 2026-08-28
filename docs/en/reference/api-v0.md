# API v0

## HTTP contract currently exposed by the application.

> **If there is no registered route, there is no documented endpoint.**

The current `v0` exposes an integrated product journey, lower-level analysis/clarification contracts, and funnel telemetry.

## Product journey

| Method | Endpoint | Purpose |
| --- | --- | --- |
| POST | `/v0/product/analyses` | Create and process an analysis. |
| GET | `/v0/product/analyses/{analysis_id}` | Retrieve a processed product result. |
| POST | `/v0/product/analyses/{analysis_id}/clarifications/{clarification_id}/answer` | Answer a clarification and return the updated result. |

`POST /v0/product/analyses` receives `cnpj` and `requirements_text`, runs the Interpreter, plans clarifications, resolves source traces, and returns `ProductAnalysisResultResponse` with `analysis_id`, normalized `cnpj`, `state`, `requirements`, `uncertainties`, and only unanswered `pending_clarifications`.

`RequirementView` exposes `temp_id`, `name`, `category`, `type`, `applicability`, nullable `condition`, `source_quote`, `source_start`, and exclusive `source_end`. It is intentionally smaller than the complete domain `RequirementCandidate`.

`ProductAnalysisState` is `NEEDS_CLARIFICATION` when at least one question is unanswered; otherwise it is `READY`.

!!! warning "Product API `READY` is not readiness"
    It only means the interpretation stage has no pending clarification. It is not calculated by `ReadinessCalculator` and does not mean the company satisfies all requirements.

## Lower-level contracts

| Method | Endpoint |
| --- | --- |
| POST | `/v0/analyses` |
| POST | `/v0/analyses/{analysis_id}/clarifications/plan` |
| GET | `/v0/analyses/{analysis_id}/clarifications` |
| POST | `/v0/analyses/{analysis_id}/clarifications/{clarification_id}/answer` |

`POST /v0/analyses` creates a `RECEIVED` record without running the Interpreter. The low-level clarification planning endpoint receives an explicit Interpreter result. Answers accept `YES` or `NO`; same-answer repetition is idempotent.

## Funnel telemetry

`POST /v0/telemetry/funnel` accepts `name`, `session_id`, and optional `analysis_id`, and returns `204 No Content`. Current event names are listed in [States and enums](states-enums.md). Funnel telemetry is currently stored in memory.

## Errors and persistence

Structured application errors use the Supplier Ready envelope documented in [Errors](errors.md); FastAPI/Pydantic validation errors can use the framework format. Current routers add no authentication/authorization mechanism. Analyses, clarifications, processed results, and funnel telemetry are currently in-memory state.

There is no dedicated HTTP endpoint yet for `ReadinessResult`, `AnalysisSummary`, the full source-trace collection, or `TruthProjection`. The Interpreter has no isolated route; it is invoked indirectly by `POST /v0/product/analyses`.

> **Reference describes the implemented `v0` contract, not future intent.**
