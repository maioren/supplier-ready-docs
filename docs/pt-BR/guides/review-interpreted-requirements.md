# Revisar requisitos interpretados

## Verifique o que foi entendido antes de usar a interpretação como base para decisões.

Depois que uma fonte é processada pelo Interpreter, o Supplier Ready produz requisitos estruturados. Revisar esse resultado significa conferir **o que foi identificado, como foi classificado, quais condições foram preservadas e qual evidência sustenta cada interpretação**.

!!! info "Disponível no MVP"
    O modelo e o Interpreter já produzem requisitos estruturados no motor. Essa capacidade ainda não está exposta como uma experiência pública completa na API/UI atual.

## 1. Comece pelo nome do requisito

Confira se `name` representa de forma fiel a exigência identificada. O campo `canonical_name`, quando presente, oferece uma forma normalizada de representar o mesmo conceito.

A normalização não deve mudar aquilo que o cliente pediu.

## 2. Revise categoria e tipo

Cada requisito pode receber uma `category` e um `type`.

As categorias atuais incluem, entre outras, CORPORATE, TAX, LABOR, FINANCIAL, TECHNICAL, LICENSING, BANKING, COMPLIANCE, DECLARATION e IDENTITY.

Os tipos atuais incluem DOCUMENT, DATA, DECLARATION, CERTIFICATION, POLICY, ACCEPTANCE e CAPABILITY.

Esses campos ajudam a organizar a análise; eles não substituem a evidência da fonte.

## 3. Confira obrigatoriedade e condição

O resultado informa `mandatory`, `conditional` e, quando necessário, `condition`.

Se `conditional` for verdadeiro, o modelo exige uma condição não vazia. Se o requisito não for condicional, `condition` deve permanecer ausente.

Uma condição relevante nunca deve desaparecer apenas para simplificar a interpretação.

## 4. Verifique a aplicabilidade

A aplicabilidade pode ser:

- `APPLICABLE` — sabemos que o requisito se aplica;
- `NOT_APPLICABLE` — sabemos que não se aplica;
- `UNKNOWN` — ainda falta informação para decidir.

`UNKNOWN` é um estado válido. Quando a aplicabilidade depende de contexto que ainda não possuímos, a próxima ação pode ser um esclarecimento.

## 5. Volte à evidência

Cada requisito interpretado possui `source_quote`.

Use esse trecho para responder:

> **A fonte realmente sustenta a interpretação apresentada?**

A evidência deve permitir verificar a conclusão; não serve apenas como uma citação decorativa.

## 6. Trate confiança como sinal, não como verdade

`confidence` varia de 0 a 1 e representa um sinal da interpretação do modelo.

Uma confiança alta não transforma uma inferência sem evidência em fato. Quando confiança e evidência apontarem em direções diferentes, a fonte deve prevalecer.

## 7. Procure incertezas, esclarecimentos e avisos

Além de `requirements`, o resultado do Interpreter pode conter:

- `uncertainties` — ambiguidades, contexto ausente ou detalhes sem suporte;
- `clarifications` — perguntas que podem ser necessárias para continuar;
- `warnings` — alertas produzidos durante a interpretação.

Uma revisão não está completa se olhar apenas para a lista de requisitos e ignorar esses sinais.

## Resultado esperado

Ao terminar a revisão, você deve conseguir responder para cada requisito:

**O que foi interpretado?**  
**Existe uma condição?**  
**Sabemos se se aplica?**  
**Qual evidência sustenta a conclusão?**  
**Existe alguma incerteza que ainda precisa ser resolvida?**

[Resolver esclarecimentos →](resolve-clarifications.md){ .md-button .md-button--primary }
