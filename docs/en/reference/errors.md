# Errors

## Current `v0` API error contract.

Supplier Ready domain/application errors use:

```json
{"error":{"code":"INVALID_CNPJ","message":"...","details":{}}}
```

Current structured codes are: `SOURCE_TOO_LARGE` (413), `INVALID_CNPJ` (422), `EMPTY_REQUIREMENTS` (422), `ANALYSIS_NOT_FOUND` (404), `ANALYSIS_NOT_PROCESSED` (409), `CLARIFICATION_NOT_FOUND` (404), `CLARIFICATION_CONFLICT` (409), and `INTERPRETER_FAILED` (502).

`CLARIFICATION_CONFLICT` occurs when an already answered clarification receives the opposite answer; repeating the same answer is idempotent. `INTERPRETER_FAILED` covers provider failure or inability to produce a valid structured result after the engine's repair attempt.

Not every HTTP 422 uses this envelope. FastAPI/Pydantic request-schema validation—invalid UUIDs or enums, missing/extra fields, incompatible types, or out-of-range values—can return the framework's standard validation format. Unmatched routes can likewise return FastAPI's standard 404.

For programmatic handling, prefer `HTTP status + error.code`; use `error.message` for display or diagnostics, not as a business-logic key.

> **A code enters this reference only when it exists in the implemented contract.**

[API v0](api-v0.md){ .md-button .md-button--primary }
