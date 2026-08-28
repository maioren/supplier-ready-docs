# Revisar requisitos interpretados

## Verifique lo entendido antes de usarlo para tomar decisiones.

La jornada actual ya expone requisitos interpretados después de procesar la fuente. Revise nombre, categoría, tipo, aplicabilidad, condición y trazabilidad presentada por la respuesta de producto.

!!! info "Disponible en el MVP"
    El Interpreter produce un modelo de dominio más rico, mientras `/v0/product/analyses` expone el subconjunto necesario para la experiencia actual, incluidos los offsets exactos de la fuente.

Compruebe siempre `source_quote` contra la fuente original. La aplicabilidad `UNKNOWN` es válida y debe mantenerse sin resolver hasta contar con contexto suficiente. El modelo completo también puede contener confianza, obligatoriedad/bloqueo, nombre canónico, emisor, incertidumbres, aclaraciones y avisos; no todos esos campos aparecen en `RequirementView`.

[Resolver aclaraciones →](resolve-clarifications.md){ .md-button .md-button--primary }
