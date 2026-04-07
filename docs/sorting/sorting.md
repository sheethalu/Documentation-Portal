## Endpoint reference (detailed)

All request and response bodies are JSON unless otherwise stated. For each endpoint below you'll find:

- API path
- Short one-line description
- Positive and negative cases for: Request type, Request body, Response body, Status code

<swagger-ui src="/swagger.yaml" filter="Sorting"/>

## SORTING – SCHEMAS

**Model: Sorting Request**

|Field	|Type	|Required	|Description|
|-------|-------|-----------|-----------|
|acknowledgmentNumber	|string	|no	|1–15 alphanumeric, case-insensitive|
|referenceNumber	|string	|no	|1–15 alphanumeric, case-insensitive|
|applicationId|string	|no	|1–15 alphanumeric, case-insensitive|
|loanStatus|string| no|One of: Approved, Pending, Rejected|
|applicationYear | number| yes | Allowed: 2024, 2025, 2026. Default: 2026|

**Sorting Request**

acknowledgmentNumber: `string (1–15 alphanumeric)`  
referenceNumber: `string (1–15 alphanumeric)`  
applicationId: `string (1–15 alphanumeric)`  
loanStatus: `string (enum: Approved, Pending, Rejected)`  
applicationYear: `number (required, enum: 2024 | 2025 | 2026; default=2026)`  


**Model: Sorting Response**

|Field	|Type	|Description|
|-------|-------|-----------|
|status	|string	|Response status.|
|applications	|array<ApplicationRecord>	|List of loan applications matching the criteria.|


**Model: ApplicationRecord**

|Field	|Type	|Description|
|-------|-------|-----------|
|applicationId	|string	|Unique ID of the loan application.|
|customerName	|string	|Customer’s full name.|
|loanType	|string	|Type of loan (e.g., Home Loan).|
|status	|string	|Application status.|
|amount	|number	|Loan amount approved/requested.|
|submittedBy	|string	|Loan officer who created the application.|
|submissionDate	|string (YYYY-MM-DD)	|Date of submission.|
|branchCode	|string	|Branch identifier.|


**SearchResponse**

status: `string`  
applications: `array<ApplicationRecord>`  


ApplicationRecord:  
  applicationId: `string`  
  customerName: `string`  
  loanType: `string`  
  status: `string`  
  amount: `number`  
  submittedBy: `string`  
  submissionDate: `string (YYYY-MM-DD)`  
  branchCode: `string`  

## Search loan applications
- **URL:** `/search-loans?sortBy=submissionDate&sortOrder=desc`
- **URL:** `/search-loans?sortBy=submissionDate&sortOrder=asc`
- **Method:** `POST`  
- **Description:** This API will sort the loan application details in ascending and descending order. Positive case returns 200 OK.

**Sorting - Descending**

**Request:**
```json
{
    "acknowledgmentNumber": "",
    "referenceNumber": "",
    "applicationId": "",
    "loanStatus": "",
    "applicationYear": "2025"
}
```
**Response:**
```json
{
  "status": "success",
  "applications": [
    {
      "applicationId": "APPID2025XYZ892",
      "customerName": "Jane Austin",
      "loanType": "Personal Loan",
      "status": "Pending",
      "amount": 90000,
      "submittedBy": "Officer B",
      "submissionDate": "2025-09-11",
      "branchCode": "BR002"
    },
      {
      "applicationId": "APPID2025XYZ891",
      "customerName": "Jane Smith",
      "loanType": "Car Loan",
      "status": "Rejected",
      "amount": 90000,
      "submittedBy": "Officer B",
      "submissionDate": "2025-06-10",
      "branchCode": "BR002"
    },
    {
      "applicationId": "APPID2025XYZ890",
      "customerName": "John Doe",
      "loanType": "Home Loan",
      "status": "Approved",
      "amount": 250000,
      "submittedBy": "Officer A",
      "submissionDate": "2025-01-20",
      "branchCode": "BR001"
    }
  ]
}

```
**Sorting - Ascending**

**Request:**
```json
{
    "acknowledgmentNumber": "",
    "referenceNumber": "",
    "applicationId": "",
    "loanStatus": "",
    "applicationYear": "2025"
}
```
**Response:**
```json
{
  "status": "success",
  "applications": [
    {
      "applicationId": "APPID2025XYZ890",
      "customerName": "John Doe",
      "loanType": "Home Loan",
      "status": "Approved",
      "amount": 250000,
      "submittedBy": "Officer A",
      "submissionDate": "2025-01-20",
      "branchCode": "BR001"
    },
    {
      "applicationId": "APPID2025XYZ891",
      "customerName": "Jane Smith",
      "loanType": "Car Loan",
      "status": "Rejected",
      "amount": 90000,
      "submittedBy": "Officer B",
      "submissionDate": "2025-06-10",
      "branchCode": "BR002"
    },
    {
      "applicationId": "APPID2025XYZ892",
      "customerName": "Jane Austin",
      "loanType": "Personal Loan",
      "status": "Pending",
      "amount": 90000,
      "submittedBy": "Officer B",
      "submissionDate": "2025-09-11",
      "branchCode": "BR002"
    }
  ]
}
```