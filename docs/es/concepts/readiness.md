# Readiness

## Readiness mide lo que ya está resuelto. No predice la decisión del cliente.

**Readiness** representa cuánto está preparada su empresa para avanzar con un cliente considerando las exigencias conocidas y la situación actual de cada requisito.

Si un análisis muestra **80% de readiness**, eso **no significa 80% de probabilidad de aprobación por el cliente**. Significa que, según la información conocida y las reglas del análisis, parte de lo que debe cumplirse ya está resuelto.

!!! info "Disponible en el MVP"
    El motor actual ya calcula readiness de forma determinista a partir de las evaluaciones de los requisitos. La experiencia visual integrada todavía está en construcción.

## Estados que alimentan readiness

**Cumplido:** 1,0  
**Parcial:** 0,5  
**Faltante:** 0,0  
**Desconocido:** 0,0  
**No aplicable:** excluido del cálculo.

## Aplicabilidad desconocida es diferente de evaluación desconocida

Si todavía no sabemos **si un requisito se aplica**, queda fuera del score y se acompaña por separado. Si sabemos que se aplica pero no sabemos **si la empresa lo cumple**, entra en el score como Desconocido con peso cero.

## Cómo se calcula hoy

`readiness = suma de pesos ÷ cantidad de requisitos evaluables × 100`

Para 7 Cumplidos, 2 Parciales y 1 Faltante:

`(7 × 1,0 + 2 × 0,5 + 1 × 0,0) ÷ 10 × 100 = 80%`

## Readiness es determinista

La IA puede ayudar a interpretar y obtener información. **No elige el score.**

> **Mismos requisitos + mismas evaluaciones = misma readiness.**

## Readiness y Ready no son lo mismo

**Readiness** es una medida de progreso: *¿Cuánto hemos resuelto?*

**Ready** es el estado de conclusión que estamos construyendo: *¿Existe algo que todavía impide avanzar?*

!!! note "En desarrollo — experiencia de producto"
    El motor actual calcula readiness, pero todavía no posee un estado de dominio `Ready`. Su definición y reglas finales aún serán implementadas y validadas.

Conceptualmente, queremos que **Ready** signifique que todo lo aplicable y necesario está resuelto, no simplemente que un número alcanzó un umbral.

> **Readiness responde: cuánto hemos resuelto?**  
> **Ready responde: existe algo que todavía impide avanzar?**
