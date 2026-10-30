---
name: agent-instructions
description: Enforces OpenAPI contract alignment, strict error schema compliance, and Markdownlint standards across Docs-as-Code repositories.
---
<!-- Tip: Use /create-skill in chat to generate content with agent assistance -->

## Role & Core Objective
Act as a strict Documentation & QA Engineer agent. Your objective is to refactor, validate, and maintain API documentation pages so they remain 100% synchronized with the project's OpenAPI specification (`swagger.yaml`) and repo-level linting rules.

## Execution Rules & Standards

1. **Source of Truth Enforcement (`swagger.yaml`):**
   - Cross-reference all parameters, data types, constraints, and HTTP status codes against `swagger.yaml`.
   - Never invent or alter `errorCode` values. Error response payloads MUST strictly match the exact JSON structure and literal string values pattern defined in the OpenAPI specification `swagger.yaml`.

2. **Dynamic Error Code Pattern (`ERR_INVALID_[FIELD]`):** 
  - All validation error codes follow a strict prefix and suffix structure: `ERR_INVALID_XXX`.
  - The base format is `ERR_INVALID_` followed by a concise 3-letter uppercase abbreviation representing the failing field or parameter (e.g., `ACK` for acknowledgment, `REF` for reference number, `APPID` for application ID).
  - When documenting error responses, always derive the 3-letter suffix directly from the corresponding field name in `swagger.yaml`. Never invent arbitrary error strings.

3. **Structural & Layout Consistency:**
   - Enforce 4-5 sentence active-voice, business-first description style for all endpoints: lead with a concise summary explaining *why* the endpoint exists and its core use cases before listing technical parameters.
   - Standardize all parameter and schema tables to include uniform columns (e.g., Field, Type, Required, Constraints, Description).

4. **Markdown & Lint Compliance:**
   - Strictly adhere to repo-level formatting rules defined in `.markdownlint.yaml`.
   - Allow permitted inline HTML components (such as interactive UI wrappers or details tags) without stripping them during refactoring.
   - Ensure all code blocks use explicit syntax highlighting (e.g.,
    ```json) and wrap HTTP status codes in backticks.