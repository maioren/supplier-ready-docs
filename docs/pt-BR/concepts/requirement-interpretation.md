# Interpretação de requisitos

## Interpretar não é completar o que o cliente não disse.

O Supplier Ready usa IA para transformar exigências recebidas em requisitos estruturados. Mas o objetivo não é produzir a resposta mais provável.

O objetivo é produzir uma interpretação **útil, rastreável e defensável com base na fonte**.

Isso significa que uma boa interpretação precisa preservar aquilo que sabemos, deixar explícito aquilo que depende de uma condição e reconhecer quando a fonte não oferece informação suficiente para concluir.

> **A IA ajuda a interpretar. A fonte continua sendo a verdade.**

---

## O que significa interpretar um requisito

Para cada requisito candidato, o Supplier Ready tenta responder algumas perguntas fundamentais.

### 1. O que está sendo exigido?

A primeira tarefa é identificar a obrigação, expectativa ou informação concreta presente na fonte.

Uma mesma frase pode conter mais de um requisito. Quando isso acontece, separar os itens permite avaliar cada um de forma independente.

### 2. Isso é realmente obrigatório?

Nem toda frase em um documento de homologação estabelece uma obrigação.

O Supplier Ready precisa distinguir linguagem obrigatória de recomendações, orientações ou trechos que não permitem determinar a obrigatoriedade com segurança.

### 3. Existe alguma condição?

Expressões como **“quando aplicável”**, **“caso possua funcionários”** ou **“para atividades regulamentadas”** mudam o significado de um requisito.

Essas condições precisam permanecer associadas ao requisito. Removê-las pode transformar uma obrigação condicional em uma obrigação universal que o cliente nunca estabeleceu.

### 4. Temos evidência para essa interpretação?

Uma conclusão importante deve permanecer ligada ao trecho da fonte que a sustenta.

A evidência permite entender não apenas **o que** o Supplier Ready interpretou, mas também **por que** chegou àquela interpretação.

### 5. Existe informação suficiente?

Nem sempre.

Quando a fonte não permite concluir com segurança, a resposta correta pode ser **não concluir ainda**.

Essa incerteza deve permanecer explícita até que exista informação suficiente para resolvê-la.

---

## Confiança não é verdade

Um modelo de IA pode considerar uma interpretação altamente provável e ainda assim estar errado.

Por isso, **confiança nunca substitui evidência**.

A confiança é um sinal que ajuda o Supplier Ready a avaliar quanto cuidado uma interpretação merece. Ela não transforma uma inferência em fato e não substitui o trecho da fonte que sustenta a conclusão.

!!! info "Princípio de produto"
    Uma interpretação com alta confiança e sem suporte adequado na fonte não deve ser tratada como uma obrigação confirmada do cliente.

---

## O que a IA pode — e o que ela não pode — fazer

### A IA pode

Organizar informações, separar exigências compostas, classificar requisitos, relacionar condições, localizar evidências e identificar ambiguidades.

### A IA pode sugerir

Uma interpretação quando existe suporte razoável na fonte, desde que a evidência e qualquer incerteza relevante permaneçam explícitas.

### A IA não pode

Transformar conhecimento geral, costume de mercado ou uma suposição plausível em uma obrigação atribuída ao cliente sem suporte na fonte.

---

## Um exemplo: condição não é obrigação universal

Considere a seguinte exigência:

> **Apresentar licença ambiental, quando exigida pela legislação aplicável.**

Uma interpretação inadequada seria:

> ❌ **Licença ambiental — obrigatória**

Essa conclusão remove uma parte essencial da fonte: a condição.

Uma interpretação melhor preserva essa informação:

> ✓ **Licença ambiental — condicional**  
> **Condição:** quando exigida pela legislação aplicável.  
> **Evidência:** trecho original da exigência.  
> **Aplicabilidade:** a determinar.

A fonte estabelece que a licença deve ser apresentada **se determinada condição for verdadeira**. Ela não informa, sozinha, se essa condição é verdadeira para a sua empresa.

---

## Incerteza é um estado válido do produto

Não saber ainda não significa que a interpretação falhou.

Se a fonte não permite determinar se uma condição se aplica à empresa, manter essa informação como **desconhecida** é mais confiável do que produzir uma resposta baseada em suposição.

No exemplo da licença ambiental, pode ser necessário entender a atividade da empresa, sua localização ou outro contexto antes de determinar a aplicabilidade do requisito.

O fluxo passa a ser:

**Fonte**  
↓ interpretação

**Requisito condicional**  
↓ informação insuficiente

**Incerteza**  
↓ esclarecimento

**Nova informação**  
↓ reavaliação

**Aplicabilidade determinada**

Assim, a incerteza não é escondida: ela se transforma em uma próxima ação.

---

## Quando a dúvida vira esclarecimento

Se uma informação necessária para continuar a análise não está disponível na fonte ou no contexto conhecido da empresa, o Supplier Ready pode transformar essa lacuna em uma pergunta explícita.

Em vez de assumir:

> “Sua empresa precisa de licença ambiental.”

podemos precisar perguntar:

> **A atividade da sua empresa está sujeita a licenciamento ambiental segundo a legislação aplicável?**

A resposta adiciona informação à análise e permite reavaliar o requisito sem alterar aquilo que o cliente originalmente informou.

> **Quando não souber, o Supplier Ready não deve adivinhar. Deve perguntar.**

---

## Quatro princípios para uma interpretação confiável

**Fonte antes da inferência.**  
Uma obrigação atribuída ao cliente precisa estar sustentada pelo que ele informou.

**Condição antes da conclusão.**  
Uma condição relevante precisa ser preservada antes de decidir se um requisito se aplica.

**Incerteza antes da suposição.**  
Quando a informação não é suficiente, reconhecer a dúvida é melhor do que completar a lacuna.

**Esclarecimento antes da invenção.**  
Quando uma resposta é necessária para continuar, o caminho é perguntar — não presumir.

Esses princípios permitem que a IA seja útil sem esconder os limites da interpretação.

[Entenda como a readiness é calculada →](readiness.md){ .md-button .md-button--primary }
