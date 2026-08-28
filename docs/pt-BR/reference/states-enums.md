# Estados e enums

## Valores fechados do contrato atual.

Esta página lista os estados e enums implementados atualmente no Supplier Ready `v0`, incluindo valores do domínio e valores expostos pela API de produto.

Os valores são apresentados exatamente como aparecem no contrato atual.

---

## Análise

### `AnalysisStatus`

Estado interno da análise registrada.

| Valor | Significado |
| --- | --- |
| `RECEIVED` | A análise foi criada e sua fonte foi recebida. |

Atualmente, `RECEIVED` é o único estado implementado em `AnalysisStatus`.

### `RequirementSourceType`

Tipo da fonte associada à análise.

| Valor | Significado |
| --- | --- |
| `TEXT` | Fonte fornecida como conteúdo textual. |

`TEXT` é o único tipo de fonte suportado pelo domínio atual.

---

## Estado da jornada de produto

### `ProductAnalysisState`

Estado exposto por `/v0/product/analyses`.

| Valor | Significado atual |
| --- | --- |
| `NEEDS_CLARIFICATION` | Existe pelo menos um esclarecimento ainda sem resposta. |
| `READY` | Não existe esclarecimento pendente na etapa atual de interpretação. |

!!! warning "`READY` não é Readiness"
    `ProductAnalysisState.READY` não resulta do cálculo de readiness e não afirma que a empresa atende todas as exigências do cliente. Ele significa somente que a jornada de interpretação atual não possui perguntas de esclarecimento pendentes.

Esse estado de API é diferente do conceito de produto **Ready** descrito em [Readiness](../concepts/readiness.md), cuja definição final ainda não existe como estado de domínio do motor de avaliação.

---

## Requisitos

### `RequirementCategory`

Categoria semântica atribuída a um requisito candidato.

| Valor |
| --- |
| `CORPORATE` |
| `TAX` |
| `LABOR` |
| `FINANCIAL` |
| `TECHNICAL` |
| `LICENSING` |
| `BANKING` |
| `COMPLIANCE` |
| `DECLARATION` |
| `IDENTITY` |
| `OTHER` |

### `RequirementType`

Tipo estrutural do requisito identificado.

| Valor |
| --- |
| `DOCUMENT` |
| `DATA` |
| `DECLARATION` |
| `CERTIFICATION` |
| `POLICY` |
| `ACCEPTANCE` |
| `CAPABILITY` |
| `OTHER` |

---

## Aplicabilidade

### `Applicability`

Indica se um requisito se aplica à empresa analisada.

| Valor | Significado |
| --- | --- |
| `APPLICABLE` | O requisito se aplica. |
| `NOT_APPLICABLE` | O requisito não se aplica. |
| `UNKNOWN` | Ainda não há informação suficiente para determinar a aplicabilidade. |

`UNKNOWN` é um estado válido e não deve ser convertido automaticamente em `APPLICABLE` ou `NOT_APPLICABLE`.

---

## Incertezas da interpretação

### `UncertaintyReason`

Motivo estruturado para uma incerteza registrada pelo Interpreter.

| Valor | Significado |
| --- | --- |
| `AMBIGUOUS` | A fonte admite interpretação ambígua. |
| `MISSING_CONTEXT` | Falta contexto necessário para uma conclusão. |
| `UNSUPPORTED_DETAIL` | Um detalhe não possui suporte suficiente na fonte. |
| `OTHER` | Outro motivo de incerteza. |

---

## Esclarecimentos

### `ClarificationAnswer`

Respostas aceitas atualmente por uma pergunta de esclarecimento.

| Valor | Efeito atual sobre aplicabilidade |
| --- | --- |
| `YES` | Resolve para `APPLICABLE`. |
| `NO` | Resolve para `NOT_APPLICABLE`. |

---

## Avaliação de requisitos

### `AssessmentStatus`

Representa a situação de atendimento de um requisito durante o cálculo de readiness.

| Valor | Significado | Peso atual |
| --- | --- | ---: |
| `SATISFIED` | Requisito atendido. | `1.0` |
| `PARTIAL` | Requisito atendido parcialmente. | `0.5` |
| `MISSING` | Requisito não atendido. | `0.0` |
| `UNKNOWN` | Situação de atendimento ainda desconhecida. | `0.0` |
| `NOT_APPLICABLE` | Requisito não aplicável. | excluído |

Um item também é excluído quando sua `Applicability` é `NOT_APPLICABLE`. Se a aplicabilidade for `UNKNOWN`, ele fica pendente e ainda não entra no score.

---

## Telemetria de funil

### `FunnelEventName`

Eventos aceitos pelo endpoint `/v0/telemetry/funnel`.

| Valor |
| --- |
| `landing_viewed` |
| `analysis_started` |
| `requirement_submitted` |
| `analysis_completed` |
| `result_viewed` |
| `requirement_expanded` |

---

## Valores que ainda não existem como estado de domínio

Alguns conceitos usados no produto ainda não existem como estados formais do motor de avaliação.

Entre eles:

- `Ready` como conclusão derivada das avaliações e bloqueios;
- estados formais de gap;
- tipos adicionais de fonte como PDF, planilha ou e-mail.

A existência de `ProductAnalysisState.READY` **não altera essa distinção**: esse valor pertence à jornada de interpretação da API de produto e possui semântica mais restrita.

[Consultar API v0](api-v0.md){ .md-button }
[Voltar para Referência](index.md){ .md-button }
