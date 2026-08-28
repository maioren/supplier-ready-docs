# Referência

## Consulte os contratos atuais do Supplier Ready.

A seção **Referência** descreve de forma precisa as estruturas, estados e interfaces que existem no MVP atual.

Diferente de [Conceitos](../concepts/index.md), que explicam o modelo mental do produto, e de [Guias](../guides/index.md), que ajudam a realizar tarefas, esta seção funciona como consulta objetiva do contrato implementado.

> **Referência descreve o contrato atual da `v0`. Não descreve intenção futura.**

Elementos planejados, mas ainda não implementados, não são apresentados aqui como parte do contrato do produto.

---

## Referências

### Estados e enums

Valores fechados usados atualmente pelo domínio e pela API, incluindo estados da análise, jornada de produto, categorias e tipos de requisito, aplicabilidade, incertezas, esclarecimentos, avaliações e eventos de telemetria.

[Consultar Estados e enums →](states-enums.md)

### Modelo de requisito

Referência campo a campo da estrutura produzida pelo Interpreter para representar um requisito candidato, incluindo tipos, nulabilidade e invariantes de validação.

[Consultar Modelo de requisito →](requirement-model.md)

### Readiness

Fórmula, pesos, contadores, estrutura de entrada e saída e regras determinísticas usadas pelo cálculo atual de readiness.

[Consultar Readiness →](readiness.md)

### API v0

Endpoints HTTP realmente expostos pela aplicação atual, incluindo a jornada integrada de produto, contratos de baixo nível e telemetria de funil.

[Consultar API v0 →](api-v0.md)

### Erros

Códigos de erro estruturados atualmente observáveis na `v0` e seus significados.

[Consultar Erros →](errors.md)

---

## Regra de estabilidade

A presença de um item nesta seção significa que ele **existe no contrato atual**, mas a `v0` ainda é uma versão inicial e pode evoluir.

Quando um contrato público mudar no MVP, sua referência correspondente deve ser atualizada junto com a implementação.

Recursos futuros como um estado de domínio **Ready** derivado das avaliações e bloqueios, evidências completas de atendimento ou novos tipos de fonte devem permanecer fora desta seção até fazerem parte efetiva do contrato.

!!! note "Sobre `ProductAnalysisState.READY`"
    A API de produto já possui um valor `READY`, documentado em [Estados e enums](states-enums.md). Ele significa que não existem esclarecimentos pendentes na etapa de interpretação e não deve ser confundido com o futuro estado de conclusão baseado em atendimento dos requisitos.
