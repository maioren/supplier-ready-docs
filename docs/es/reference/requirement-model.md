# Modelo de requisito

## Estructura actual de un requisito interpretado.

El Interpreter representa cada requisito como `RequirementCandidate`.

| Campo | Tipo | Nulo | Regla actual |
| --- | --- | :---: | --- |
| `temp_id` | string | no | Identificador temporal. |
| `name` | string | no | Nombre interpretado. |
| `canonical_name` | string | sí | Nombre canónico cuando existe. |
| `category` | `RequirementCategory` | no | Categoría semántica. |
| `type` | `RequirementType` | no | Tipo estructural. |
| `mandatory` | boolean | no | Si la fuente lo establece como obligatorio. |
| `blocking` | boolean | sí | Indicación de bloqueo cuando puede determinarse. |
| `conditional` | boolean | no | Si depende de una condición. |
| `condition` | string | sí | Texto de la condición. |
| `applicability` | `Applicability` | no | `APPLICABLE`, `NOT_APPLICABLE` o `UNKNOWN`. |
| `issuer` | string | sí | Emisor/entidad cuando es identificable. |
| `source_quote` | string | no | Fragmento no vacío que sustenta la interpretación. |
| `confidence` | float | no | Entre 0.0 y 1.0 inclusive. |

Invariante: `conditional = true` exige `condition` no vacío; `conditional = false` exige `condition = null`.

El modelo usa validación estricta y rechaza campos extra. `source_quote` es obligatorio para trazabilidad; la confianza no reemplaza la evidencia ni representa probabilidad de aprobación.

`RequirementView` de la API de producto es deliberadamente menor que este modelo de dominio.

[Estados y enums](states-enums.md){ .md-button }
