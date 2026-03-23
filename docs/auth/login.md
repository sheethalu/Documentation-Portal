## Endpoint reference (detailed)

All request and response bodies are JSON unless otherwise stated. For each endpoint below you'll find:

- API path
- Short one-line description
- Positive and negative cases for: Request type, Request body, Response body, Status code

## AUTHENTICATION API – SCHEMAS

**Model: AuthRequest**

|Field	|Type	|Required	|Description|
|-------|-------|-----------|-----------|
|username	|string	|yes	|Login username of the user.|
|password	|string	|yes	|Account password.|

**AuthRequest**
```
username: `string (required)`  
password: `string (required)`  
```

**Model: AuthResponse**

|Field	  | Type	| Description  |
|---------|---------|--------------|
| status  |	string  |	Response status, e.g., "success". |
| token	  |string (JWT)	| Access token used for authentication.|
| expiresIn |	number |	Expiration time in seconds.        |
|issuedAt	|string (ISO8601)  |	Timestamp when token was issued.|
|roles	|array[string]	| The user’s roles / permissions.|

**AuthResponse**
```
status: `string`  
token: `string (JWT)`  
expiresIn: `number`  
issuedAt: `string (ISO 8601 datetime)`  
roles: `array[string]`  
```

## Login (auth)
- **URL:** `/auth/login/`  
- **Method:** `POST` 
- **Description:** Authenticate and receive an access token. Positive case returns 200 with token.Negative cases: invalid credentials (401), missing fields (400).  

**Request:**  
```json
{
  "username": "loan.officer",
  "password": "Test@123"
}
```
**Response for success 200 OK**
```json
{
    "status": "success",
    "token": "eyMockToken123456789.placeholder",
    "expiresIn": 3600,
    "issuedAt": "2025-01-20T10:20:30Z",
    "roles": [
        "LoanOfficer",
        "ReadOnlyUser"
    ]
}
```
**Response for invalid credentials- 400 Bad Request**
```json
{
  "status": "error",
  "errorCode": "ERR_INVALID_CREDENTIALS",
  "message": "Invalid username or password."
}
```

