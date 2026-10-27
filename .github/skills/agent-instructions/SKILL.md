---
name: agent-instructions
description: Governs project rules, OpenAPI schema alignment, dropdown template structure, and MkDocs formatting across all API documentation files.
---
<!-- Tip: Use /create-skill in chat to generate content with agent assistance -->

Act as a documentation editor that refactors half-drafted API files into production-ready Markdown aligned with `swagger.yaml`

## Workspace Reference Files
* **Structural Template Source:** Always inspect `docs/dropdown/dropdowns-test.md` first to understand the standard header structure, Markdown table format, and dropdown section layout required across this repository.
* **Schema Validation Source:** Cross-reference parameters, data types, and status codes against `swagger.yaml`.

## Refactoring Execution Rules
When invoked on any file (including `docs/dropdown/dropdowns-test.md` and `docs/auth/login-test.md`):

1. **Refactor Endpoint Descriptions:**
   * Rewrite existing descriptions (including the description in `dropdowns-test.md`) to be concise and active-voice.
   * Lead with a 4-sentence business summary explaining *why* the endpoint exists, functionality and use cases before listing technical details.
  
2. **Enforce Template Layout from `dropdowns-test.md`:**
   * Copy the structural layout, section headings, and table formatting from `docs/dropdown/dropdowns-test.md` and apply them to the file being refactored.
   * Do not add any additional columns to schema tables unless otherwise explicitly requested.
   
3. **Verify API Coverage (`swagger.yaml`):**
   * Ensure parameter tables include Type, Required, Constraints and Description.
   * Document both successful responses (`200 OK`) and error references mentioned in `swagger.yaml`.
   * Never invent or alter `errorCode` values. All error responses MUST strictly match the exact JSON structure and literal `errorCode` strings defined in `swagger.yaml` (e.g., `{"status": "error", "errorCode": "ERR_INVALID_PARAM", "message": "..."}`).
   * Wrap status codes in backticks and use ```json for payload blocks.

4. **Maintain Markdown Consistency:**
   * Match the established pattern in dropdowns-test.md and login-test.md for headings, lists, tables, and fenced code blocks.
  * Preserve repo lint exceptions from `.markdownlint.yaml`, allow inline HTML tags such as <swagger-ui> or <details>.
