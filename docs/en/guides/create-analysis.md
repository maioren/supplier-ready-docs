# Create an analysis

## Register the requirements you need to understand.

An **analysis** is the starting point for working with a customer's requirements in Supplier Ready. Creating one records the company being analyzed and the textual source received from the customer.

> **Creating an analysis registers the problem we want to solve. It is not the interpretation yet.**

!!! info "Available in the MVP"
    The current product journey accepts a CNPJ and textual requirements, creates the analysis and processes it through the Interpreter. The lower-level API can also create only the `RECEIVED` analysis record.

## Before you start

You need a valid CNPJ and meaningful requirement text. The current source type is `TEXT`; direct PDF, spreadsheet or email upload is not yet part of this MVP stage.

## Product journey

`POST /v0/product/analyses` creates and processes the analysis. It can return either `NEEDS_CLARIFICATION` or `READY` as the interpretation-journey state.

!!! warning "`READY` has a narrow meaning here"
    `ProductAnalysisState.READY` only means there are no pending interpretation clarifications. It is not the readiness score and does not mean the company already satisfies every customer requirement.

## Lower-level creation

`POST /v0/analyses` receives `cnpj` and `requirements_text`, returns HTTP `201`, and creates a record with status `RECEIVED`. `RECEIVED` means the source was registered; it does not mean requirements were interpreted.

Invalid input can produce `INVALID_CNPJ`, `EMPTY_REQUIREMENTS` or `SOURCE_TOO_LARGE`.

[Review interpreted requirements →](review-interpreted-requirements.md){ .md-button .md-button--primary }
