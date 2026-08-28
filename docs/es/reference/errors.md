# Errores

## Contrato actual de errores de la API `v0`.

Los errores de dominio/aplicación de Supplier Ready usan:

```json
{"error":{"code":"INVALID_CNPJ","message":"...","details":{}}}
```

Códigos estructurados actuales: `SOURCE_TOO_LARGE` (413), `INVALID_CNPJ` (422), `EMPTY_REQUIREMENTS` (422), `ANALYSIS_NOT_FOUND` (404), `ANALYSIS_NOT_PROCESSED` (409), `CLARIFICATION_NOT_FOUND` (404), `CLARIFICATION_CONFLICT` (409) e `INTERPRETER_FAILED` (502).

`CLARIFICATION_CONFLICT` ocurre cuando una aclaración ya respondida recibe la respuesta opuesta; repetir la misma respuesta es idempotente. `INTERPRETER_FAILED` cubre una falla del proveedor o la imposibilidad de producir un resultado estructurado válido después del intento de reparación del motor.

No todo HTTP 422 usa este envelope. La validación de schema de FastAPI/Pydantic puede devolver el formato estándar del framework. Una ruta inexistente también puede devolver el 404 estándar de FastAPI.

Para tratamiento programático, prefiera `HTTP status + error.code`; use `error.message` para presentación o diagnóstico, no como clave de lógica de negocio.

> **Un código entra en esta referencia solamente cuando existe en el contrato implementado.**

[API v0](api-v0.md){ .md-button .md-button--primary }
