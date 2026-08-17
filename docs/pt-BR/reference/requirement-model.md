# Modelo de requisito

## Estrutura atual de um requisito interpretado.

O Interpreter representa cada requisito identificado como um `RequirementCandidate`.

Esta página descreve o contrato atual dessa estrutura na `v0`: campos, tipos, nulabilidade, valores permitidos e invariantes de validação.

---

## `RequirementCandidate`

| Campo | Tipo | Nulo? | Regra atual |
| --- | --- | :---: | --- |
| `temp_id` | `string` | não | Identificador temporário do requisito dentro do resultado da interpretação. |
| `name` | `string` | não | Nome interpretado do requisito. |
| `canonical_name` | `string` | sim | Nome canônico quando disponível. |
| `category` | `RequirementCategory` | não | Categoria semântica do requisito. |
| `type` | `RequirementType` | não | Tipo estrutural do requisito. |
| `mandatory` | `boolean` | não | Indica se a fonte estabelece o requisito como obrigatório. |
| `blocking` | `boolean` | sim | Indicação de bloqueio quando essa informação pode ser determinada. |
| `conditional` | `boolean` | não | Indica se o requisito depende de uma condição. |
| `condition` | `string` | sim | Condição textual associada ao requisito condicional. |
| `applicability` | `Applicability` | não | Aplicabilidade atual: `APPLICABLE`, `NOT_APPLICABLE` ou `UNKNOWN`. |
| `issuer` | `string` | sim | Emissor ou entidade relacionada ao requisito, quando identificável. |
| `source_quote` | `string` | não | Trecho não vazio da fonte que sustenta a interpretação. |
| `confidence` | `float` | não | Confiança da interpretação, entre `0.0` e `1.0`, inclusive. |

Os valores possíveis de `category`, `type` e `applicability` estão listados em [Estados e enums](states-enums.md).

---

## Identificação

### `temp_id`

Identificador temporário usado para relacionar o requisito a outras estruturas produzidas durante o fluxo, como incertezas e esclarecimentos.

O contrato atual exige uma `string`, mas não estabelece nesta estrutura um formato específico, como UUID.

### `name`

Nome legível produzido para representar aquilo que foi identificado como requisito.

### `canonical_name`

Nome normalizado ou canônico quando essa representação estiver disponível.

Pode ser `null`.

---

## Classificação

### `category`

Classifica semanticamente o assunto do requisito usando `RequirementCategory`.

Exemplos de valores atuais incluem `CORPORATE`, `TAX`, `TECHNICAL`, `LICENSING` e `COMPLIANCE`.

### `type`

Representa a natureza estrutural do que está sendo exigido usando `RequirementType`.

Exemplos atuais incluem `DOCUMENT`, `DATA`, `DECLARATION`, `CERTIFICATION`, `POLICY` e `CAPABILITY`.

Categoria e tipo respondem perguntas diferentes: uma descreve **sobre o que** é o requisito; a outra, **que tipo de exigência** ele representa.

---

## Obrigatoriedade e bloqueio

### `mandatory`

Booleano obrigatório.

- `true` — a interpretação considera que a fonte estabelece o requisito como obrigatório;
- `false` — a interpretação não o classifica como obrigatório.

Esse campo não substitui `conditional`. Um requisito pode ser obrigatório quando determinada condição for satisfeita.

### `blocking`

Pode ser `true`, `false` ou `null`.

A nulabilidade permite representar situações em que o caráter bloqueante não pode ser determinado no contrato atual.

`blocking` não deve ser confundido com `mandatory`: são informações distintas no modelo.

---

## Condicionalidade

### `conditional`

Booleano que informa se o requisito depende de uma condição.

### `condition`

Texto da condição quando `conditional = true`.

O modelo possui uma invariante explícita:

```text
conditional = true  → condition deve conter texto
conditional = false → condition deve ser null
```

Portanto, estas combinações são inválidas:

```text
conditional = true
condition = null
```

```text
conditional = false
condition = "quando aplicável"
```

Essa regra impede que a condição seja perdida ou que uma condição seja associada a um requisito declarado como incondicional.

---

## Aplicabilidade

### `applicability`

Usa o enum `Applicability`:

- `APPLICABLE`;
- `NOT_APPLICABLE`;
- `UNKNOWN`.

A aplicabilidade é obrigatória no objeto, mas pode assumir `UNKNOWN` quando ainda não existe informação suficiente para determinar se o requisito se aplica à empresa.

`UNKNOWN` não equivale a `false` e não deve ser interpretado como `NOT_APPLICABLE`.

---

## Emissor

### `issuer`

Identifica um emissor ou entidade relacionada ao requisito quando essa informação puder ser determinada.

Pode ser `null`.

O contrato do `RequirementCandidate` não impõe catálogo fechado de emissores.

---

## Evidência da fonte

### `source_quote`

Trecho da fonte usado como evidência para a interpretação.

É uma `string` obrigatória com pelo menos um caractere. Um `RequirementCandidate` válido não pode possuir `source_quote` vazio.

Esse campo sustenta a rastreabilidade entre o requisito estruturado e aquilo que foi efetivamente informado na fonte.

[Entenda o conceito de Rastreabilidade e evidências](../concepts/traceability-evidence.md)

---

## Confiança

### `confidence`

Número entre `0.0` e `1.0`, inclusive.

```text
0.0 ≤ confidence ≤ 1.0
```

Valores fora desse intervalo são inválidos para o modelo.

`confidence` expressa a confiança associada à interpretação; não representa probabilidade de aprovação pelo cliente nem substitui `source_quote` como evidência.

---

## Validação do objeto

O modelo atual usa validação estrita e rejeita campos extras.

Isso significa que um `RequirementCandidate` deve respeitar a estrutura declarada e não pode receber propriedades arbitrárias fora do contrato.

Além das validações de tipo, existem duas restrições explícitas no modelo:

1. `source_quote` precisa ser não vazio;
2. `conditional` e `condition` precisam respeitar a invariante de condicionalidade.

`confidence` também é limitado ao intervalo de `0.0` a `1.0`.

---

## Exemplo estrutural

Um requisito condicional pode assumir uma estrutura como:

```json
{
  "temp_id": "req-2",
  "name": "Registro no conselho profissional competente",
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
```

!!! warning "Exemplo ilustrativo"
    Os valores acima servem para demonstrar a estrutura do contrato. Eles não representam a saída garantida do Interpreter para um texto específico.

---

## Estruturas relacionadas

`RequirementCandidate` não existe isoladamente no resultado do Interpreter.

Uma interpretação também pode conter:

- informações sobre o cliente identificado;
- `uncertainties`;
- `clarifications`;
- `warnings`.

Uma `Uncertainty` pode referenciar o requisito por meio de `requirement_temp_id`, mantendo a relação com o candidato correspondente.

[Consultar Estados e enums](states-enums.md){ .md-button }
[Voltar para Referência](index.md){ .md-button }
