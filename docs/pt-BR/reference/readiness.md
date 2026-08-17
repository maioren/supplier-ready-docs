# Readiness

## Contrato determinístico do cálculo atual.

Esta página descreve a implementação atual da readiness na `v0`: estrutura de entrada, regras de inclusão e exclusão, pesos, fórmula e estrutura do resultado.

Para entender o significado de produto da readiness, consulte [Readiness em Conceitos](../concepts/readiness.md).

---

## Entrada: `RequirementAssessment`

O cálculo recebe uma lista de avaliações de requisitos.

Cada item possui exatamente três campos:

| Campo | Tipo | Regra |
| --- | --- | --- |
| `requirement_temp_id` | `string` | Obrigatório e não vazio. |
| `status` | `AssessmentStatus` | Situação de atendimento do requisito. |
| `applicability` | `Applicability` | Aplicabilidade atual do requisito. |

O modelo usa validação estrita e rejeita campos extras.

Exemplo estrutural:

```json
{
  "requirement_temp_id": "req-1",
  "status": "SATISFIED",
  "applicability": "APPLICABLE"
}
```

---

## Pesos por status

O cálculo usa os seguintes pesos:

| `AssessmentStatus` | Peso |
| --- | ---: |
| `SATISFIED` | `1.0` |
| `PARTIAL` | `0.5` |
| `MISSING` | `0.0` |
| `UNKNOWN` | `0.0` |
| `NOT_APPLICABLE` | `0.0`* |

`NOT_APPLICABLE` possui peso definido como `0.0`, mas um item com esse status é excluído antes de participar do cálculo. Portanto, esse peso não contribui para o score na implementação atual.

---

## Ordem das regras de classificação

Para cada `RequirementAssessment`, o calculador aplica as regras nesta ordem.

### 1. Status `NOT_APPLICABLE`

Se:

```text
status = NOT_APPLICABLE
```

o item é excluído imediatamente.

Efeito:

```text
excluded_not_applicable_count += 1
```

O item não entra no denominador nem nos contadores de status avaliáveis.

### 2. Aplicabilidade `NOT_APPLICABLE`

Se o status não causou a exclusão anterior, mas:

```text
applicability = NOT_APPLICABLE
```

o item também é excluído.

Efeito:

```text
excluded_not_applicable_count += 1
```

### 3. Aplicabilidade `UNKNOWN`

Se o item não foi excluído e:

```text
applicability = UNKNOWN
```

ele é tratado como pendência de aplicabilidade.

Efeito:

```text
pending_applicability_count += 1
```

O item ainda não entra no score.

### 4. Item avaliável

Os itens restantes entram no cálculo.

Efeito:

```text
scoreable_count += 1
weighted_total += peso(status)
```

O contador correspondente ao status também é incrementado para `SATISFIED`, `PARTIAL`, `MISSING` ou `UNKNOWN`.

---

## Fórmula

Quando existe pelo menos um item avaliável:

```text
score = (weighted_total / scoreable_count) × 100
```

onde:

```text
weighted_total = soma dos pesos dos itens avaliáveis
```

O resultado é um `float` entre `0.0` e `100.0`.

### Nenhum item avaliável

Se:

```text
scoreable_count = 0
```

então:

```text
score = null
```

A implementação não converte ausência de itens avaliáveis em `0%`.

---

## Exemplo de cálculo

Considere os seguintes itens avaliáveis:

```text
7 × SATISFIED
2 × PARTIAL
1 × MISSING
```

Então:

```text
weighted_total = (7 × 1.0) + (2 × 0.5) + (1 × 0.0)
weighted_total = 8.0

scoreable_count = 10

score = (8.0 / 10) × 100
score = 80.0
```

O resultado é:

```text
80.0
```

---

## Aplicabilidade desconhecida × status desconhecido

A implementação trata esses casos de forma diferente.

### `applicability = UNKNOWN`

O item não é considerado avaliável ainda.

```text
pending_applicability_count += 1
```

Ele não entra no denominador.

### `applicability = APPLICABLE` e `status = UNKNOWN`

O item é avaliável, mas seu atendimento é desconhecido.

```text
scoreable_count += 1
unknown_count += 1
peso = 0.0
```

Ele entra no denominador e reduz o score em relação a um item atendido.

---

## Saída: `ReadinessResult`

O calculador retorna um objeto com oito campos:

| Campo | Tipo | Significado |
| --- | --- | --- |
| `score` | `float \| null` | Percentual calculado entre `0.0` e `100.0`; `null` quando não existem itens avaliáveis. |
| `scoreable_count` | `int` | Quantidade de itens que participaram do cálculo. |
| `pending_applicability_count` | `int` | Itens cuja aplicabilidade ainda é `UNKNOWN`. |
| `excluded_not_applicable_count` | `int` | Itens excluídos por status ou aplicabilidade `NOT_APPLICABLE`. |
| `satisfied_count` | `int` | Itens avaliáveis com status `SATISFIED`. |
| `partial_count` | `int` | Itens avaliáveis com status `PARTIAL`. |
| `missing_count` | `int` | Itens avaliáveis com status `MISSING`. |
| `unknown_count` | `int` | Itens avaliáveis com status `UNKNOWN`. |

Todos os contadores são inteiros maiores ou iguais a zero.

---

## Exemplo de resultado

Para uma entrada que resulte em 7 atendidos, 2 parciais e 1 faltando:

```json
{
  "score": 80.0,
  "scoreable_count": 10,
  "pending_applicability_count": 0,
  "excluded_not_applicable_count": 0,
  "satisfied_count": 7,
  "partial_count": 2,
  "missing_count": 1,
  "unknown_count": 0
}
```

---

## Propriedades do cálculo atual

### Determinístico

A função não usa IA, aleatoriedade ou confiança do Interpreter para escolher o percentual.

Para a mesma lista de avaliações, o resultado é o mesmo.

### Sem arredondamento explícito

A implementação calcula diretamente:

```text
(weighted_total / scoreable_count) × 100.0
```

Não existe, nesta camada, uma regra explícita de arredondamento para número inteiro ou quantidade fixa de casas decimais.

### Sem pesos por requisito

Na implementação atual, o peso depende exclusivamente de `AssessmentStatus`.

Não existe peso adicional por categoria, requisito, obrigatoriedade ou caráter bloqueante.

### Sem estado `Ready`

`ReadinessResult` não possui campo `ready` e o calculador não determina se a empresa está `Ready`.

Essa decisão não faz parte do contrato atual desta camada.

---

## Pseudocódigo do algoritmo

```text
para cada assessment:
    se status == NOT_APPLICABLE:
        excluded += 1
        continuar

    se applicability == NOT_APPLICABLE:
        excluded += 1
        continuar

    se applicability == UNKNOWN:
        pending += 1
        continuar

    scoreable += 1
    weighted_total += peso(status)
    incrementar contador do status

se scoreable == 0:
    score = null
senão:
    score = weighted_total / scoreable × 100
```

Esse fluxo corresponde às regras implementadas atualmente pelo `ReadinessCalculator`.

[Consultar Estados e enums](states-enums.md){ .md-button }
[Entender Readiness como conceito](../concepts/readiness.md){ .md-button }
