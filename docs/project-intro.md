# Overview & Getting Started

## Purpose

This API lets a loan officer search existing loan applications using simple search filters (acknowledgement number, reference number, application ID, loan status, year).

**Base URL:** `https://a8fcbf71-9a93-43f6-ab3c-b95b953b1c57.mock.pstmn.io/`

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

## What you need

- A tool to make HTTP requests (Postman).
- For this mock, **authentication** is required.

## Authentication

Auth uses JSON Web Tokens (JWT) sent in the Authorization header: `Authorization: Bearer <access_token>.`

## UI Expectations and Filters (Business Rules)

- Three text inputs (Acknowledgement Number, Reference Number, Application Id).
- **Acknowledgement Number**: 1–15 alphanumeric (case-insensitive). Anything else → *Invalid Acknowledgement Number*.  
- **Reference Number**: 1–15 alphanumeric (case-insensitive). Anything else → *Invalid Reference Number*.  
- **Application Id**: 1–15 alphanumeric (case-insensitive). Anything else → *Invalid Application ID*.  
- Two dropdowns (Loan Status, Application Year).
- **Loan Status**: one of `Approved`,`Pending`, `Rejected`.
- Application Year is auto-selected to current year (2026) and a mandatory field.
- **Application Year**: **(Required)** Allowed: `2024`, `2025`, `2026`. Default UI value: `2026`.
- **Sorting**: Results can be sorted in Ascending or Descending order. Primary sort fields include Submission Date, Amount, and Customer Name.

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
