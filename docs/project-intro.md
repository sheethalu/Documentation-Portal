# Overview

The Loan Search API is organized around REST. It provides internal backend services for dashboard applications to query loan records, populate search filters, and authenticate administrative sessions.

The API accepts JSON-encoded request bodies, returns standard JSON responses, and uses predictable HTTP response codes, verbs, and JWT authentication.

**Base URL:** `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io/`

## UI Expectations and Filters (Business Rules)
To ensure consistent data querying across dashboard applications, search parameters adhere to strict validation logic. Client applications can query application records using three primary text identifiers: `Acknowledgement Number`, `Reference Number`, and `Application ID`. These fields accept 1–15 case-insensitive alphanumeric characters.

Filtering by application status is constrained to three supported statuses: `Approved`, `Pending`, and `Rejected`. For Year filters, the system defaults to `2026`, but also allows querying records from previous two consecutive years `2024` and `2025`. Result sets can be sorted in ascending or descending order by Submission Date, Amount, or Customer Name. 

### Search results table fields

| Application ID  | Customer Name | Loan Type | Status   | Amount | Submitted By | Submission Date | Branch Code |
| --------------- | ------------- | --------- | -------- | ------ | ------------ | --------------- | ----------- |
| APPID2025XYZ001 | John Doe      | Home Loan | Approved | 250000 | Officer A    | 2025-01-20      | BR001       |

## Endpoints

**Login- Auth**
- `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io/auth/login`

**Search loans**
- `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io/search-loans`

**Dropdown options**
- `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io//dropdown/filters`

## Repository & Information Architecture

This documentation portal uses a **Docs-as-Code** approach. The source Markdown files, OpenAPI specifications, and automated CI/CD configurations are organized as follows:

```text

Documentation-Portal/
├── .github/workflows/
│   └── deploy.yml          # GitHub Actions CI/CD pipeline
├── docs/                   # Base documentation source
│   ├── auth/               # Endpoint docs: Authentication
│   │   └── login.md
│   ├── dropdown/           # Endpoint docs: Reference Data
│   │   └── dropdowns.md
│   ├── errors/             # Global error response codes
│   │   └── errors.md
│   ├── search/             # Endpoint docs: Search & Loans
│   │   └── search-loans.md
│   ├── sorting/            # Endpoint docs: Sorting parameters
│   │   └── sorting.md
│   ├── index.md            # Technical Writer Portfolio & Resume
│   ├── project-intro.md    # System architecture & domain overview
│   ├── resources.md        # Downloadable Postman collections & test cases
│   └── swagger.yaml        # OpenAPI 3.0 specification file
├── .markdownlint.yaml      # Markdown linting rule configuration
├── .spectral.yaml          # Spectral OpenAPI linting ruleset
└── mkdocs.yml              # Site navigation & plugin configuration

```