# Rastreabilidade e evidências

## Toda conclusão importante deve conseguir apontar de volta para sua origem.

O Supplier Ready não deve pedir que você simplesmente confie em uma interpretação produzida pela IA.

Sempre que uma conclusão for atribuída às exigências do cliente, queremos que seja possível entender **qual informação foi interpretada, qual trecho sustenta essa interpretação e de onde esse trecho veio**.

Rastreabilidade é o que permite sair de uma conclusão estruturada e voltar até aquilo que realmente foi informado.

---

## Fonte, evidência e rastreabilidade não são a mesma coisa

Esses três conceitos trabalham juntos, mas têm papéis diferentes.

### Fonte

É o conteúdo recebido do cliente: documento, texto, e-mail, planilha, checklist ou outra informação usada como origem da análise.

### Evidência

É a parte específica da fonte que sustenta uma interpretação ou conclusão.

### Rastreabilidade

É a capacidade de conectar a conclusão à sua evidência e, a partir dela, voltar à fonte original.

Em resumo:

**Fonte**  
↓ contém

**Evidência**  
↓ sustenta

**Conclusão**

E a rastreabilidade mantém esse caminho verificável nos dois sentidos.

---

## Um exemplo

Considere novamente a exigência:

> **A empresa deverá apresentar comprovante de inscrição no CNPJ válido e, quando aplicável, registro no conselho profissional competente.**

O Supplier Ready pode identificar:

**Requisito interpretado**  
Registro no conselho profissional competente.

**Classificação**  
Condicional.

**Evidência**  
> “quando aplicável, registro no conselho profissional competente”

A classificação **condicional** não aparece literalmente como um campo na fonte. Ela é uma interpretação estruturada produzida a partir da expressão **“quando aplicável”**.

A evidência permite que uma pessoa verifique por que essa interpretação foi produzida.

---

## Evidência não precisa conter a conclusão pronta

Uma evidência sustenta uma conclusão. Ela não precisa apresentar essa conclusão no mesmo formato usado pelo Supplier Ready.

O cliente provavelmente não escreverá:

> `mandatory = CONDITIONAL`

Essa é uma representação estruturada do produto.

O que importa é que exista na fonte informação suficiente para justificar essa classificação — por exemplo:

> “quando aplicável”

A estrutura ajuda o sistema a trabalhar com a informação. A evidência permite verificar se essa estrutura respeita aquilo que o cliente informou.

---

## Evidência limita a inferência

Rastreabilidade não serve apenas para explicar uma conclusão depois que ela foi produzida. Ela também ajuda a limitar aquilo que pode ser concluído.

Se uma obrigação atribuída ao cliente não consegue apontar para uma evidência adequada na fonte, essa obrigação precisa ser tratada com cuidado.

!!! info "Princípio de produto"
    Uma interpretação pode organizar ou classificar aquilo que está na fonte. Ela não deve usar a rastreabilidade como decoração para justificar uma obrigação que a fonte não sustenta.

Por isso, evidência e interpretação precisam permanecer semanticamente conectadas.

---

## Evidência da exigência e evidência de atendimento

À medida que uma análise avança, aparecem dois tipos de informação que não devem ser confundidos.

### Evidência da exigência

Sustenta **o que o cliente pediu**.

Exemplo:

> Cliente: “Apresentar comprovante de inscrição no CNPJ válido.”

Esse trecho sustenta a existência do requisito.

### Evidência de atendimento

Sustenta **por que consideramos que a empresa atende ou não atende ao requisito**.

Conceitualmente, pode ser um documento, dado ou outra informação da empresa que demonstre a situação daquele requisito.

Por exemplo:

**Requisito**  
Apresentar comprovante de inscrição no CNPJ válido.

**Evidência da exigência**  
Trecho em que o cliente solicita o comprovante.

**Evidência de atendimento**  
Informação ou documento da empresa que demonstre que o CNPJ está válido.

!!! note "Em desenvolvimento — experiência do produto"
    O MVP já preserva evidências da fonte durante a interpretação. O modelo completo de evidências de atendimento da empresa e sua experiência integrada ainda serão evoluídos e validados.

---

## Duas origens, duas perguntas diferentes

Essa separação cria uma cadeia importante dentro do Supplier Ready:

**Exigência do cliente**  
← evidência da fonte

↓ interpretação

**Requisito**

↓ avaliação

**Situação do requisito**  
← evidência da empresa

↓

**Readiness**

A evidência da fonte responde:

> **Por que dizemos que o cliente exige isso?**

A evidência da empresa responde:

> **Por que dizemos que esse requisito está — ou não está — atendido?**

São decisões diferentes e precisam permanecer rastreáveis separadamente.

---

## Rastreabilidade não elimina a necessidade de julgamento

Uma evidência permite verificar a origem de uma interpretação, mas não garante automaticamente que a interpretação esteja correta.

Uma pessoa ainda pode olhar para o mesmo trecho e identificar uma condição, nuance ou ambiguidade que mereça revisão.

Por isso, rastreabilidade não significa:

> “A IA mostrou uma citação, então a conclusão é verdadeira.”

Significa:

> “A IA mostrou qual informação sustenta sua conclusão, então podemos verificá-la.”

Essa diferença é essencial para um produto em que decisões podem depender da interpretação de documentos e exigências externas.

---

## Três perguntas para qualquer conclusão importante

Queremos que uma conclusão relevante dentro do Supplier Ready consiga responder:

### O que concluímos?

A interpretação ou avaliação produzida pelo produto.

### Com base em quê?

A evidência que sustenta essa conclusão.

### Onde está a informação original?

A fonte da qual essa evidência foi extraída ou obtida.

Se uma conclusão não consegue responder às três perguntas, sua rastreabilidade está incompleta.

> **Não queremos apenas respostas. Queremos respostas que possam ser verificadas.**

[Voltar para Interpretação de requisitos](requirement-interpretation.md){ .md-button }
[Entenda a Readiness →](readiness.md){ .md-button .md-button--primary }
