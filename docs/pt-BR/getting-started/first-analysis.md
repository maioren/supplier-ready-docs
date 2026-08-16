# Sua primeira análise

## Comece pelas exigências que você recebeu.

Toda análise no Supplier Ready parte de uma fonte: aquilo que seu cliente efetivamente informou como condição para cadastro ou homologação.

Nesta primeira experiência, vamos acompanhar como esse conteúdo deixa de ser apenas texto e passa a se tornar uma estrutura de requisitos que pode ser analisada com rastreabilidade.

!!! info "Disponível no MVP"
    O motor atual já permite criar uma análise a partir do CNPJ da empresa e do texto com as exigências recebidas, interpretar requisitos, preservar evidências da fonte, tratar esclarecimentos e calcular readiness. A experiência visual integrada para realizar todo esse fluxo ainda está sendo construída.

## Um exemplo para acompanhar

Imagine que seu cliente tenha enviado a seguinte exigência:

> **A empresa deverá apresentar comprovante de inscrição no CNPJ válido e, quando aplicável, registro no conselho profissional competente.**

É uma frase curta, mas ela contém mais de uma informação importante. O Supplier Ready precisa separar essas informações sem transformar condições em certezas.

---

## 1. A fonte entra na análise

!!! info "Disponível no MVP"

A análise começa com a identificação da sua empresa e o conteúdo recebido do cliente.

O texto original é a referência para determinar o que foi efetivamente solicitado. Ele não deve ser substituído silenciosamente por uma interpretação da IA.

No exemplo, a fonte continua sendo:

> A empresa deverá apresentar comprovante de inscrição no CNPJ válido e, quando aplicável, registro no conselho profissional competente.

!!! note "Em desenvolvimento — experiência do produto"
    A interface que permitirá criar e acompanhar uma análise de ponta a ponta ainda está sendo construída. Por isso, esta documentação descreve o comportamento do produto sem presumir botões ou telas que ainda não existem.

---

## 2. O Supplier Ready identifica os requisitos

!!! info "Disponível no MVP"

O motor interpreta o conteúdo e organiza as exigências em requisitos individuais.

Conceitualmente, nosso exemplo pode resultar em algo como:

**Comprovante de inscrição no CNPJ válido**  
Obrigatório

**Registro no conselho profissional competente**  
Condicional — quando aplicável

Separar os requisitos é importante porque cada um pode ter uma condição, uma evidência e uma situação diferente dentro da sua empresa.

---

## 3. Cada interpretação continua ligada à fonte

!!! info "Disponível no MVP"

O Supplier Ready preserva o trecho da fonte que sustenta cada requisito identificado.

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

O Supplier Ready deve preservar essa incerteza em vez de assumir uma resposta.

A análise pode então precisar de um esclarecimento como:

> **Precisamos esclarecer**  
> O registro no conselho profissional se aplica à atividade da sua empresa?

O motor do MVP já possui o fluxo para planejar, listar e responder esclarecimentos.

> **Quando não souber, o Supplier Ready não deve adivinhar. Deve perguntar.**

---

## 5. A realidade da sua empresa entra na análise

!!! note "Em desenvolvimento — experiência do produto"

Depois de entender o que o cliente exige, precisamos confrontar esses requisitos com a realidade da sua empresa.

Para o exemplo, algumas perguntas passam a importar:

- O CNPJ informado está válido?
- A atividade da empresa exige registro em conselho profissional?
- Se exige, a empresa possui o registro necessário?

É essa comparação que permite transformar requisitos em gaps concretos, em vez de apenas produzir uma lista de documentos.

---

## 6. A análise caminha para Readiness

!!! info "Disponível no MVP"
    O cálculo determinístico de readiness já existe no motor. A experiência integrada que produzirá automaticamente todas as avaliações necessárias para o usuário ainda está em desenvolvimento.

Conforme os requisitos são avaliados, eles podem assumir situações como:

- **Atendido** — a empresa cumpre o requisito.
- **Parcial** — o requisito foi atendido apenas em parte.
- **Faltando** — existe uma ação necessária.
- **Desconhecido** — ainda não há informação suficiente.
- **Não aplicável** — o requisito não se aplica à empresa.

Requisitos cuja aplicabilidade ainda não foi determinada permanecem pendentes até que exista informação suficiente para avaliá-los.

A readiness transforma essas avaliações em uma visão objetiva do quanto já está resolvido e do que ainda impede a empresa de avançar.

---

## 7. O objetivo é chegar ao Ready

!!! note "Em desenvolvimento — experiência do produto"

O resultado final que estamos construindo não é apenas uma lista interpretada de exigências.

Queremos que uma análise consiga responder, de forma simples:

**O que meu cliente pediu?**  
**O que minha empresa já atende?**  
**O que ainda falta?**  
**O que precisa ser esclarecido?**

Quando tudo que precisa ser resolvido estiver resolvido, sua empresa estará **Ready** para avançar com aquele cliente.

---

## O que você viu nesta primeira análise

Uma exigência aparentemente simples pode conter múltiplos requisitos, condições e dúvidas. O Supplier Ready transforma esse conteúdo em uma estrutura que preserva a fonte, torna a incerteza explícita e prepara o caminho para identificar os gaps da sua empresa.

A experiência completa ainda está sendo construída, mas o núcleo que sustenta esse fluxo já está tomando forma no MVP.

[Entenda como os requisitos são interpretados →](../concepts/requirement-interpretation.md){ .md-button .md-button--primary }
