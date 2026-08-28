# Supplier Ready

## Saiba o que falta para sua empresa estar pronta para um novo cliente.

Transforme exigências de cadastro e homologação em um caminho claro. Comece entendendo com precisão o que o cliente pediu e avance até saber o que sua empresa já atende e o que ainda precisa resolver.

[Comece por aqui](getting-started/index.md){ .md-button .md-button--primary }
[Entenda o produto](concepts/index.md){ .md-button }

---

## Homologar um novo cliente não deveria virar uma corrida contra o tempo.

As exigências podem chegar em documentos, e-mails, planilhas, checklists e portais. Cada cliente pede informações diferentes, usa termos diferentes e organiza o processo de um jeito diferente.

Antes mesmo de começar a providenciar o que falta, alguém precisa entender o que realmente está sendo pedido.

**Quais documentos são obrigatórios? Existe alguma exigência que só se aplica em determinadas situações? O que já temos? O que ainda precisa ser providenciado?**

Esse trabalho normalmente acontece de forma manual, espalhado entre pessoas, arquivos e sistemas — e muitas vezes só fica claro que algo está faltando quando o prazo já está apertado.

**O resultado é um processo que depende de interpretação manual, conhecimento espalhado pela empresa e acompanhamento constante — justamente quando sua empresa precisa responder rápido e com confiança.**

---

## Das exigências do cliente ao Ready.

### 1. Traga as exigências do seu cliente

Na primeira experiência do MVP, informe sua empresa pelo CNPJ e cole o texto original com as condições para cadastro ou homologação.

### 2. Entenda o que realmente está sendo pedido

O Supplier Ready organiza as exigências em requisitos, preserva condições e incertezas e mantém cada interpretação ligada ao trecho correspondente da fonte.

### 3. Esclareça o que depende de contexto

Quando uma condição não permite determinar com segurança se um requisito se aplica, o Supplier Ready mantém a dúvida explícita e permite resolvê-la antes de seguir.

### 4. Compare com a realidade da sua empresa

A próxima camada do produto conecta os requisitos interpretados às informações e evidências da sua empresa para determinar o que está atendido e o que ainda exige ação.

### 5. Acompanhe o que falta para estar pronto

O motor já possui o cálculo determinístico de **readiness** a partir das avaliações dos requisitos. A experiência integrada de avaliação, gaps e readiness continua em desenvolvimento.

---

## Entenda não apenas a resposta, mas de onde ela veio.

O Supplier Ready usa IA para ajudar a interpretar as exigências do seu cliente sem transformar suposições em fatos.

**Rastreável até a fonte**  
Veja o trecho original que sustenta cada requisito identificado.

**Explícito quando existe dúvida**  
Condições e ambiguidades permanecem visíveis até que possam ser esclarecidas.

**Sem inventar exigências**  
Uma inferência da IA não se transforma silenciosamente em uma obrigação para sua empresa.

> **Quando não souber, o Supplier Ready não deve adivinhar. Deve perguntar.**

A IA ajuda a interpretar. A fonte continua sendo a verdade.

---

## Seu cliente pode falar outro idioma. O Supplier Ready também deve falar o seu.

O produto e sua documentação estão sendo preparados desde o início para português, inglês e espanhol.

Nossa direção é permitir que exigências recebidas em um idioma sejam trabalhadas em outro sem perder a fonte original nem sua rastreabilidade.

!!! note "Direção de produto"
    A documentação já possui versões em português, inglês e espanhol. A experiência multilíngue de ponta a ponta do produto ainda deve ser tratada como direção em desenvolvimento, não como capacidade completa do MVP atual.

---

## O que já funciona no MVP

A primeira jornada utilizável já consegue:

- receber CNPJ e texto das exigências;
- criar e processar uma análise;
- interpretar requisitos com IA;
- preservar o trecho e a posição da fonte associados a cada requisito;
- manter incertezas explícitas;
- pedir esclarecimentos para condições de aplicabilidade;
- atualizar a aplicabilidade após respostas Sim/Não;
- apresentar os requisitos interpretados quando não existem esclarecimentos pendentes.

Ela ainda **não avalia automaticamente se sua empresa possui os documentos ou evidências necessários**.

---

## Estamos construindo o Supplier Ready em camadas.

Depois de entender com confiança o que um novo cliente está exigindo, o produto avança para conectar essas exigências à realidade da empresa.

**Entender as exigências**  
O que o cliente realmente pediu?

↓

**Entender sua empresa**  
O que você já possui e o que já atende?

↓

**Identificar os gaps**  
O que falta, o que precisa de atenção e o que precisa ser esclarecido?

↓

**Chegar ao Ready**  
Existe algo que ainda impede sua empresa de avançar?

### Readiness e Ready são coisas diferentes

**Readiness** é a medida determinística de progresso que já existe no motor.

**Ready** é o estado final de produto que ainda estamos definindo e implementando sobre avaliações, gaps e bloqueios.

!!! warning "Não confunda com ProductAnalysisState.READY"
    A API da jornada de interpretação usa atualmente `READY` quando não existem esclarecimentos pendentes. Esse é um estado técnico daquela etapa e **não significa que a empresa esteja Ready para homologação**.

!!! note "Produto em desenvolvimento"
    Algumas capacidades já existem na primeira jornada web ou no motor; outras representam a direção do produto. A documentação indica essa diferença para não apresentar intenção futura como contrato atual.

---

## Continue pela documentação

Se esta é sua primeira visita, comece entendendo a jornada que já existe. Para contratos técnicos, consulte a Referência. Para acompanhar a direção do produto, veja também o que estamos construindo.

[Primeiros passos](getting-started/index.md){ .md-button .md-button--primary }
[API v0](reference/api-v0.md){ .md-button }
[O que estamos construindo](product/roadmap.md){ .md-button }

---

**Documentação do Supplier Ready**  
O produto está em desenvolvimento. Esta documentação evolui junto com as capacidades validadas do produto.
