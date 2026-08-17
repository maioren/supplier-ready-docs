# Referência

## Consulte os contratos atuais do Supplier Ready.

A seção **Referência** descreve de forma precisa as estruturas, estados e interfaces que existem no MVP atual.

Diferente de [Conceitos](../concepts/index.md), que explicam o modelo mental do produto, e de [Guias](../guides/index.md), que ajudam a realizar tarefas, esta seção funciona como consulta objetiva do contrato implementado.

> **Referência descreve o contrato atual da `v0`. Não descreve intenção futura.**

Elementos planejados, mas ainda não implementados, não são apresentados aqui como parte do contrato do produto.

---

## Referências

### Estados e enums

Valores fechados usados atualmente pelo domínio, incluindo estados da análise, tipos de fonte, categorias e tipos de requisito, aplicabilidade, incertezas, esclarecimentos e avaliações.

[Consultar Estados e enums →](states-enums.md)

### Modelo de requisito

Referência campo a campo da estrutura produzida pelo Interpreter para representar um requisito candidato, incluindo tipos, nulabilidade e invariantes de validação.

[Consultar Modelo de requisito →](requirement-model.md)

### Readiness

Fórmula, pesos, contadores, estrutura de entrada e saída e regras determinísticas usadas pelo cálculo atual de readiness.

[Consultar Readiness →](readiness.md)

### API v0

Endpoints HTTP realmente expostos pela aplicação atual, seus contratos de entrada e saída e códigos de resposta.

**Próxima referência a ser publicada.**

### Erros

Códigos de erro públicos do MVP e seus significados.

**Planejado para esta seção.**

---

## Regra de estabilidade

A presença de um item nesta seção significa que ele **existe no contrato atual**, mas a `v0` ainda é uma versão inicial e pode evoluir.

Quando um contrato público mudar no MVP, sua referência correspondente deve ser atualizada junto com a implementação.

Recursos futuros como o estado de domínio **Ready**, evidências completas de atendimento, novos tipos de fonte ou endpoints ainda não expostos devem permanecer fora desta seção até fazerem parte efetiva do contrato.
