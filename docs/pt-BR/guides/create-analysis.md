# Criar uma análise

## Registre as exigências que você precisa entender.

Uma **análise** é o ponto de partida para trabalhar com as exigências de um cliente no Supplier Ready.

Criar uma análise significa registrar **qual empresa está sendo analisada** e **qual conteúdo foi recebido como fonte das exigências**.

> **Criar uma análise registra o problema que queremos resolver. Ainda não é a interpretação.**

!!! info "Disponível no MVP"
    O motor atual já permite criar uma análise a partir de um CNPJ e de uma fonte textual. A experiência visual integrada para executar essa tarefa ainda está sendo construída.

---

## Antes de começar

Para criar uma análise no MVP atual, você precisa de duas informações:

### CNPJ da empresa

O CNPJ identifica a empresa cuja preparação será analisada.

O motor aceita o CNPJ:

- com a máscara padrão, como `12.345.678/0001-XX`; ou
- somente com os 14 dígitos.

O valor precisa representar um CNPJ válido. Quando aceito, ele é normalizado para o formato padrão.

### Texto com as exigências

O conteúdo recebido do cliente é fornecido atualmente como **texto**.

Esse texto precisa conter conteúdo significativo e respeitar o limite de tamanho configurado no ambiente.

!!! note "Limitação atual do MVP"
    A fonte suportada hoje é `TEXT`. Upload direto de PDF, planilhas, e-mails ou outros formatos ainda não faz parte desta etapa do MVP.

---

## 1. Prepare a fonte

Use como entrada aquilo que efetivamente foi informado pelo cliente.

Por exemplo:

> A empresa deverá apresentar comprovante de inscrição no CNPJ válido e, quando aplicável, registro no conselho profissional competente.

Evite reescrever o conteúdo apenas para torná-lo mais fácil para a IA. Preservar a formulação recebida ajuda a manter condições, exceções e ambiguidades que podem ser relevantes durante a interpretação.

Se for necessário preparar conteúdo vindo de outro formato para o MVP atual, o objetivo é preservar o significado da fonte — não antecipar sua interpretação.

---

## 2. Crie a análise

!!! info "Disponível no MVP"

No contrato atual da API, a criação acontece por meio de:

`POST /v0/analyses`

A operação recebe dois campos:

```json
{
  "cnpj": "12.345.678/0001-XX",
  "requirements_text": "Texto das exigências recebidas do cliente"
}
```

!!! warning "Exemplo ilustrativo"
    O CNPJ acima é apenas uma representação de formato. Para uma requisição real, use um CNPJ válido.

Neste estágio, o objetivo da operação é registrar a análise e preservar o texto informado como sua fonte.

---

## 3. Confirme que a análise foi recebida

Quando a criação é aceita, o MVP responde com HTTP `201` e informa:

- `analysis_id` — identificador único da análise;
- `cnpj` — CNPJ normalizado;
- `status` — estado atual da análise.

O estado inicial disponível hoje é:

`RECEIVED`

Conceitualmente, uma resposta tem esta forma:

```json
{
  "analysis_id": "<uuid-da-analise>",
  "cnpj": "<cnpj-normalizado>",
  "status": "RECEIVED"
}
```

`RECEIVED` significa que a análise foi criada e sua fonte foi registrada.

**Não significa que os requisitos já foram interpretados.**

---

## 4. Entenda o que foi preservado

A análise criada mantém a fonte textual associada ao registro da análise.

No modelo atual:

**Empresa**  
→ identificada pelo CNPJ

**Fonte**  
→ tipo `TEXT`

**Conteúdo**  
→ texto das exigências recebido na criação

**Estado inicial**  
→ `RECEIVED`

Essa separação é importante porque a fonte existe antes das interpretações que serão produzidas a partir dela.

---

## 5. Trate entradas inválidas

A criação pode ser rejeitada quando a entrada não atende às regras atuais do MVP.

### CNPJ inválido

Se o CNPJ não possuir um formato aceito ou não for válido, a operação retorna o erro de domínio:

`INVALID_CNPJ`

### Exigências vazias

Se o texto não contiver conteúdo significativo:

`EMPTY_REQUIREMENTS`

### Fonte acima do limite

Se o conteúdo ultrapassar o limite de caracteres configurado no ambiente:

`SOURCE_TOO_LARGE`

O limite é configurável, por isso esta documentação não assume um número fixo de caracteres.

---

## 6. Prossiga para a interpretação

Criar a análise estabelece a origem do trabalho:

**CNPJ + fonte das exigências**  
↓

**Análise recebida (`RECEIVED`)**  
↓

**Interpretação dos requisitos**

A interpretação é uma etapa separada. É nela que o Supplier Ready começa a transformar o texto recebido em requisitos estruturados, preservando condições, evidências e incertezas.

!!! note "Em desenvolvimento — experiência do produto"
    A experiência que conectará criação, interpretação e acompanhamento da análise em um único fluxo visual ainda está sendo construída. Este guia descreve apenas o comportamento que já existe no MVP.

---

## Resultado esperado

Ao concluir esta tarefa, você deve ter uma análise criada com:

- um identificador próprio;
- o CNPJ válido e normalizado da empresa;
- a fonte textual preservada;
- estado `RECEIVED`.

A partir daí, a análise está pronta para seguir para a interpretação dos requisitos.

[Entenda como os requisitos são interpretados →](../concepts/requirement-interpretation.md){ .md-button .md-button--primary }
