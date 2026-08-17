# API v0

## Contrato HTTP atualmente exposto pela aplicação.

A API `v0` reúne os endpoints HTTP registrados hoje pelo Supplier Ready.

Esta referência descreve apenas rotas realmente incluídas na aplicação atual. Capacidades existentes internamente no domínio ou no orchestrator, mas que ainda não possuem rota HTTP registrada, ficam fora desta página.

!!! note "Estado atual"
    A aplicação se identifica como **Supplier Ready `0.1.0`** e registra atualmente os routers de `analyses` e `clarifications`.

---

## Visão geral

| Método | Endpoint | Finalidade |
| --- | --- | --- |
| `POST` | `/v0/analyses` | Criar uma análise. |
| `POST` | `/v0/analyses/{analysis_id}/clarifications/plan` | Planejar esclarecimentos a partir de um resultado do Interpreter. |
| `GET` | `/v0/analyses/{analysis_id}/clarifications` | Listar esclarecimentos de uma análise. |
| `POST` | `/v0/analyses/{analysis_id}/clarifications/{clarification_id}/answer` | Responder um esclarecimento. |

Não existem, no router HTTP atual, endpoints públicos para executar o Interpreter, calcular Readiness, gerar Summary, consultar Source Trace ou obter a Truth Projection.

---

# Análises

## `POST /v0/analyses`

Cria uma nova análise a partir do CNPJ da empresa e de uma fonte textual com as exigências.

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
| `requirements_text` | `string` | sim | Deve conter conteúdo significativo e respeitar o limite configurado da fonte. |

!!! warning "CNPJ ilustrativo"
    O CNPJ acima demonstra apenas o formato do payload. Uma requisição real precisa usar um CNPJ válido.

### Normalização do CNPJ

O serviço aceita:

```text
123456780001XX
```

ou:

```text
12.345.678/0001-XX
```

quando os dígitos representam um CNPJ válido.

A resposta utiliza a máscara padrão.

### Response — `201 Created`

```json
{
  "analysis_id": "<uuid>",
  "cnpj": "<cnpj-normalizado>",
  "status": "RECEIVED"
}
```

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `analysis_id` | `UUID` | Identificador criado para a análise. |
| `cnpj` | `string` | CNPJ normalizado. |
| `status` | `AnalysisStatus` | Estado inicial da análise. Atualmente `RECEIVED`. |

### Erros de domínio conhecidos

| HTTP | Código | Condição |
| ---: | --- | --- |
| `422` | `INVALID_CNPJ` | CNPJ inválido ou fora dos formatos aceitos. |
| `422` | `EMPTY_REQUIREMENTS` | Texto sem conteúdo significativo. |
| `413` | `SOURCE_TOO_LARGE` | Fonte excede o limite configurado. |

Quando `SOURCE_TOO_LARGE` ocorre, `details` contém atualmente:

```json
{
  "max_chars": 10000,
  "actual_chars": 12000
}
```

Os números acima são apenas ilustrativos: o limite real é configurável no ambiente.

---

# Esclarecimentos

Os endpoints de esclarecimento usam o `analysis_id` no path.

```text
/v0/analyses/{analysis_id}/clarifications
```

O `analysis_id` precisa ser um UUID válido e corresponder a uma análise existente.

---

## `POST /v0/analyses/{analysis_id}/clarifications/plan`

Planeja perguntas de esclarecimento para requisitos condicionais cuja aplicabilidade ainda é desconhecida.

### Path parameter

| Parâmetro | Tipo | Descrição |
| --- | --- | --- |
| `analysis_id` | `UUID` | Identificador da análise existente. |

### Request

O payload é um `InterpreterResultInput` completo:

```json
{
  "buyer": {
    "name": "Cliente Exemplo",
    "confidence": 0.95
  },
  "requirements": [
    {
      "temp_id": "req-1",
      "name": "Registro no conselho profissional",
      "canonical_name": null,
      "category": "LICENSING",
      "type": "DOCUMENT",
      "mandatory": true,
      "blocking": null,
      "conditional": true,
      "condition": "quando aplicável",
      "applicability": "UNKNOWN",
      "issuer": null,
      "source_quote": "quando aplicável, registro no conselho profissional competente",
      "confidence": 0.92
    }
  ],
  "uncertainties": [],
  "clarifications": [],
  "warnings": []
}
```

!!! warning "Exemplo estrutural"
    O payload demonstra o contrato. Os valores não representam uma saída garantida do Interpreter para uma fonte específica.

### `InterpreterResultInput`

| Campo | Tipo | Regra |
| --- | --- | --- |
| `buyer` | `BuyerCandidateInput` | Obrigatório. |
| `requirements` | `array<RequirementCandidateInput>` | Obrigatório. |
| `uncertainties` | `array<UncertaintyInput>` | Opcional no modelo; padrão `[]`. |
| `clarifications` | `array<string>` | Obrigatório. |
| `warnings` | `array<string>` | Obrigatório. |

Os modelos de entrada rejeitam campos extras.

### Critério atual para gerar uma pergunta

Um requisito gera esclarecimento quando todas estas condições são verdadeiras:

```text
conditional = true
applicability = UNKNOWN
condition contém texto
não existe pergunta já planejada para requirement_temp_id
```

A pergunta gerada atualmente usa o formato:

```text
A condição se aplica ao fornecedor? {condition}
```

### Response — `200 OK`

Retorna uma lista de `ClarificationQuestion`.

```json
[
  {
    "id": "<uuid-da-pergunta>",
    "analysis_id": "<uuid-da-analise>",
    "requirement_temp_id": "req-1",
    "condition": "quando aplicável",
    "question": "A condição se aplica ao fornecedor? quando aplicável",
    "answer": null,
    "resolved_applicability": null
  }
]
```

### `ClarificationQuestion`

| Campo | Tipo | Nulo? |
| --- | --- | :---: |
| `id` | `UUID` | não |
| `analysis_id` | `UUID` | não |
| `requirement_temp_id` | `string` | não |
| `condition` | `string` | não |
| `question` | `string` | não |
| `answer` | `YES \| NO` | sim |
| `resolved_applicability` | `Applicability` | sim |

### Erro de domínio conhecido

| HTTP | Código | Condição |
| ---: | --- | --- |
| `404` | `ANALYSIS_NOT_FOUND` | O `analysis_id` não corresponde a uma análise existente. |

---

## `GET /v0/analyses/{analysis_id}/clarifications`

Lista as perguntas de esclarecimento já planejadas para a análise.

### Response — `200 OK`

Retorna:

```text
array<ClarificationQuestion>
```

Quando não existem perguntas planejadas, a lista pode ser vazia.

### Erro de domínio conhecido

| HTTP | Código | Condição |
| ---: | --- | --- |
| `404` | `ANALYSIS_NOT_FOUND` | A análise não existe. |

---

## `POST /v0/analyses/{analysis_id}/clarifications/{clarification_id}/answer`

Responde uma pergunta de esclarecimento existente.

### Path parameters

| Parâmetro | Tipo |
| --- | --- |
| `analysis_id` | `UUID` |
| `clarification_id` | `UUID` |

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

### Efeito sobre a aplicabilidade

```text
YES → APPLICABLE
NO  → NOT_APPLICABLE
```

### Response — `200 OK`

```json
{
  "clarification": {
    "id": "<uuid-da-pergunta>",
    "analysis_id": "<uuid-da-analise>",
    "requirement_temp_id": "req-1",
    "condition": "quando aplicável",
    "question": "A condição se aplica ao fornecedor? quando aplicável",
    "answer": "YES",
    "resolved_applicability": "APPLICABLE"
  },
  "applicability": "APPLICABLE"
}
```

### Idempotência da resposta

Se a pergunta já foi respondida e a mesma resposta é enviada novamente, a operação devolve o resultado correspondente sem conflito.

Exemplo:

```text
YES → YES
```

continua válido.

Se uma resposta diferente for enviada depois que a pergunta já foi resolvida, ocorre conflito:

```text
YES → NO
```

### Erros de domínio conhecidos

| HTTP | Código | Condição |
| ---: | --- | --- |
| `404` | `ANALYSIS_NOT_FOUND` | A análise não existe. |
| `404` | `CLARIFICATION_NOT_FOUND` | O esclarecimento não existe para aquela análise. |
| `409` | `CLARIFICATION_CONFLICT` | O esclarecimento já foi respondido com valor diferente. |

---

# Formato dos erros de domínio

Erros gerados como `ApplicationError` seguem este envelope:

```json
{
  "error": {
    "code": "INVALID_CNPJ",
    "message": "CNPJ must be valid and use either 14 digits or the standard mask.",
    "details": {}
  }
}
```

Estrutura:

| Campo | Tipo |
| --- | --- |
| `error.code` | `string` |
| `error.message` | `string` |
| `error.details` | `object` |

!!! note "Erros de validação do framework"
    O envelope acima é específico para `ApplicationError`. Erros de validação de request gerados pelo FastAPI/Pydantic não passam por esse handler e podem usar o formato padrão de validação do framework.

---

# Autenticação

A aplicação atual não registra mecanismo de autenticação ou autorização nesses routers.

Isso descreve apenas o contrato presente da `v0`; **não deve ser interpretado como decisão de segurança para uma API pública de produção**.

---

# Persistência atual

As análises e perguntas de esclarecimento são mantidas atualmente em memória pelo serviço da aplicação.

Consequências desta implementação do MVP:

- os registros não representam persistência durável;
- reiniciar o processo pode eliminar o estado mantido em memória;
- o contrato atual serve para validar o slice funcional, não uma arquitetura final de armazenamento.

---

# O que não está exposto via HTTP

O código atual possui capacidades internas adicionais, mas elas não fazem parte da API HTTP registrada hoje.

Entre elas estão:

- execução do `RequirementInterpreter`;
- consulta do resultado interpretado;
- cálculo de readiness;
- summary;
- source traces;
- truth projection.

Essas capacidades só devem entrar nesta referência quando uma rota pública correspondente fizer parte efetiva da aplicação.

---

## Regra para esta referência

> **Se não existe rota registrada, não existe endpoint documentado.**

Isso mantém a documentação da API alinhada ao contrato que realmente pode ser chamado na `v0`.

[Consultar Modelo de requisito](requirement-model.md){ .md-button }
[Consultar Estados e enums](states-enums.md){ .md-button }
