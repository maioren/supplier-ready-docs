# Resolver esclarecimentos

## Transforme uma condição desconhecida em uma decisão explícita.

Esclarecimentos existem para situações em que o Supplier Ready identifica um requisito condicional, mas ainda não possui informação suficiente para determinar se ele se aplica à empresa.

> **Quando não souber, o Supplier Ready não deve adivinhar. Deve perguntar.**

!!! info "Disponível no MVP"
    A jornada de produto já consegue criar uma análise, apresentar esclarecimentos pendentes, registrar respostas e devolver a análise atualizada. Os endpoints de baixo nível de esclarecimento também permanecem disponíveis na `v0`.

## 1. Entenda quando uma pergunta é criada

No comportamento atual, um esclarecimento é planejado quando o requisito é **condicional**, sua aplicabilidade está `UNKNOWN` e existe uma condição explícita a resolver.

O serviço mantém no máximo uma pergunta planejada por requisito dentro da análise.

## 2. Revise a condição antes de responder

Cada esclarecimento mantém a referência ao requisito, a condição original e a pergunta produzida.

Antes de responder, confirme que você entendeu **qual condição está sendo avaliada**. A resposta não altera o texto original do cliente; ela adiciona contexto à análise.

## 3. Responda Sim ou Não

Na experiência do produto, as opções apresentadas ao usuário são **Sim** e **Não**. No contrato HTTP, elas são representadas pelos valores:

- `YES` — a condição se aplica;
- `NO` — a condição não se aplica.

A resposta resolve a aplicabilidade para `APPLICABLE` ou `NOT_APPLICABLE`, respectivamente.

Na jornada de produto, a operação é:

`POST /v0/product/analyses/{analysis_id}/clarifications/{clarification_id}/answer`

com payload:

```json
{
  "answer": "YES"
}
```

A resposta devolve a análise de produto atualizada.

!!! note "Contrato de baixo nível"
    A `v0` também mantém `POST /v0/analyses/{analysis_id}/clarifications/{clarification_id}/answer`, que retorna o resultado específico do esclarecimento. Consulte [API v0](../reference/api-v0.md) para os dois contratos.

## 4. Observe o estado da jornada

A resposta integrada usa `ProductAnalysisState`:

- `NEEDS_CLARIFICATION` — ainda existe pelo menos uma pergunta sem resposta;
- `READY` — não existem esclarecimentos pendentes.

!!! warning "READY nesta resposta não é o Ready final do produto"
    `ProductAnalysisState.READY` significa apenas que a **interpretação pode prosseguir sem esclarecimentos pendentes**. Não significa que todos os requisitos estejam atendidos, que a readiness seja 100% ou que a empresa esteja pronta para homologação.

Quando ainda existem perguntas, `pending_clarifications` contém apenas as não respondidas. Quando a última pergunta é resolvida, a jornada passa a apresentar o resultado interpretado.

## 5. Confirme a aplicabilidade resolvida

No orquestrador, responder `YES` atualiza o requisito correspondente para `APPLICABLE`; responder `NO` atualiza para `NOT_APPLICABLE`.

Responder novamente com o mesmo valor é idempotente. Tentar alterar uma resposta já registrada para o valor oposto gera `CLARIFICATION_CONFLICT`.

Se a análise ou o esclarecimento não existir, o MVP retorna os erros de domínio correspondentes.

## Resultado esperado

Ao concluir os esclarecimentos necessários, condições antes desconhecidas passam a ter decisões explícitas de aplicabilidade e a interpretação pode ser apresentada sem perguntas pendentes — sem transformar uma suposição da IA em fato.

[Revisar requisitos interpretados →](review-interpreted-requirements.md){ .md-button .md-button--primary }
