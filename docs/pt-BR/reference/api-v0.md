# API v0

## Contrato HTTP atualmente exposto pela aplicação.

A API `v0` documentada aqui corresponde às rotas realmente registradas na aplicação atual do Supplier Ready.

> **Se não existe rota registrada, não existe endpoint documentado.**

A aplicação se identifica como **Supplier Ready `0.1.0`** e registra hoje quatro superfícies HTTP relevantes para a `v0`: análises de baixo nível, esclarecimentos de baixo nível, jornada de produto e telemetria de funil.

---

## Visão geral

### Jornada de produto

| Método | Endpoint | Finalidade |
| --- | --- | --- |
| `POST` | `/v0/product/analyses` | Criar **e processar** uma análise em uma única operação. |
| `GET` | `/v0/product/analyses/{analysis_id}` | Consultar o resultado processado da jornada de produto. |
| `POST` | `/v0/product/analyses/{analysis_id}/clarifications/{clarification_id}/answer` | Responder um esclarecimento e receber o resultado atualizado. |

### Contratos de baixo nível

| Método | Endpoint | Finalidade |
| --- | --- | --- |
| `POST` | `/v0/analyses` | Criar uma análise sem executar o Interpreter. |
| `POST` | `/v0/analyses/{analysis_id}/clarifications/plan` | Planejar esclarecimentos a partir de um `InterpreterResult` fornecido pelo cliente da API. |
| `GET` | `/v0/analyses/{analysis_id}/clarifications` | Listar esclarecimentos planejados. |
| `POST` | `/v0/analyses/{analysis_id}/clarifications/{clarification_id}/answer` | Responder um esclarecimento. |

### Telemetria

| Método | Endpoint | Finalidade |
| --- | --- | --- |
| `POST` | `/v0/telemetry/funnel` | Registrar um evento do funil de uso. |

!!! note "Duas superfícies de análise"
    `/v0/analyses` representa o contrato de baixo nível: cria e registra a fonte. Já `/v0/product/analyses` executa a jornada integrada atual: cria a análise, processa o texto pelo Interpreter e retorna uma visão pronta para a experiência de produto.

---

# Jornada de produto

## `POST /v0/product/analyses`

Cria a análise, executa o Requirement Interpreter, planeja os esclarecimentos necessários, resolve a rastreabilidade dos requisitos na fonte e devolve o resultado da jornada em uma única chamada.

### Request

```json
{
  "cnpj": "12.345.678/0001-XX",
  "requirements_text": "Texto das exigências recebidas do cliente"
}
```

| Campo | Tipo | Obrigatório | Regra |
| --- | --- | :---: | --- |
| `cnpj` | `string` | sim | CNPJ válido com 14 dígitos ou máscara padrão. |
| `requirements_text` | `string` | sim | Texto não vazio e dentro do limite configurado da fonte. |

O modelo rejeita campos extras.

### Response — `201 Created`

Retorna `ProductAnalysisResultResponse`:

```json
{
  "analysis_id": "<uuid>",
  "cnpj": "<cnpj-normalizado>",
  "state": "NEEDS_CLARIFICATION",
  "requirements": [
    {
      "temp_id": "req-1",
      "name": "Registro no conselho profissional",
      "category": "LICENSING",
      "type": "DOCUMENT",
      "applicability": "UNKNOWN",
      "condition": "quando aplicável",
      "source_quote": "quando aplicável, registro no conselho profissional competente",
      "source_start": 120,
      "source_end": 184
    }
  ],
  "uncertainties": [],
  "pending_clarifications": []
}
```

Os valores acima são apenas ilustrativos.

### `ProductAnalysisResultResponse`

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `analysis_id` | `UUID` | Identificador da análise. |
| `cnpj` | `string` | CNPJ normalizado. |
| `state` | `ProductAnalysisState` | Estado da jornada de produto. |
| `requirements` | `array<RequirementView>` | Requisitos interpretados na visão exposta ao produto. |
| `uncertainties` | `array<UncertaintyView>` | Incertezas estruturadas da interpretação. |
| `pending_clarifications` | `array<ClarificationQuestion>` | Apenas esclarecimentos ainda sem resposta. |

### `RequirementView`

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `temp_id` | `string` | Identificador temporário do requisito. |
| `name` | `string` | Nome interpretado. |
| `category` | `RequirementCategory` | Categoria do requisito. |
| `type` | `RequirementType` | Tipo do requisito. |
| `applicability` | `Applicability` | Aplicabilidade atual. |
| `condition` | `string \| null` | Condição, quando existente. |
| `source_quote` | `string` | Trecho da fonte usado na interpretação. |
| `source_start` | `int` | Índice inicial de `source_quote` no texto original. |
| `source_end` | `int` | Índice final exclusivo de `source_quote` no texto original. |

A visão de produto é deliberadamente menor que o `RequirementCandidate` completo. Campos internos como `confidence`, `mandatory`, `blocking`, `canonical_name` e `issuer` não fazem parte de `RequirementView` neste contrato.

### `UncertaintyView`

| Campo | Tipo |
| --- | --- |
| `reason` | `UncertaintyReason` |
| `message` | `string` |
| `source_quote` | `string` |
| `requirement_temp_id` | `string \| null` |

### `ProductAnalysisState`

Valores atuais:

```text
NEEDS_CLARIFICATION
READY
```

A regra é objetiva:

```text
existe pelo menos um esclarecimento sem resposta
→ NEEDS_CLARIFICATION

não existe esclarecimento pendente
→ READY
```

!!! warning "`READY` aqui não é a readiness do produto"
    `ProductAnalysisState.READY` significa apenas que a **etapa atual de interpretação não possui esclarecimentos pendentes**. Ele não resulta do `ReadinessCalculator`, não mede atendimento dos requisitos e não significa que a empresa esteja pronta para o cliente no sentido conceitual de **Ready**.

### Erros estruturados conhecidos

| HTTP | Código | Condição |
| ---: | --- | --- |
| `422` | `INVALID_CNPJ` | CNPJ inválido. |
| `422` | `EMPTY_REQUIREMENTS` | Texto sem conteúdo significativo. |
| `413` | `SOURCE_TOO_LARGE` | Fonte acima do limite configurado. |
| `502` | `INTERPRETER_FAILED` | O Interpreter ou seu provedor não conseguiu produzir um resultado válido. |

---

## `GET /v0/product/analyses/{analysis_id}`

Retorna a mesma estrutura `ProductAnalysisResultResponse` para uma análise já processada.

### Path parameter

| Parâmetro | Tipo |
| --- | --- |
| `analysis_id` | `UUID` |

### Response — `200 OK`

```text
ProductAnalysisResultResponse
```

### Erros estruturados conhecidos

| HTTP | Código | Condição |
| ---: | --- | --- |
| `404` | `ANALYSIS_NOT_FOUND` | A análise não existe. |
| `409` | `ANALYSIS_NOT_PROCESSED` | A análise existe, mas ainda não possui resultado do Interpreter. |

---

## `POST /v0/product/analyses/{analysis_id}/clarifications/{clarification_id}/answer`

Responde um esclarecimento da jornada de produto e devolve imediatamente o `ProductAnalysisResultResponse` atualizado.

### Request

```json
{
  "answer": "YES"
}
```

Valores aceitos:

```text
YES
NO
```

Efeito atual:

```text
YES → APPLICABLE
NO  → NOT_APPLICABLE
```

Depois da resposta, a aplicabilidade do requisito correspondente é atualizada no resultado processado da análise.

### Response — `200 OK`

```text
ProductAnalysisResultResponse
```

Se aquela era a última pergunta pendente, `state` passa de `NEEDS_CLARIFICATION` para `READY`.

### Idempotência

Repetir a mesma resposta é válido. Enviar posteriormente uma resposta diferente gera conflito.

### Erros estruturados conhecidos

| HTTP | Código | Condição |
| ---: | --- | --- |
| `404` | `ANALYSIS_NOT_FOUND` | A análise não existe. |
| `409` | `ANALYSIS_NOT_PROCESSED` | A análise ainda não possui resultado interpretado. |
| `404` | `CLARIFICATION_NOT_FOUND` | O esclarecimento não pertence à análise ou não existe. |
| `409` | `CLARIFICATION_CONFLICT` | Já existe resposta diferente para o esclarecimento. |

---

# Contratos de baixo nível

## `POST /v0/analyses`

Cria e armazena uma análise, mas **não executa o Interpreter**.

### Request

```json
{
  "cnpj": "12.345.678/0001-XX",
  "requirements_text": "Texto das exigências recebidas do cliente"
}
```

### Response — `201 Created`

```json
{
  "analysis_id": "<uuid>",
  "cnpj": "<cnpj-normalizado>",
  "status": "RECEIVED"
}
```

O CNPJ aceita 14 dígitos ou máscara padrão, precisa ser válido e é devolvido normalizado.

### Erros estruturados conhecidos

| HTTP | Código |
| ---: | --- |
| `422` | `INVALID_CNPJ` |
| `422` | `EMPTY_REQUIREMENTS` |
| `413` | `SOURCE_TOO_LARGE` |

---

## `POST /v0/analyses/{analysis_id}/clarifications/plan`

Planeja perguntas de esclarecimento a partir de um `InterpreterResultInput` fornecido explicitamente no request.

Este é um contrato de baixo nível. A jornada `/v0/product/analyses` já faz o planejamento internamente depois de executar o Interpreter.

Uma pergunta é criada quando todas as condições abaixo são verdadeiras:

```text
conditional = true
applicability = UNKNOWN
condition contém texto
não existe pergunta já planejada para requirement_temp_id
```

### Response — `200 OK`

```text
array<ClarificationQuestion>
```

### Erro estruturado conhecido

| HTTP | Código |
| ---: | --- |
| `404` | `ANALYSIS_NOT_FOUND` |

---

## `GET /v0/analyses/{analysis_id}/clarifications`

Lista todas as perguntas planejadas para a análise, incluindo perguntas já respondidas.

### Response — `200 OK`

```text
array<ClarificationQuestion>
```

### Erro estruturado conhecido

| HTTP | Código |
| ---: | --- |
| `404` | `ANALYSIS_NOT_FOUND` |

---

## `POST /v0/analyses/{analysis_id}/clarifications/{clarification_id}/answer`

Responde diretamente uma pergunta de esclarecimento.

### Request

```json
{
  "answer": "YES"
}
```

### Response — `200 OK`

Retorna `ClarificationAnswerResult`:

```json
{
  "clarification": {
    "id": "<uuid>",
    "analysis_id": "<uuid>",
    "requirement_temp_id": "req-1",
    "condition": "quando aplicável",
    "question": "A condição se aplica ao fornecedor? quando aplicável",
    "answer": "YES",
    "resolved_applicability": "APPLICABLE"
  },
  "applicability": "APPLICABLE"
}
```

### Erros estruturados conhecidos

| HTTP | Código |
| ---: | --- |
| `404` | `ANALYSIS_NOT_FOUND` |
| `404` | `CLARIFICATION_NOT_FOUND` |
| `409` | `CLARIFICATION_CONFLICT` |

!!! note "Diferença para a jornada de produto"
    Neste endpoint de baixo nível, o serviço de esclarecimentos devolve a aplicabilidade resolvida. Na jornada `/v0/product/...`, o orchestrator também atualiza o requisito dentro do `InterpreterResult` armazenado e devolve a visão completa do produto.

---

# Telemetria de funil

## `POST /v0/telemetry/funnel`

Registra um evento de uso no funil atual.

### Request

```json
{
  "name": "analysis_started",
  "session_id": "<uuid>",
  "analysis_id": null
}
```

| Campo | Tipo | Obrigatório |
| --- | --- | :---: |
| `name` | `FunnelEventName` | sim |
| `session_id` | `UUID` | sim |
| `analysis_id` | `UUID \| null` | não |

O modelo rejeita campos extras.

### `FunnelEventName`

Valores aceitos atualmente:

```text
landing_viewed
analysis_started
requirement_submitted
analysis_completed
result_viewed
requirement_expanded
```

### Response — `204 No Content`

A resposta não possui body.

!!! note "Persistência atual"
    A telemetria de funil é armazenada em memória na implementação atual.

---

# Formato dos erros estruturados

`ApplicationError` é serializado como:

```json
{
  "error": {
    "code": "INVALID_CNPJ",
    "message": "CNPJ must be valid and use either 14 digits or the standard mask.",
    "details": {}
  }
}
```

Para o catálogo completo, consulte [Erros](errors.md).

Erros de validação gerados diretamente pelo FastAPI/Pydantic podem usar o formato padrão do framework em vez desse envelope.

---

# Autenticação

Os routers registrados atualmente não adicionam mecanismo de autenticação ou autorização.

Isso descreve o estado presente da `v0` e **não representa uma decisão de segurança para uma API pública de produção**.

---

# Persistência atual

Análises, esclarecimentos, resultados processados e telemetria de funil são mantidos atualmente em memória pelos serviços da aplicação.

Reiniciar o processo pode eliminar esse estado. A `v0` atual valida o fluxo funcional; não define a arquitetura final de persistência.

---

# O que ainda não possui endpoint dedicado

Apesar de algumas capacidades participarem internamente da jornada de produto, não existe hoje endpoint HTTP dedicado para:

- calcular ou consultar `ReadinessResult`;
- gerar `AnalysisSummary`;
- consultar o conjunto completo de source traces como recurso próprio;
- consultar `TruthProjection`.

O Interpreter também não possui uma rota isolada: sua execução é exposta **indiretamente** por `POST /v0/product/analyses`.

---

## Regra desta referência

> **A documentação acompanha as rotas registradas na aplicação, não apenas as classes disponíveis internamente.**

[Consultar Erros](errors.md){ .md-button .md-button--primary }
[Consultar Estados e enums](states-enums.md){ .md-button }
