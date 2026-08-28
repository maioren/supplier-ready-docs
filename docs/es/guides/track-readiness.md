# Acompañar Readiness

## Use readiness para acompañar el progreso, no para predecir aprobación.

El cálculo es determinístico: `SATISFIED = 1.0`, `PARTIAL = 0.5`, `MISSING = 0.0` y evaluación `UNKNOWN = 0.0`. Los requisitos no aplicables se excluyen; aquellos con aplicabilidad desconocida quedan pendientes y fuera del denominador.

Si no existen requisitos evaluables, el score es `null`. Lea siempre el porcentaje junto con sus contadores y bloqueos restantes.

**80% de readiness no significa 80% de probabilidad de aprobación por el cliente.**

!!! info "Disponible en el motor del MVP"
    El cálculo existe en el motor, pero todavía no hay un endpoint HTTP dedicado ni una experiencia completa para acompañarlo.

!!! note "Ready final sigue en desarrollo"
    El motor de readiness no define un estado de dominio `Ready`. `ProductAnalysisState.READY` es distinto: solo indica que la jornada de interpretación no tiene aclaraciones pendientes.

[Entender Readiness como concepto](../concepts/readiness.md){ .md-button }
