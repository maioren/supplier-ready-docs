# Sua primeira análise

## Comece pelas exigências que você recebeu.

Toda análise no Supplier Ready parte de uma fonte: aquilo que seu cliente efetivamente informou como condição para cadastro ou homologação.

Nesta primeira experiência, vamos acompanhar como esse conteúdo deixa de ser apenas texto e passa a se tornar uma estrutura de requisitos que pode ser analisada com rastreabilidade.

!!! info "Disponível no MVP"
    A primeira experiência web já permite informar o CNPJ, colar o texto das exigências, executar a interpretação, responder esclarecimentos de aplicabilidade e revisar os requisitos com rastreabilidade até a fonte. A avaliação da realidade da empresa e a readiness integrada permanecem como próximas etapas do produto.

## Um exemplo para acompanhar

Imagine que seu cliente tenha enviado a seguinte exigência:

> **A empresa deverá apresentar comprovante de inscrição no CNPJ válido e, quando aplicável, registro no conselho profissional competente.**

É uma frase curta, mas ela contém mais de uma informação importante. O Supplier Ready precisa separar essas informações sem transformar condições em certezas.

---

## 1. A fonte entra na análise

!!! info "Disponível no MVP"

A análise começa com a identificação da sua empresa e o conteúdo recebido do cliente.

Na primeira experiência web, você informa o CNPJ da empresa e cola o texto original das exigências antes de iniciar a análise.

O texto original é a referência para determinar o que foi efetivamente solicitado. Ele não deve ser substituído silenciosamente por uma interpretação da IA.

No exemplo, a fonte continua sendo:

> A empresa deverá apresentar comprovante de inscrição no CNPJ válido e, quando aplicável, registro no conselho profissional competente.

---

## 2. O Supplier Ready identifica os requisitos

!!! info "Disponível no MVP"

Ao iniciar a análise, a jornada de produto cria o registro e executa o Interpreter. O conteúdo é organizado em requisitos individuais.

Conceitualmente, nosso exemplo pode resultar em algo como:

**Comprovante de inscrição no CNPJ válido**  
Obrigatório

**Registro no conselho profissional competente**  
Condicional — quando aplicável

Separar os requisitos é importante porque cada um pode ter uma condição, uma evidência e uma situação diferente dentro da sua empresa.

---

## 3. Cada interpretação continua ligada à fonte

!!! info "Disponível no MVP"

O Supplier Ready preserva o trecho da fonte que sustenta cada requisito identificado e a jornada atual também devolve a posição inicial e final desse trecho no texto recebido.

Isso permite diferenciar claramente:

**O que o cliente informou**  
> “quando aplicável, registro no conselho profissional competente”

**Como o Supplier Ready interpretou**  
> Registro no conselho profissional — requisito condicional.

A interpretação ajuda a organizar a informação. **A fonte continua sendo a verdade.**

---

## 4. Condições não viram fatos

!!! info "Disponível no MVP"

A expressão **“quando aplicável”** não informa, sozinha, se o registro no conselho profissional é obrigatório para a sua empresa.

O Supplier Ready preserva essa incerteza em vez de assumir uma resposta.

Quando existe uma condição cuja aplicabilidade ainda é desconhecida, a experiência atual apresenta um esclarecimento e permite responder **Sim** ou **Não**.

No contrato da API, essas respostas são representadas por `YES` e `NO` e resolvem a aplicabilidade para `APPLICABLE` ou `NOT_APPLICABLE`.

> **Quando não souber, o Supplier Ready não deve adivinhar. Deve perguntar.**

!!! warning "READY nesta etapa não é o Ready final"
    Quando todos os esclarecimentos de interpretação são resolvidos, a API de produto usa o estado `READY`. Esse estado significa apenas que não existem esclarecimentos pendentes; não significa que todos os requisitos estejam atendidos ou que a empresa já esteja pronta para homologação.

---

## 5. Revise o que foi entendido

!!! info "Disponível no MVP"

Depois que não existem esclarecimentos pendentes, a experiência apresenta os requisitos interpretados.

Para cada requisito, a jornada atual consegue mostrar informações como:

- nome;
- categoria e tipo;
- aplicabilidade;
- condição, quando existir;
- trecho da fonte;
- posição desse trecho no texto original.

A análise também mantém incertezas explícitas para que não sejam confundidas com fatos.

---

## 6. A realidade da sua empresa entra na análise

!!! note "Em desenvolvimento — experiência do produto"

Depois de entender o que o cliente exige, precisamos confrontar esses requisitos com a realidade da sua empresa.

Para o exemplo, algumas perguntas passam a importar:

- O CNPJ informado está válido?
- A atividade da empresa exige registro em conselho profissional?
- Se exige, a empresa possui o registro necessário?

É essa comparação que permitirá transformar requisitos em gaps concretos, em vez de apenas produzir uma lista de documentos.

A experiência pública atual ainda não coleta de ponta a ponta as evidências de atendimento necessárias para produzir essa avaliação.

---

## 7. A análise caminha para Readiness

!!! info "Disponível no MVP — motor"
    O cálculo determinístico de readiness já existe no motor, mas ainda não está exposto na jornada web/API de produto atual porque depende das avaliações dos requisitos.

Quando essas avaliações estiverem disponíveis, elas podem assumir situações como:

- **Atendido** — a empresa cumpre o requisito.
- **Parcial** — o requisito foi atendido apenas em parte.
- **Faltando** — existe uma ação necessária.
- **Desconhecido** — ainda não há informação suficiente.
- **Não aplicável** — o requisito não se aplica à empresa.

Requisitos cuja aplicabilidade ainda não foi determinada permanecem pendentes até que exista informação suficiente para avaliá-los.

A readiness transforma essas avaliações em uma visão objetiva do quanto já está resolvido.

---

## 8. O objetivo continua sendo chegar ao Ready

!!! note "Em desenvolvimento — experiência do produto"

O resultado final que estamos construindo não é apenas uma lista interpretada de exigências.

Queremos que uma análise consiga responder, de forma simples:

**O que meu cliente pediu?**  
**O que minha empresa já atende?**  
**O que ainda falta?**  
**O que precisa ser esclarecido?**

O estado final de produto **Ready** ainda será definido e implementado sobre as etapas de avaliação, gaps e bloqueios. Ele não deve ser confundido com `ProductAnalysisState.READY`, usado hoje apenas pela etapa de interpretação.

---

## O que você viu nesta primeira análise

Uma exigência aparentemente simples pode conter múltiplos requisitos, condições e dúvidas. O Supplier Ready já consegue transformar esse conteúdo em uma estrutura rastreável, resolver condições de aplicabilidade e apresentar o que foi entendido sem esconder incertezas.

O próximo grande passo da experiência é conectar essa interpretação à realidade da empresa para avaliar atendimento, gaps e readiness.

[Entenda como os requisitos são interpretados →](../concepts/requirement-interpretation.md){ .md-button .md-button--primary }
