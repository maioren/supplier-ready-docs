# Acompanhar a Readiness

## Use a readiness para acompanhar progresso — não para prever aprovação.

A readiness resume o estado das avaliações conhecidas em um score determinístico. Acompanhar esse número ajuda a perceber evolução, mas o percentual precisa ser lido junto com as pendências da análise.

!!! info "Disponível no MVP"
    O cálculo de readiness já existe no motor. A API/UI pública para acompanhar sua evolução ainda não está disponível como experiência integrada.

## 1. Confira quantos requisitos são avaliáveis

O resultado informa `scoreable_count`: quantos requisitos efetivamente entraram no cálculo.

Requisitos não aplicáveis são excluídos. Requisitos cuja aplicabilidade ainda é desconhecida também ficam fora do denominador enquanto essa condição não for resolvida.

## 2. Leia o score

Os pesos atuais são:

- `SATISFIED` = 1,0;
- `PARTIAL` = 0,5;
- `MISSING` = 0,0;
- `UNKNOWN` = 0,0.

O score é:

`somatório dos pesos ÷ quantidade de requisitos avaliáveis × 100`

Se não houver requisito avaliável, o score é `null` em vez de um percentual artificial.

## 3. Leia os contadores junto com o percentual

O resultado também informa quantidades de itens atendidos, parciais, faltando e desconhecidos, além de:

- `pending_applicability_count` — requisitos cuja aplicabilidade ainda precisa ser determinada;
- `excluded_not_applicable_count` — requisitos excluídos por não se aplicarem.

Esses números explicam o que existe por trás do percentual.

## 4. Não interprete readiness como probabilidade

Uma readiness de 80% significa progresso segundo as avaliações conhecidas e a fórmula atual.

**Não significa 80% de chance de o cliente aprovar sua empresa.**

A decisão do cliente pode depender de verificações ou informações que não fazem parte da análise.

## 5. Procure bloqueios antes de comemorar o percentual

Uma análise pode ter readiness muito alta e ainda possuir um requisito faltando. Por isso, acompanhe o score junto com os estados e gaps restantes.

!!! note "Ready ainda está em desenvolvimento"
    O motor atual calcula readiness, mas ainda não possui um estado de domínio `Ready`. Nossa direção é que Ready represente ausência de bloqueios relevantes, e não apenas `score == 100`.

## Resultado esperado

Ao acompanhar readiness, você deve conseguir responder:

**Quanto já resolvemos?**  
**Quantos itens ainda estão faltando ou desconhecidos?**  
**Existem condições cuja aplicabilidade ainda precisa ser resolvida?**  
**O que ainda impede a análise de chegar ao Ready?**

[Entenda o conceito de Readiness](../concepts/readiness.md){ .md-button }
