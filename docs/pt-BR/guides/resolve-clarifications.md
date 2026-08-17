# Resolver esclarecimentos

## Transforme uma condição desconhecida em uma decisão explícita.

Esclarecimentos existem para situações em que o Supplier Ready identifica um requisito condicional, mas ainda não possui informação suficiente para determinar se ele se aplica à empresa.

> **Quando não souber, o Supplier Ready não deve adivinhar. Deve perguntar.**

!!! info "Disponível no MVP"
    O MVP já consegue planejar, listar e responder esclarecimentos. A experiência visual integrada ainda está em desenvolvimento.

## 1. Entenda quando uma pergunta é criada

No comportamento atual, um esclarecimento é planejado quando o requisito é **condicional**, sua aplicabilidade está `UNKNOWN` e existe uma condição explícita a resolver.

O serviço mantém no máximo uma pergunta planejada por requisito dentro da análise.

## 2. Revise a condição antes de responder

Cada esclarecimento mantém a referência ao requisito, a condição original e a pergunta produzida.

Antes de responder, confirme que você entendeu **qual condição está sendo avaliada**. A resposta não altera o texto original do cliente; ela adiciona contexto à análise.

## 3. Responda YES ou NO

O contrato atual aceita duas respostas:

- `YES` — a condição se aplica;
- `NO` — a condição não se aplica.

A resposta resolve a aplicabilidade para `APPLICABLE` ou `NOT_APPLICABLE`, respectivamente.

Na API atual, a operação é:

`POST /v0/analyses/{analysis_id}/clarifications/{clarification_id}/answer`

com uma resposta no formato:

```json
{
  "answer": "YES"
}
```

## 4. Confirme a aplicabilidade resolvida

Depois da resposta, o resultado informa o esclarecimento atualizado e a aplicabilidade resolvida.

Responder novamente com o mesmo valor é idempotente. Tentar alterar uma resposta já registrada para o valor oposto gera `CLARIFICATION_CONFLICT`.

Se a análise ou o esclarecimento não existir, o MVP retorna os erros de domínio correspondentes.

## 5. Reavalie o requisito

No orquestrador do motor, a resposta atualiza a aplicabilidade do requisito correspondente. Isso permite que as próximas etapas deixem de tratar aquela condição como desconhecida.

!!! note "Experiência integrada"
    A API pública atual expõe as operações de esclarecimento, enquanto a reavaliação integrada de toda a análise ainda está sendo consolidada como experiência de produto.

## Resultado esperado

Ao concluir um esclarecimento, uma condição antes desconhecida passa a ter uma decisão explícita de aplicabilidade, sem transformar uma suposição da IA em fato.

[Acompanhar a Readiness →](track-readiness.md){ .md-button .md-button--primary }
