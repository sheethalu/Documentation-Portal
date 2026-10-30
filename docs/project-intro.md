# Overview

The Loan Search API is organized around REST. It provides internal backend services for dashboard applications to query loan records, populate search filters, and authenticate administrative sessions.

The API accepts JSON-encoded request bodies, returns standard JSON responses, and uses predictable HTTP response codes, verbs, and JWT authentication.

**Base URL:** `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io/`

## API Reference

To ensure consistent data querying across dashboard applications, search parameters adhere to strict validation logic. Client applications can query application records using three primary text identifiers: `Acknowledgement Number`, `Reference Number`, and `Application ID`. These fields accept 1–15 case-insensitive alphanumeric characters.

Filtering by application status is constrained to three supported statuses: `Approved`, `Pending`, and `Rejected`. For Year filters, the system defaults to `2026`, but also allows querying records from previous two consecutive years `2024` and `2025`. Result sets can be sorted in ascending or descending order by Submission Date, Amount, or Customer Name.

### Search results table fields

| Application ID  | Customer Name | Loan Type | Status   | Amount | Submitted By | Submission Date | Branch Code |
| --------------- | ------------- | --------- | -------- | ------ | ------------ | --------------- | ----------- |
| APPID2025XYZ001 | John Doe      | Home Loan | Approved | 250000 | Officer A    | 2025-01-20      | BR001       |

## Endpoints

**Login-Auth**
- `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io/auth/login`

**Search**
- `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io/search-loans`

**Dropdown**
- `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io/dropdown/filters`

## Repository & Information Architecture

This documentation portal uses a **Docs-as-Code** approach. The source Markdown files, OpenAPI specifications, and automated CI/CD configurations are organized as follows:

```text

Documentation-Portal/
├── .github
|    ├── /skills/agent-instructions
|    |    └── SKILL.md            # Custom AI agent governance & schema rules
|    └── /workflows/
│         └── deploy.yml          # GitHub Actions CI/CD pipeline
├── .husky                        # Git pre-commit hooks for automated code linting & validation
├── docs/                         # Base documentation source
│   ├── auth/                     # Endpoint docs: Authentication
│   │   └── login.md
│   ├── dropdown/                 # Endpoint docs: Reference Data
│   │   └── dropdowns.md
│   ├── errors/                   # Global error response codes
│   │   └── errors.md
│   ├── search/                   # Endpoint docs: Search & sorting loan applications
│   │   └── search-loans.md
│   ├── index.md                  # Technical Writer/QA Portfolio & Resume
│   ├── project-intro.md          # System architecture & domain overview
│   ├── resources.md              # Downloadable Postman collections & test cases
│   └── swagger.yaml              # OpenAPI 3.0 specification file
├── .markdownlint.yaml            # Markdown linting rule configuration
├── .spectral.yaml                # Spectral OpenAPI linting ruleset
└── mkdocs.yml                    # Site navigation & plugin configuration

```

### Docs-As-Code & AI-Assisted Workflow

To accelerate delivery while maintaining production-grade accuracy, this portal leverages a custom **AI Agent Governance Framework** (`SKILL.md` + OpenAPI contracts):

- The agent cross-references error rules (`errors.md`) and strict OpenAPI schemas (`swagger.yaml`), completely eliminating hallucinated error codes.
- Automated markdown/JSON linting combined with mandatory manual review ensures clean layout consistency before deployment to GitHub Pages.

### Workflow Comparison: AI Draft vs. Final Polish

To demonstrate the human-in-the-loop refinement process:
- **Raw AI Skeleton (`search-test.md`):** Generated via repository agent rules to instantly establish parameter and error tables.

   ![AI Draft](docs/portfolio-assets/images/ai-draft.png)

- **Production-Ready Output:** The final polished page deployed to the live portal.
    *[View the live search-loans.md documentation page in production →](https://sheethalu.github.io/Documentation-Portal/search/search-loans/)*