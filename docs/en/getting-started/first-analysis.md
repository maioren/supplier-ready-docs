# Your first analysis

## Start with the requirements you received.

Every Supplier Ready analysis starts from a source: what your customer actually communicated as a condition for onboarding or qualification.

In this first walkthrough, we'll follow how that content moves from plain text into a traceable structure of requirements.

!!! info "Available in the MVP"
    The current engine can create an analysis from a company tax identifier and requirement text, interpret requirements, preserve source evidence, handle clarifications, and calculate readiness. The integrated visual experience for this complete flow is still being built.

## An example to follow

Imagine your customer sent this requirement:

> **The company must provide proof of a valid company registration and, when applicable, registration with the relevant professional council.**

It is a short sentence, but it contains more than one important piece of information. Supplier Ready needs to separate them without turning conditions into certainties.

---

## 1. The source enters the analysis

!!! info "Available in the MVP"

The analysis begins with the company identification and the content received from the customer.

The original text remains the reference for determining what was actually requested. It must not be silently replaced by an AI interpretation.

!!! note "In development — product experience"
    The interface for creating and following an analysis end to end is still being built. This documentation therefore describes product behavior without assuming buttons or screens that do not yet exist.

---

## 2. Supplier Ready identifies requirements

!!! info "Available in the MVP"

The engine interprets the content and organizes the requirements into individual units.

Conceptually, our example may produce:

**Proof of valid company registration**  
Mandatory

**Registration with the relevant professional council**  
Conditional — when applicable

Separating requirements matters because each can have its own condition, evidence, applicability, and evaluation.

---

## 3. Each interpretation remains linked to the source

!!! info "Available in the MVP"

Supplier Ready preserves the source excerpt that supports each identified requirement.

This makes it possible to distinguish clearly between **what the customer said** and **how Supplier Ready interpreted it**.

The interpretation helps organize the information. **The source remains the truth.**

---

## 4. Conditions do not become facts

!!! info "Available in the MVP"

The phrase **“when applicable”** does not tell us, by itself, whether professional registration is mandatory for your company.

Supplier Ready should preserve that uncertainty rather than assume an answer.

The analysis may therefore require a clarification such as:

> **We need to clarify**  
> Does professional council registration apply to your company's activity?

The MVP engine already supports planning, listing, and answering clarifications.

> **When Supplier Ready doesn't know, it shouldn't guess. It should ask.**

---

## 5. Your company's reality enters the analysis

!!! note "In development — product experience"

After understanding what the customer requires, those requirements need to be compared with your company's reality.

That comparison turns requirements into concrete gaps instead of merely producing a document list.

---

## 6. The analysis moves toward Readiness

!!! info "Available in the MVP"
    Deterministic readiness calculation already exists in the engine. The integrated experience that will automatically produce all necessary evaluations for the user is still in development.

As requirements are evaluated, they can be **Satisfied**, **Partial**, **Missing**, **Unknown**, or **Not applicable**.

Readiness turns these evaluations into an objective view of what is resolved and what still prevents the company from moving forward.

---

## 7. The goal is to reach Ready

!!! note "In development — product experience"

The final result we're building is not just an interpreted list of requirements. We want an analysis to answer simply: **What did my customer ask for? What does my company already meet? What is still missing? What needs clarification?**

When everything that needs to be resolved has been resolved, your company will be **Ready** to move forward with that customer.

[Understand requirement interpretation →](../concepts/requirement-interpretation.md){ .md-button .md-button--primary }
