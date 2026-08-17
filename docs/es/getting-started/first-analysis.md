# Su primer análisis

## Comience por las exigencias que recibió.

Todo análisis en Supplier Ready parte de una fuente: aquello que su cliente efectivamente informó como condición para registro, homologación o calificación.

En este primer recorrido veremos cómo ese contenido deja de ser solo texto y se convierte en una estructura de requisitos con trazabilidad.

!!! info "Disponible en el MVP"
    El motor actual ya permite crear un análisis a partir de la identificación fiscal de la empresa y del texto de las exigencias, interpretar requisitos, preservar evidencias de la fuente, tratar aclaraciones y calcular readiness. La experiencia visual integrada todavía está en construcción.

## Un ejemplo para acompañar

Imagine que su cliente envió esta exigencia:

> **La empresa deberá presentar comprobante de inscripción fiscal válido y, cuando corresponda, registro ante el consejo profesional competente.**

Es una frase breve, pero contiene más de una información importante. Supplier Ready debe separarlas sin transformar condiciones en certezas.

## 1. La fuente entra en el análisis

!!! info "Disponible en el MVP"

El texto original sigue siendo la referencia para determinar lo que realmente se solicitó. No debe ser sustituido silenciosamente por una interpretación de la IA.

!!! note "En desarrollo — experiencia de producto"
    La interfaz para crear y seguir un análisis de punta a punta todavía está en construcción. Por eso esta documentación describe el comportamiento del producto sin asumir botones o pantallas que aún no existen.

## 2. Supplier Ready identifica los requisitos

!!! info "Disponible en el MVP"

El motor interpreta el contenido y organiza las exigencias en requisitos individuales, cada uno con su propia condición, evidencia, aplicabilidad y evaluación.

## 3. Cada interpretación sigue vinculada a la fuente

!!! info "Disponible en el MVP"

Supplier Ready preserva el fragmento de la fuente que sustenta cada requisito. La interpretación organiza la información. **La fuente sigue siendo la verdad.**

## 4. Las condiciones no se convierten en hechos

!!! info "Disponible en el MVP"

“Cuando corresponda” no informa por sí solo si el registro profesional es obligatorio para su empresa. Supplier Ready debe preservar esa incertidumbre y puede necesitar una aclaración.

> **Cuando Supplier Ready no sabe, no debe adivinar. Debe preguntar.**

## 5. La realidad de su empresa entra en el análisis

!!! note "En desarrollo — experiencia de producto"

Después de entender lo que exige el cliente, esos requisitos deben compararse con la realidad de su empresa para convertirlos en gaps concretos.

## 6. El análisis avanza hacia Readiness

!!! info "Disponible en el MVP"
    El cálculo determinista de readiness ya existe en el motor. La experiencia integrada todavía está en desarrollo.

Los requisitos pueden evaluarse como **Cumplido**, **Parcial**, **Faltante**, **Desconocido** o **No aplicable**.

## 7. El objetivo es llegar a Ready

!!! note "En desarrollo — experiencia de producto"

Queremos que un análisis responda de forma simple: **¿Qué pidió mi cliente? ¿Qué cumple ya mi empresa? ¿Qué falta? ¿Qué necesita aclaración?**

Cuando todo lo necesario esté resuelto, su empresa estará **Ready** para avanzar.

[Entienda la interpretación de requisitos →](../concepts/requirement-interpretation.md){ .md-button .md-button--primary }
