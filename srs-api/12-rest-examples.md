# SRS File Format processor

SRS file format processor transform Paanda file definition to operations. 

## Quickstart REST API

```http
GET {host}/api/srs/{app_name}/{srs_name}/{renderer}?ptype={ptype}&ptoken={bearertoken}
Authorization: Bearer {{token}}
```

```http
POST {host}/api/srs/{app_name}/{srs_name}/{renderer}?{querystring}&ptoken={bearertoken}
Authorization: Bearer {{token}}
{
    "param1": "value1",
    "param2": "value2"
}
```

- `ptype` optional token reaplacing header token
- `ptype` optional type of expeceted response (default JSON) 
- `app_name` application context **REQUIRED**
- `srs_name` SRS definition name **REQUIRED** 
- `renderer` renderer **OPTIONAL**
- `querystring` **OPTIONAL** all query strings value are passed to engine
- **renderer** if  contains ANY string SRS is executed against data sources


## Examples


### GET  BADGE

**Request**

```http
GET {{host}}/api/srs/{app_name}/view?ptype=svg
```

**Response**

image

### Run Definition

Nothing happens here just return definition without executing any command

```http
GET {{host}}/api/srs/examples/hello-parameters HTTP/1.1
Authorization: Bearer {{token}}
```

### GET JSON

Any renderer will execute command  

```http
GET {{host}}/api/srs/examples/hello-parameters/1 HTTP/1.1
Authorization: Bearer {{token}}
```

## GET EXCEL

```http3
GET {{host}}/api/srs/examples/hello-parameters/1?ptype=xlsx HTTP/1.1

Authorization: Bearer {{token}}
```

## Example API request

```htttp
GET {host}/api/srs/{app_name}/{srs_name}/{srs renderer]}?[parameters]&ptype=[target type]&ptoken=[bearertoken]
```

```htttp
POST {host}/api/srs/{app_name}/{srs_name}/{srs renderer]}?[parameters]&ptype=[target type]&ptoken=[bearertoken]
```
