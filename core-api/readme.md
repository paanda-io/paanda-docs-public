# Introduction

The Paanda API is built on HTTP. API is RESTful and it:

- Uses predictable, resource-oriented URLs.
- Uses built-in HTTP capabilities for passing parameters and authentication.
- Responds with standard HTTP response codes to indicate errors.
- Returns JSON.

Example

```http
GET {host}/api/system/ping
```
Returns: Authorized or Not authorized

## Using REST API

Most of REST endpoints require authentiction (token).
Token can be provided using:

### Authorization header (recommended)

```http
GET {host}/api/system/ping
Authorization: Bearer {token}
```

### Cookie

Cookie format

```
Name = ptoken
Value = {{token}}
```

Request

```http
GET {{host}}/api/system/ping
```

### URL authorization parameter (not recommended)

```http
GET {{host}}/api/system/ping?ptoken={{token}}
```

## Response codes

Paanda returns standard HTTP response codes.

| Code | Description                                                  |
| :--- | :----------------------------------------------------------- |
| 200  | Everything worked as expected                                |
| 400  | Bad Request (client error) - Missing a required parameter, malformed request |
| 401  | Unauthorized - No valid API key provided                     |
| 403  | Forbidden The request was valid, but the server is refusing action. The user  not have the necessary permissions for a resource. |
| 404  | Not Found - The requested item doesn’t exist                 |
| 413  | Request Entity Too Large - Attachment size is too big        |
| 500  | Server Errors - something is wrong on Paanda end             |
