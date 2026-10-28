# API reference (detailed)

This endpoint verifies a user’s identity before they can access the loan application portal and protected services. Staff sign in with a username and password to search, review, and manage loan records securely. Once the credentials are validated, the API returns a JWT that authorizes subsequent requests. This approach keeps access controlled, supports role-based permissions, and maintains a secure session for daily loan operations.

## Login (auth)
- **URL:** `/auth/login`
- **Method:** `POST`
- **Authentication:** Not required for this endpoint
- **Content-Type:** `application/json`
- **Description:** Validates a user’s credentials and returns an access token for subsequent authenticated requests. Positive case returns `200 OK` with token details; negative cases include invalid credentials, missing fields, and server-side authentication failures.

<swagger-ui src="https://sheethalu.github.io/Documentation-Portal/swagger.yaml" filter="Authentication"></swagger-ui>

## AUTHENTICATION API – SCHEMAS

**Model: AuthRequest**

| Field    | Type   | Required | Description                     |
| -------- | ------ | -------- | ------------------------------- |
| username | string | Yes      | Login username of the user.     |
| password | string | Yes      | Account password. |

**AuthRequest**
```yaml
username: `string (required)`
password: `string (required)`
```



| Field     | Type             | Required | Description                                    |
| --------- | ---------------- | -------- | ---------------------------------------------- |
| status    | string           | Yes      | Response status returned by the authentication service. |
| token     | string (JWT)     | Yes      | Access token used for authentication. |
| expiresIn | number           | Yes      | Expiration time in seconds. |
| issuedAt  | string (ISO 8601) | Yes      | Timestamp when the token was issued. |
| roles     | array[string]    | Yes      | The user’s roles and permissions. |

**AuthResponse**
```yaml
status: `string`
token: `string (JWT)`
expiresIn: `number`
issuedAt: `string (ISO 8601 datetime)`
roles: `array[string]`
```

### Example request

```json
{
  "username": "loan.officer",
  "password": "Test@123"
}
```

### Success response: `200 OK`

```json
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1Ni...",
  "expiresIn": 3600,
  "issuedAt": "2025-01-20T10:20:30Z",
  "roles": [
    "LoanOfficer",
    "ReadOnlyUser"
  ]
}
```

### Error responses

- `400 Bad Request` — Missing or malformed request fields such as `username` or `password`.
- `401 Unauthorized` — Invalid username or password.
- `500 Internal Server Error` — Authentication service failure or unexpected backend error.

**Example: `400 Bad Request`**
```json
{
  "status": "error",
  "errorCode": "INVALID_INPUT",
  "message": "username and password are required"
}
```

**Example: `401 Unauthorized`**
```json
{
  "status": "error",
  "errorCode": "ERR_INVALID_CREDENTIALS",
  "message": "Invalid username or password."
}
```

**Example: `500 Internal Server Error`**
```json
{
  "status": "error",
  "errorCode": "AUTH_SERVER_ERROR",
  "message": "Authentication service unavailable."
}
```
