# Readiness

## Contrato determinístico del cálculo actual.

La entrada es una lista de `RequirementAssessment` con `requirement_temp_id`, `status` y `applicability`. El modelo es estricto y rechaza campos extra.

Pesos: `SATISFIED = 1.0`, `PARTIAL = 0.5`, `MISSING = 0.0`, `UNKNOWN = 0.0`. Los elementos `NOT_APPLICABLE` se excluyen.

El orden importa: status `NOT_APPLICABLE` → excluir; aplicabilidad `NOT_APPLICABLE` → excluir; aplicabilidad `UNKNOWN` → pendiente; los demás elementos son evaluables.

Con al menos un elemento evaluable:

`score = weighted_total / scoreable_count × 100`

Si `scoreable_count = 0`, `score = null`.

`ReadinessResult` contiene `score`, `scoreable_count`, `pending_applicability_count`, `excluded_not_applicable_count`, `satisfied_count`, `partial_count`, `missing_count` y `unknown_count`.

El cálculo es determinístico, no tiene regla explícita de redondeo ni pesos adicionales por requisito. `ReadinessResult` no contiene un campo final `ready`.

!!! note "Diferente del READY de la API de producto"
    `ProductAnalysisState.READY` pertenece a la jornada de interpretación y solo significa que no hay aclaraciones pendientes.

[Estados y enums](states-enums.md){ .md-button }
