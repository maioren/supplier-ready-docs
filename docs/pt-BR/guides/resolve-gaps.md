# Entender e resolver gaps

## Transforme o que falta em próximas ações.

Um **gap** é a distância entre aquilo que um requisito aplicável exige e a situação atual da empresa.

O objetivo não é apenas apontar problemas. É tornar visível **o que ainda precisa acontecer para a análise avançar**.

!!! note "Em desenvolvimento — experiência do produto"
    O MVP já possui estados de avaliação e cálculo de readiness, mas `Gap` ainda não existe como objeto de domínio próprio nem como fluxo operacional completo.

## 1. Procure o que ainda não está resolvido

Na direção atual do produto, gaps podem surgir principalmente quando um requisito está:

- `PARTIAL` — algo já foi atendido, mas ainda falta uma parte;
- `MISSING` — existe uma ação necessária;
- `UNKNOWN` — falta informação para determinar a situação;
- com aplicabilidade `UNKNOWN` — falta esclarecer se o requisito se aplica.

Essas situações não são equivalentes e não devem produzir a mesma próxima ação.

## 2. Diferencie ação de esclarecimento

Um requisito `MISSING` tende a apontar para algo que a empresa precisa providenciar.

Uma aplicabilidade `UNKNOWN`, por outro lado, pede primeiro uma decisão: **isso realmente se aplica?**

Resolver a dúvida antes de executar uma ação evita trabalho desnecessário.

## 3. Priorize bloqueios reais

Uma readiness alta não garante que não exista um requisito importante faltando.

Por isso, a futura experiência de gaps deverá destacar bloqueios e próximas ações, em vez de ordenar o trabalho apenas pelo percentual de readiness.

## 4. Atualize a análise conforme a realidade muda

Quando uma pendência for resolvida, sua avaliação deverá ser atualizada. A readiness poderá então ser recalculada a partir do novo estado conhecido.

!!! note "Direção de produto"
    A modelagem final de gap, prioridade, responsável, prazo e ação recomendada ainda não foi implementada. Esta página descreve o modelo mental que orienta a experiência em desenvolvimento.

## Resultado esperado

Ao trabalhar sobre gaps, queremos que a análise deixe de responder apenas **“o que está errado?”** e passe a responder:

> **O que falta, por que falta e qual é a próxima decisão ou ação necessária?**

[Acompanhar a Readiness →](track-readiness.md){ .md-button .md-button--primary }
