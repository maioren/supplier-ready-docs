# API v0

## Contrato HTTP expuesto actualmente por la aplicación.

> **Si no existe una ruta registrada, no existe un endpoint documentado.**

La `v0` actual expone una jornada integrada de producto, contratos de bajo nivel de análisis/aclaraciones y telemetría de funil.

## Jornada de producto

| Método | Endpoint | Finalidad |
| --- | --- | --- |
| POST | `/v0/product/analyses` | Crear y procesar un análisis. |
| GET | `/v0/product/analyses/{analysis_id}` | Consultar el resultado procesado. |
| POST | `/v0/product/analyses/{analysis_id}/clarifications/{clarification_id}/answer` | Responder una aclaración y devolver el resultado actualizado. |

`POST /v0/product/analyses` recibe `cnpj` y `requirements_text`, ejecuta el Interpreter, planifica aclaraciones, resuelve trazas de fuente y devuelve `ProductAnalysisResultResponse` con `analysis_id`, `cnpj` normalizado, `state`, `requirements`, `uncertainties` y solamente `pending_clarifications` sin respuesta.

`RequirementView` expone `temp_id`, `name`, `category`, `type`, `applicability`, `condition` nullable, `source_quote`, `source_start` y `source_end` exclusivo. Es deliberadamente menor que `RequirementCandidate`.

`ProductAnalysisState` es `NEEDS_CLARIFICATION` si existe una pregunta sin respuesta; de lo contrario es `READY`.

!!! warning "El `READY` de la API de producto no es readiness"
    Solo significa que la interpretación no tiene aclaraciones pendientes. No proviene de `ReadinessCalculator` ni significa que la empresa cumpla todas las exigencias.

## Contratos de bajo nivel

| Método | Endpoint |
| --- | --- |
| POST | `/v0/analyses` |
| POST | `/v0/analyses/{analysis_id}/clarifications/plan` |
| GET | `/v0/analyses/{analysis_id}/clarifications` |
| POST | `/v0/analyses/{analysis_id}/clarifications/{clarification_id}/answer` |

`POST /v0/analyses` crea un registro `RECEIVED` sin ejecutar el Interpreter. El endpoint de planificación recibe explícitamente un resultado del Interpreter. Las respuestas aceptan `YES` o `NO`; repetir la misma respuesta es idempotente.

## Telemetría de funil

`POST /v0/telemetry/funnel` acepta `name`, `session_id` y `analysis_id` opcional y devuelve `204 No Content`. Los eventos actuales están en [Estados y enums](states-enums.md). La telemetría se almacena actualmente en memoria.

## Errores y persistencia

Los errores estructurados usan el envelope documentado en [Errores](errors.md); la validación FastAPI/Pydantic puede usar el formato del framework. Los routers actuales no agregan autenticación/autorización. Análisis, aclaraciones, resultados y telemetría están actualmente en memoria.

Todavía no existe endpoint dedicado para `ReadinessResult`, `AnalysisSummary`, la colección completa de source traces o `TruthProjection`. El Interpreter no posee una ruta aislada; se ejecuta indirectamente mediante `POST /v0/product/analyses`.

> **Referencia describe el contrato `v0` implementado, no intención futura.**
