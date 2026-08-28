# Estados y enums

## Valores cerrados del contrato actual.

Esta página lista los enums actuales del dominio y de la API de producto de Supplier Ready `v0`. Los valores aparecen exactamente como en el contrato.

## Análisis

`AnalysisStatus`: `RECEIVED`.

`RequirementSourceType`: `TEXT`.

## Estado de la jornada de producto

`ProductAnalysisState`: `NEEDS_CLARIFICATION`, `READY`.

!!! warning "`READY` no es Readiness"
    `ProductAnalysisState.READY` solo significa que no hay aclaraciones de interpretación pendientes. No proviene del cálculo de readiness ni afirma que la empresa cumple todas las exigencias.

## Requisitos

`RequirementCategory`: `CORPORATE`, `TAX`, `LABOR`, `FINANCIAL`, `TECHNICAL`, `LICENSING`, `BANKING`, `COMPLIANCE`, `DECLARATION`, `IDENTITY`, `OTHER`.

`RequirementType`: `DOCUMENT`, `DATA`, `DECLARATION`, `CERTIFICATION`, `POLICY`, `ACCEPTANCE`, `CAPABILITY`, `OTHER`.

## Aplicabilidad

`Applicability`: `APPLICABLE`, `NOT_APPLICABLE`, `UNKNOWN`.

## Incertidumbre

`UncertaintyReason`: `AMBIGUOUS`, `MISSING_CONTEXT`, `UNSUPPORTED_DETAIL`, `OTHER`.

## Aclaraciones

`ClarificationAnswer`: `YES` → `APPLICABLE`; `NO` → `NOT_APPLICABLE`.

## Evaluación

`AssessmentStatus`: `SATISFIED` (1.0), `PARTIAL` (0.5), `MISSING` (0.0), `UNKNOWN` (0.0), `NOT_APPLICABLE` (excluido).

## Telemetría de funil

`FunnelEventName`: `landing_viewed`, `analysis_started`, `requirement_submitted`, `analysis_completed`, `result_viewed`, `requirement_expanded`.

Un estado final de dominio `Ready`, estados formales de gap y fuentes como PDF, planilla o correo no forman parte del contrato actual.

[API v0](api-v0.md){ .md-button }
