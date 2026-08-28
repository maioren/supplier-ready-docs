# Review interpreted requirements

## Verify what was understood before using it for decisions.

The current product journey already exposes interpreted requirements after processing the source. Review the requirement name, category, type, applicability, condition and source trace presented by the product response.

!!! info "Available in the MVP"
    The Interpreter produces the richer domain model, while `/v0/product/analyses` exposes the subset needed by the current product experience, including exact source offsets.

Always verify `source_quote` against the original source. `UNKNOWN` applicability is valid and should remain unresolved until enough context exists. The full Interpreter model can also contain confidence, mandatory/blocking flags, canonical name, issuer, uncertainties, clarifications and warnings; not all of those fields are exposed by the current `RequirementView`.

A review should answer: what was interpreted, whether a condition exists, whether applicability is known, what source evidence supports the interpretation, and whether uncertainty remains.

[Resolve clarifications →](resolve-clarifications.md){ .md-button .md-button--primary }
