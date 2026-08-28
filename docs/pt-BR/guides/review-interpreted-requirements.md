# Revisar requisitos interpretados

## Verifique o que foi entendido antes de usar a interpretação como base para decisões.

Depois que uma fonte é processada pelo Interpreter, o Supplier Ready produz requisitos estruturados. Revisar esse resultado significa conferir **o que foi identificado, como foi classificado, quais condições foram preservadas e qual evidência sustenta cada interpretação**.

!!! info "Disponível no MVP"
    A jornada de produto já cria e processa uma análise, resolve esclarecimentos de aplicabilidade e apresenta os requisitos interpretados com rastreabilidade até a fonte. O contrato completo do `RequirementCandidate` contém campos adicionais que permanecem disponíveis na camada de domínio.

## 1. Comece pelo nome do requisito

Confira se `name` representa de forma fiel a exigência identificada.

No contrato completo do Interpreter, `canonical_name`, quando presente, oferece uma forma normalizada de representar o mesmo conceito. A resposta atual da jornada `/v0/product/analyses` apresenta `name`, mas não expõe `canonical_name`.

A normalização não deve mudar aquilo que o cliente pediu.

## 2. Revise categoria e tipo

Cada requisito apresentado pela jornada de produto possui uma `category` e um `type`.

As categorias atuais incluem, entre outras, CORPORATE, TAX, LABOR, FINANCIAL, TECHNICAL, LICENSING, BANKING, COMPLIANCE, DECLARATION e IDENTITY.

Os tipos atuais incluem DOCUMENT, DATA, DECLARATION, CERTIFICATION, POLICY, ACCEPTANCE e CAPABILITY.

Esses campos ajudam a organizar a análise; eles não substituem a evidência da fonte.

## 3. Confira a condição

A resposta da jornada de produto informa `condition` quando o requisito depende de uma condição.

No contrato completo do `RequirementCandidate`, essa relação é representada também por `conditional`: quando `conditional` é verdadeiro, o modelo exige uma condição não vazia; quando é falso, `condition` deve ser `null`.

Uma condição relevante nunca deve desaparecer apenas para simplificar a interpretação.

## 4. Verifique a aplicabilidade

A aplicabilidade pode ser:

- `APPLICABLE` — sabemos que o requisito se aplica;
- `NOT_APPLICABLE` — sabemos que não se aplica;
- `UNKNOWN` — ainda falta informação para decidir.

Na jornada de produto, requisitos condicionais podem permanecer `UNKNOWN` enquanto houver um esclarecimento pendente. Depois da resposta, sua aplicabilidade é atualizada para `APPLICABLE` ou `NOT_APPLICABLE`.

`UNKNOWN` é um estado válido e não deve ser tratado como `NOT_APPLICABLE`.

## 5. Volte à evidência e à posição na fonte

Cada requisito apresentado pela jornada possui:

- `source_quote` — trecho da fonte que sustenta a interpretação;
- `source_start` — posição inicial desse trecho;
- `source_end` — posição final.

Use esses dados para responder:

> **A fonte realmente sustenta a interpretação apresentada?**

A evidência deve permitir verificar a conclusão; não serve apenas como uma citação decorativa.

## 6. Entenda os campos que pertencem ao contrato completo

O `RequirementCandidate` usado internamente pelo Interpreter contém informações adicionais, entre elas `canonical_name`, `mandatory`, `blocking`, `conditional`, `issuer` e `confidence`.

Esses campos fazem parte do modelo de domínio atual, mas não são todos projetados na resposta `RequirementView` da jornada de produto.

Por isso, ao revisar a experiência atual, não presuma que todo campo do modelo interno esteja disponível na interface pública correspondente.

[Consultar Modelo de requisito →](../reference/requirement-model.md)

## 7. Procure incertezas e esclarecimentos pendentes

A resposta da jornada de produto também apresenta:

- `uncertainties` — ambiguidades, contexto ausente ou detalhes sem suporte;
- `pending_clarifications` — perguntas de aplicabilidade que ainda precisam de resposta.

O `InterpreterResult` completo possui ainda `clarifications` e `warnings`, mas esses campos não são projetados diretamente em `ProductAnalysisResultResponse`.

Uma revisão não está completa se olhar apenas para a lista de requisitos e ignorar os sinais que continuam pendentes.

## Resultado esperado

Ao terminar a revisão, você deve conseguir responder para cada requisito:

**O que foi interpretado?**  
**Existe uma condição?**  
**Sabemos se se aplica?**  
**Qual trecho da fonte sustenta a conclusão?**  
**Existe alguma incerteza ou esclarecimento que ainda precisa ser resolvido?**

[Resolver esclarecimentos →](resolve-clarifications.md){ .md-button .md-button--primary }
