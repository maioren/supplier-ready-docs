# Erros

## Contrato de erro atual da API `v0`.

Esta página descreve os erros estruturados que o Supplier Ready expõe atualmente por meio de `ApplicationError`, além de separar esses erros dos erros de validação gerados pelo FastAPI/Pydantic.

---

## Envelope de erro do Supplier Ready

Erros de domínio e aplicação usam este formato:

```json
{
  "error": {
    "code": "INVALID_CNPJ",
    "message": "CNPJ must be valid and use either 14 digits or the standard mask.",
    "details": {}
  }
}
```

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `error.code` | `string` | Código estável para tratamento programático. |
| `error.message` | `string` | Mensagem humana associada ao erro. |
| `error.details` | `object` | Informações adicionais; vazio quando não existem detalhes. |

O status HTTP faz parte do erro e é retornado como status da resposta.

---

## Catálogo atual

| HTTP | Código | Quando ocorre |
| ---: | --- | --- |
| `413` | `SOURCE_TOO_LARGE` | O texto das exigências excede o limite configurado para a fonte. |
| `422` | `INVALID_CNPJ` | O CNPJ não é válido ou não usa um dos formatos aceitos. |
| `422` | `EMPTY_REQUIREMENTS` | O texto das exigências está vazio ou contém apenas espaços. |
| `404` | `ANALYSIS_NOT_FOUND` | A análise solicitada não existe no armazenamento atual. |
| `409` | `ANALYSIS_NOT_PROCESSED` | A análise existe, mas ainda não possui resultado do Interpreter. |
| `404` | `CLARIFICATION_NOT_FOUND` | O esclarecimento não existe para a análise informada. |
| `409` | `CLARIFICATION_CONFLICT` | Um esclarecimento já foi respondido e uma resposta diferente foi enviada. |
| `502` | `INTERPRETER_FAILED` | O Interpreter não conseguiu produzir um resultado estruturado válido ou o provedor de IA falhou durante a interpretação. |

---

## `INVALID_CNPJ`

### HTTP `422 Unprocessable Entity`

Ocorre quando o CNPJ informado:

- não possui 14 dígitos nem a máscara padrão aceita;
- possui dígitos verificadores inválidos;
- é formado pela repetição do mesmo dígito.

Exemplo:

```json
{
  "error": {
    "code": "INVALID_CNPJ",
    "message": "CNPJ must be valid and use either 14 digits or the standard mask.",
    "details": {}
  }
}
```

---

## `EMPTY_REQUIREMENTS`

### HTTP `422 Unprocessable Entity`

Ocorre quando `requirements_text` não contém conteúdo significativo.

Exemplo:

```json
{
  "error": {
    "code": "EMPTY_REQUIREMENTS",
    "message": "Requirements text must contain meaningful content.",
    "details": {}
  }
}
```

---

## `SOURCE_TOO_LARGE`

### HTTP `413 Content Too Large`

Ocorre quando o tamanho de `requirements_text` excede o limite configurado no ambiente.

A medição atual usa a quantidade de caracteres Unicode do texto.

`details` informa o limite e o tamanho recebido:

```json
{
  "error": {
    "code": "SOURCE_TOO_LARGE",
    "message": "Requirements text exceeds the configured source size limit.",
    "details": {
      "max_chars": 10000,
      "actual_chars": 12000
    }
  }
}
```

!!! note "Valores ilustrativos"
    `max_chars` depende da configuração do ambiente. Os números do exemplo não definem um limite fixo da API.

---

## `ANALYSIS_NOT_FOUND`

### HTTP `404 Not Found`

Ocorre quando uma operação depende de uma análise existente e o `analysis_id` informado não pode ser encontrado.

Exemplo:

```json
{
  "error": {
    "code": "ANALYSIS_NOT_FOUND",
    "message": "Analysis was not found.",
    "details": {}
  }
}
```

---

## `ANALYSIS_NOT_PROCESSED`

### HTTP `409 Conflict`

Ocorre quando a análise existe, mas ainda não foi processada pelo Requirement Interpreter e uma operação tenta acessar seu resultado interpretado.

Exemplo:

```json
{
  "error": {
    "code": "ANALYSIS_NOT_PROCESSED",
    "message": "Analysis has not been processed by the requirement interpreter.",
    "details": {}
  }
}
```

Esse erro representa uma diferença de estado: a análise existe, mas o recurso solicitado ainda não está disponível para ela.

---

## `CLARIFICATION_NOT_FOUND`

### HTTP `404 Not Found`

Ocorre quando o `clarification_id` não identifica uma pergunta existente dentro da análise informada.

Exemplo:

```json
{
  "error": {
    "code": "CLARIFICATION_NOT_FOUND",
    "message": "Clarification was not found for this analysis.",
    "details": {}
  }
}
```

---

## `CLARIFICATION_CONFLICT`

### HTTP `409 Conflict`

Uma resposta de esclarecimento é idempotente quando o mesmo valor é enviado novamente.

```text
YES → YES
NO  → NO
```

Porém, se o esclarecimento já foi respondido e uma resposta diferente é enviada depois, a API retorna `CLARIFICATION_CONFLICT`.

```text
YES → NO
NO  → YES
```

Exemplo:

```json
{
  "error": {
    "code": "CLARIFICATION_CONFLICT",
    "message": "Clarification was already answered with a different value.",
    "details": {}
  }
}
```

---

## `INTERPRETER_FAILED`

### HTTP `502 Bad Gateway`

Ocorre quando a etapa de interpretação não consegue produzir um `InterpreterResult` válido.

O código cobre atualmente dois grupos de falha:

1. o provedor de IA falha durante a execução;
2. o resultado produzido não respeita o contrato estrutural ou as invariantes do Interpreter mesmo após a tentativa de correção prevista pelo motor.

Exemplo:

```json
{
  "error": {
    "code": "INTERPRETER_FAILED",
    "message": "Requirement interpreter could not produce valid structured output.",
    "details": {}
  }
}
```

ou, em falha do provedor:

```json
{
  "error": {
    "code": "INTERPRETER_FAILED",
    "message": "Requirement interpreter provider failed.",
    "details": {}
  }
}
```

O mesmo `code` pode, portanto, possuir mensagens diferentes conforme a origem da falha.

---

## Erros de validação do FastAPI/Pydantic

Nem todo HTTP `422` é um `ApplicationError` do Supplier Ready.

Quando o request não respeita o schema HTTP — por exemplo:

- UUID inválido no path;
- enum com valor não reconhecido;
- campo obrigatório ausente;
- tipo incompatível;
- campo extra em modelos configurados com `extra="forbid"`;
- `confidence` fora do intervalo aceito;

— a validação ocorre antes da lógica de domínio e o FastAPI/Pydantic retorna seu formato padrão de erro.

Esse tipo de resposta **não usa necessariamente** o envelope:

```json
{
  "error": {
    "code": "..."
  }
}
```

Portanto, consumidores da `v0` devem distinguir:

```text
ApplicationError do Supplier Ready
→ error.code + error.message + error.details

Erro de validação do framework
→ contrato padrão de validação do FastAPI/Pydantic
```

---

## Outros erros HTTP

### `404` de rota

Uma URL que não corresponde a uma rota registrada pode receber o `404` padrão do FastAPI, sem um `error.code` do Supplier Ready.

### Falhas internas não convertidas em `ApplicationError`

O handler customizado só transforma instâncias de `ApplicationError` no envelope documentado nesta página.

Falhas inesperadas de infraestrutura, configuração ou programação que não sejam convertidas explicitamente em `ApplicationError` não possuem, nesta `v0`, garantia de usar esse mesmo contrato.

---

## Como tratar erros programaticamente

Para erros que usam o envelope do Supplier Ready, prefira tomar decisões com base em:

```text
HTTP status + error.code
```

Use `error.message` para apresentação ou diagnóstico, não como chave de lógica de negócio.

Por exemplo:

```text
409 + CLARIFICATION_CONFLICT
```

é um contrato mais estável para tratamento do que comparar o texto completo da mensagem.

---

## Regra para a referência de erros

> **Um código só entra nesta página quando existe no contrato implementado.**

Novos códigos devem ser documentados junto com a mudança que os torna observáveis na `v0`.

[Consultar API v0](api-v0.md){ .md-button .md-button--primary }
[Voltar para Referência](index.md){ .md-button }
