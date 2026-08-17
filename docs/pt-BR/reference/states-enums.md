# Estados e enums

## Valores fechados do domínio atual.

Esta página lista os estados e enums implementados atualmente no Supplier Ready `v0`.

Os valores são apresentados exatamente como aparecem no contrato do domínio.

---

## Análise

### `AnalysisStatus`

Estado atual de uma análise.

| Valor | Significado |
| --- | --- |
| `RECEIVED` | A análise foi criada e sua fonte foi recebida. |

Atualmente, `RECEIVED` é o único estado implementado para uma análise.

### `RequirementSourceType`

Tipo da fonte associada à análise.

| Valor | Significado |
| --- | --- |
| `TEXT` | Fonte fornecida como conteúdo textual. |

`TEXT` é o único tipo de fonte suportado pelo domínio atual.

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

`UNKNOWN` é um estado válido do domínio e não deve ser convertido automaticamente em `APPLICABLE` ou `NOT_APPLICABLE`.

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

Uma incerteza também possui uma mensagem, um trecho da fonte e pode estar associada a um requisito candidato específico.

---

## Esclarecimentos

### `ClarificationAnswer`

Respostas aceitas atualmente por uma pergunta de esclarecimento.

| Valor | Efeito atual sobre aplicabilidade |
| --- | --- |
| `YES` | Resolve para `APPLICABLE`. |
| `NO` | Resolve para `NOT_APPLICABLE`. |

O contrato atual aceita apenas respostas binárias `YES` e `NO`.

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

O peso listado corresponde à implementação atual do cálculo de readiness. Um item também é excluído quando sua `Applicability` é `NOT_APPLICABLE`.

Se a `Applicability` for `UNKNOWN`, o item permanece como pendência de aplicabilidade e ainda não entra no score.

---

## Valores que ainda não existem no contrato

Alguns conceitos usados na documentação de produto ainda não são enums ou estados implementados na `v0`.

Entre eles:

- `Ready` como estado de domínio;
- estados formais de gap;
- tipos adicionais de fonte como PDF, planilha ou e-mail.

Eles não devem ser tratados como valores válidos da API ou do domínio atual até serem implementados.

[Voltar para Referência](index.md){ .md-button }
