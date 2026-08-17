# Readiness

## Readiness measures what is already resolved. It does not predict the customer's decision.

**Readiness** represents how prepared your company is to move forward with a customer based on known requirements and the current state of each requirement.

If an analysis shows **80% readiness**, that does **not mean an 80% chance of customer approval**. It means that, according to the known information and analysis rules, part of what needs to be met is already resolved.

!!! info "Available in the MVP"
    The current engine already calculates readiness deterministically from requirement evaluations. The integrated visual experience is still being built.

## States that feed readiness

**Satisfied:** 1.0  
**Partial:** 0.5  
**Missing:** 0.0  
**Unknown:** 0.0  
**Not applicable:** excluded from the calculation.

## Unknown applicability is different from an unknown evaluation

If we do not yet know **whether a requirement applies**, it stays outside the score and is tracked separately as an applicability pending item. If applicability is known but we do not know **whether the company satisfies it**, the evaluation is Unknown and participates in the score with weight zero.

## How the score is calculated today

`readiness = sum of weights ÷ number of evaluable requirements × 100`

For 7 Satisfied, 2 Partial, and 1 Missing requirement:

`(7 × 1.0 + 2 × 0.5 + 1 × 0.0) ÷ 10 × 100 = 80%`

If there are no evaluable requirements, the engine does not force an artificial percentage.

## Readiness is deterministic

AI can help interpret requirements and gather information. **It does not choose the score.**

> **Same requirements + same evaluations = same readiness.**

## Readiness and Ready are not the same thing

**Readiness** is a measure of progress: *How much have we resolved?*

**Ready** is the completion state we're building: *Is there anything that still prevents us from moving forward?*

!!! note "In development — product experience"
    The current engine calculates readiness but does not yet have a `Ready` domain state. Its final definition and rules will still be implemented and validated.

Conceptually, we want **Ready** to mean that everything applicable and necessary has been resolved — not simply that a number reached a threshold.

> **Readiness answers: how much have we resolved?**  
> **Ready answers: is there anything still preventing us from moving forward?**
