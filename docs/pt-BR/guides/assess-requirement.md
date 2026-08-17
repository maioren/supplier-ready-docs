# Avaliar um requisito

## Determine a situação do requisito com base na realidade da empresa.

Depois de entender o que o cliente exige e determinar se o requisito se aplica, a análise precisa confrontar essa exigência com a situação da empresa.

!!! note "Em desenvolvimento — experiência do produto"
    O domínio do MVP já define os estados usados pela readiness, mas ainda não existe uma experiência pública completa para coletar evidências da empresa e produzir essas avaliações de ponta a ponta.

## 1. Confirme a aplicabilidade

Antes de avaliar atendimento, determine se o requisito é `APPLICABLE`, `NOT_APPLICABLE` ou ainda `UNKNOWN`.

Se a aplicabilidade ainda for desconhecida, resolva a condição antes de tratar o requisito como atendido ou faltando.

## 2. Reúna a informação da empresa

A avaliação deve ser sustentada por informação da empresa capaz de responder se o requisito foi cumprido.

Esse é o ponto em que a futura **evidência de atendimento** se diferencia da evidência da exigência: uma mostra o que o cliente pediu; a outra sustenta a situação da empresa diante desse pedido.

## 3. Determine o estado

O domínio atual reconhece cinco estados:

- `SATISFIED` — atendido;
- `PARTIAL` — atendido parcialmente;
- `MISSING` — faltando;
- `UNKNOWN` — informação insuficiente;
- `NOT_APPLICABLE` — não aplicável.

Não use `UNKNOWN` como sinônimo de falha. Ele significa que ainda não existe informação suficiente para concluir.

## 4. Preserve a justificativa

A experiência que estamos construindo deverá permitir explicar por que um requisito recebeu determinado estado e qual informação da empresa sustenta essa avaliação.

!!! note "Ainda não disponível como fluxo completo"
    O modelo atual de `RequirementAssessment` registra identificador do requisito, status e aplicabilidade. O modelo completo de evidência de atendimento ainda será evoluído e validado.

## Resultado esperado

Uma avaliação confiável deve responder:

**Esse requisito se aplica?**  
**Qual é a situação atual?**  
**Que informação sustenta essa situação?**  
**Existe alguma ação ou informação ainda necessária?**

[Entender e resolver gaps →](resolve-gaps.md){ .md-button .md-button--primary }
