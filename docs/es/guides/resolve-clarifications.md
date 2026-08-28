# Resolver aclaraciones

## Convierta una condición desconocida en una decisión explícita.

Se planifica una aclaración cuando un requisito es condicional, su aplicabilidad es `UNKNOWN` y existe una condición explícita que resolver.

> **Cuando Supplier Ready no sabe, no debe adivinar. Debe preguntar.**

La jornada actual presenta preguntas pendientes y acepta `YES` o `NO`: `YES → APPLICABLE`, `NO → NOT_APPLICABLE`.

Use `POST /v0/product/analyses/{analysis_id}/clarifications/{clarification_id}/answer`. La respuesta devuelve el análisis actualizado. Al resolver la última aclaración, el estado de producto pasa a `READY`: significa que la interpretación no tiene aclaraciones pendientes, no que todas las exigencias estén cumplidas.

Repetir la misma respuesta es idempotente; cambiar una respuesta ya registrada produce `CLARIFICATION_CONFLICT`.

[Acompañar Readiness →](track-readiness.md){ .md-button .md-button--primary }
