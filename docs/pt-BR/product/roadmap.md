# O que estamos construindo

Estamos construindo o Supplier Ready em camadas, começando pelo problema que sustenta todo o restante: entender com confiança o que um novo cliente exige da sua empresa.

## 1. Entender as exigências

Transformar o que o cliente enviou em requisitos claros, rastreáveis e sem suposições silenciosas.

!!! info "Primeira jornada disponível"
    O MVP já recebe uma fonte textual, executa a interpretação, preserva rastreabilidade, apresenta incertezas e resolve condições de aplicabilidade por esclarecimentos.

## 2. Entender sua empresa

Relacionar os requisitos à realidade da sua empresa: o que já existe, o que está válido e o que efetivamente atende cada exigência.

!!! note "Em desenvolvimento"
    O domínio já possui estados de avaliação, mas a coleta e vinculação completa de evidências de atendimento ainda não fazem parte da jornada pública de ponta a ponta.

## 3. Identificar e resolver os gaps

Mostrar o que falta, o que exige ação, o que depende de informação e quais bloqueios ainda impedem o avanço.

!!! note "Em desenvolvimento"
    `Gap` ainda não é um objeto formal do domínio atual. A modelagem de ação, prioridade, responsável e prazo permanece como direção de produto.

## 4. Acompanhar a Readiness

Transformar avaliações conhecidas em uma medida determinística de progresso.

!!! info "Disponível no motor"
    O `ReadinessCalculator` já existe e possui fórmula, pesos e contadores definidos. A readiness ainda não está exposta na jornada web/API de produto atual.

## 5. Chegar ao Ready

Construir um estado final que responda se ainda existe algo relevante impedindo a empresa de avançar com aquele cliente.

!!! warning "Dois usos diferentes de READY"
    A jornada de interpretação possui hoje `ProductAnalysisState.READY`, que significa apenas **sem esclarecimentos pendentes**. O **Ready final do produto**, baseado em atendimento, gaps e bloqueios, ainda não existe como estado de domínio.

---

## Princípio de evolução

Cada nova camada deve preservar o que sustenta a confiança no produto:

**fonte original → interpretação rastreável → aplicabilidade explícita → avaliação sustentada → gaps acionáveis → readiness determinística → Ready**

!!! note "Produto em desenvolvimento"
    Esta página comunica a direção pública do produto, não um compromisso de datas. Capacidades atuais e futuras são identificadas separadamente para que roadmap não seja confundido com Referência.
