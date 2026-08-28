# Track Readiness

## Use readiness to track progress—not to predict approval.

The readiness engine is deterministic. `SATISFIED = 1.0`, `PARTIAL = 0.5`, `MISSING = 0.0`, and assessment `UNKNOWN = 0.0`. Non-applicable requirements are excluded; requirements with unknown applicability remain pending and outside the denominator.

If there are no scoreable requirements, the score is `null`. Always read the percentage together with its counters and remaining blockers.

**80% readiness does not mean an 80% probability that the customer will approve the company.**

!!! info "Available in the MVP engine"
    The calculation exists in the engine, but there is no dedicated public HTTP endpoint or complete product experience for tracking it yet.

!!! note "Final Ready is still in development"
    The readiness engine does not define a domain `Ready` state. `ProductAnalysisState.READY` is different: it only means the interpretation journey has no pending clarification.

[Understand Readiness as a concept](../concepts/readiness.md){ .md-button }
