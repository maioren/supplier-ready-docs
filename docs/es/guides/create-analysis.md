# Crear un análisis

## Registre las exigencias que necesita entender.

Un **análisis** es el punto de partida para trabajar con las exigencias de un cliente en Supplier Ready. Crearlo registra la empresa analizada y la fuente textual recibida del cliente.

> **Crear un análisis registra el problema que queremos resolver. Todavía no es la interpretación.**

!!! info "Disponible en el MVP"
    La jornada actual del producto acepta un CNPJ y exigencias textuales, crea el análisis y lo procesa con el Interpreter. La API de bajo nivel también puede crear solamente el registro `RECEIVED`.

Actualmente la fuente soportada es `TEXT`; la carga directa de PDF, planillas o correos todavía no forma parte de esta etapa.

`POST /v0/product/analyses` crea y procesa el análisis. Puede devolver `NEEDS_CLARIFICATION` o `READY` como estado de la jornada de interpretación.

!!! warning "`READY` tiene aquí un significado restringido"
    Solo significa que no hay aclaraciones de interpretación pendientes. No es el score de readiness ni significa que la empresa ya cumple todas las exigencias.

`POST /v0/analyses` crea únicamente el registro de bajo nivel con estado `RECEIVED`. Entradas inválidas pueden producir `INVALID_CNPJ`, `EMPTY_REQUIREMENTS` o `SOURCE_TOO_LARGE`.

[Revisar requisitos interpretados →](review-interpreted-requirements.md){ .md-button .md-button--primary }
