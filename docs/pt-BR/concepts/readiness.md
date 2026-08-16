# Readiness

## Readiness mede o que já está resolvido. Não prevê a decisão do cliente.

**Readiness** representa o quanto sua empresa está preparada para avançar com um cliente considerando as exigências conhecidas e a situação atual de cada requisito.

Se uma análise apresenta **80% de readiness**, isso **não significa 80% de chance de aprovação pelo cliente**.

Significa que, segundo as informações conhecidas e as regras da análise, parte do que precisa ser atendido já está resolvida.

!!! info "Disponível no MVP"
    O motor atual já calcula readiness de forma determinística a partir das avaliações dos requisitos. A experiência visual integrada para acompanhar esse resultado ainda está sendo construída.

---

## Os estados que alimentam a readiness

Depois que a aplicabilidade de um requisito é conhecida, sua situação pode contribuir para o cálculo da readiness.

### Atendido

O requisito foi resolvido.

**Peso atual no MVP:** 1,0

### Parcial

O requisito foi atendido apenas em parte e ainda existe algo a resolver.

**Peso atual no MVP:** 0,5

### Faltando

O requisito se aplica, mas ainda não foi atendido.

**Peso atual no MVP:** 0,0

### Desconhecido

Sabemos que o requisito é avaliável, mas ainda não temos informação suficiente para determinar se ele foi atendido.

**Peso atual no MVP:** 0,0

### Não aplicável

O requisito não se aplica à empresa.

Ele é **excluído do cálculo** e não reduz a readiness.

---

## Aplicabilidade desconhecida é diferente de avaliação desconhecida

Essa diferença é importante.

Se ainda não sabemos **se um requisito se aplica à empresa**, sua aplicabilidade permanece desconhecida. Nesse caso, o requisito fica fora do cálculo de readiness e é acompanhado separadamente como uma pendência de aplicabilidade.

Se já sabemos que o requisito é avaliável, mas ainda não sabemos **se a empresa o atende**, sua avaliação pode ficar como **Desconhecido**. Nesse caso, ele participa do cálculo com peso zero.

Em outras palavras:

**Não sabemos se se aplica**  
→ pendência de aplicabilidade; ainda não entra no score.

**Sabemos que se aplica, mas não sabemos se está atendido**  
→ entra no score como Desconhecido.

Essa distinção impede que uma condição ainda não resolvida seja tratada como uma falha da empresa.

---

## Como o score é calculado hoje

!!! info "Disponível no MVP"

O cálculo atual usa os pesos dos requisitos avaliáveis:

`readiness = soma dos pesos ÷ quantidade de requisitos avaliáveis × 100`

Considere uma análise com:

- 7 requisitos **Atendidos**;
- 2 requisitos **Parciais**;
- 1 requisito **Faltando**.

O cálculo será:

`(7 × 1,0 + 2 × 0,5 + 1 × 0,0) ÷ 10 × 100 = 80%`

A readiness dessa análise é **80%**.

Se não existir nenhum requisito avaliável, o motor não força um percentual artificial: o score permanece sem valor até que exista informação suficiente para calculá-lo.

---

## Readiness é determinística

A IA pode ajudar a interpretar exigências, identificar condições, encontrar evidências e obter as informações necessárias para avaliar requisitos.

**Ela não escolhe o score.**

Depois que as avaliações são conhecidas, regras determinísticas calculam a readiness.

> **Mesmos requisitos + mesmas avaliações = mesma readiness.**

Isso torna o resultado reproduzível e evita que duas execuções da IA produzam percentuais diferentes para exatamente a mesma situação conhecida.

---

## Readiness não é probabilidade de aprovação

O Supplier Ready conhece as exigências que foram informadas e a situação registrada para cada requisito. Ele não controla a decisão final do cliente.

Um cliente pode considerar informações adicionais, realizar verificações próprias ou tomar decisões que não estavam expressas nas exigências analisadas.

Por isso:

> **80% de readiness significa progresso na preparação. Não 80% de chance de aprovação.**

A readiness ajuda sua empresa a entender o que já foi resolvido e onde ainda existem gaps. Ela não promete qual será a decisão do cliente.

---

## Readiness e Ready não são a mesma coisa

### Readiness

É uma **medida de progresso**.

Responde:

> **Quanto do que conseguimos avaliar já está resolvido?**

### Ready

É um **estado de conclusão** que estamos construindo para o produto.

Responde:

> **Existe algo que ainda impede minha empresa de avançar?**

!!! note "Em desenvolvimento — experiência do produto"
    O motor atual calcula readiness, mas ainda não possui um estado de domínio `Ready`. A definição e as regras finais desse estado ainda serão implementadas e validadas.

Conceitualmente, queremos que **Ready** signifique que tudo que se aplica e precisa ser resolvido foi resolvido — e não simplesmente que um número atingiu determinado percentual.

---

## Uma readiness alta ainda pode esconder um bloqueio

Imagine uma análise com muitos requisitos:

**19 requisitos atendidos**  
**1 requisito obrigatório faltando**

A readiness pode estar muito próxima de 100%, mas ainda existe algo concreto impedindo a conclusão do processo.

É por isso que o objetivo do Supplier Ready não é apenas aumentar um percentual.

O objetivo é tornar os **bloqueios restantes visíveis e acionáveis** até que possam ser resolvidos.

---

## O caminho até o Ready

O modelo mental é:

**Requisitos conhecidos**  
↓

**Aplicabilidade**  
↓

**Avaliação de cada requisito**  
↓

**Readiness**  
↓

**Bloqueios restantes?**  
↓

**Ready**

A readiness mostra o progresso. Ready representa a conclusão.

> **Readiness responde: quanto já resolvemos?**  
> **Ready responde: existe algo que ainda impede avançar?**
