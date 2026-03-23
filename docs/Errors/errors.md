# Errors

Errors are returned using standard HTTP error code syntax. Depending on the status code, the response body may be in JSON or plaintext.

Search API uses conventional HTTP response codes to indicate the success or failure of an API request along with clear error messages. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted).

HTTP Status Code Summary

### 200 OK (Success)

200	OK	Everything worked as expected.

```json
{
  "status": "success",
  "applications": [
    {
      "applicationId": "APPID2025XYZ001",
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

### 400 Bad Request  

400	Bad Request	The request was unacceptable, often due to missing a required parameter.
Invalid input fields.

```json
{
  "status": "error",
  "errorCode": "ERR_INVALID_ACK",
  "message": "Invalid Acknowledgment Number"
}

{
  "status": "error",
  "errorCode": "ERR_INVALID_REF",
  "message": "Invalid Reference Number"
}

{
  "status": "error",
  "errorCode": "ERR_INVALID_APPID",
  "message": "Invalid Application ID"
}

```

### 402	Request Failed  

The parameters were valid but the request failed.

```json
{
  "error": "Something went wrong",
  "errorCode": "ERR_402",
  "message": "Something went wrong, please try again after sometime"
}
```

### 404	Not Found  

The requested resource doesn’t exist.

```json
{
  "error": "Missing mandatory field",
  "errorCode": "ERR_MIS_APPYR",
  "message": "Application Year is required"
}
```