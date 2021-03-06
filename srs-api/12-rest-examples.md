# SRS File Format processor

SRS file format processor transform Paanda file definition to data operations. 

## Quickstart REST API

```http
GET {host}/api/srs/{app_name}/{srs_name}/{renderer}?ptype={ptype}
Authorization: Bearer {{token}}
```

```http
POST {host}/api/srs/{app_name}/{srs_name}/{renderer}?ptype={ptype}
Authorization: Bearer {{token}}
{
    "param1": "value1",
    "param2": "value2"
}
```

- Authorization methods , three options are available:
  - `ptoken`  **OPTIONAL** query parameter
  - Authorization: Bearer method
  - Cookie ptoken
- `app_name` **REQUIRED** application context 
- `srs_name` **REQUIRED** SRS definition name 
- `pformat`  **OPTIONAL** pretty print (warning response type plain/Text) only for preview
- `ptype`  **OPTIONAL** type of rendered  [see target.type](/srs-api/08-targets.md#target-type)
- `pscope`  **OPTIONAL** limit execution to comma separated command names
- `renderer`  **OPTIONAL** any string will execute srs , preferred command.name or [see target.renderer](/srs-api/08-targets.md#target-renderer)
- `querystring` **OPTIONAL** all query strings value are passed to engine



## Examples


### GET  BADGE

**Request**

```http
GET {{host}}/api/srs/{app_name}/view?ptype=svg
```

**Response**

image


### GET EXCEL

```http
GET {{host}}/api/srs/examples/hello-parameters/1?ptype=xlsx

Authorization: Bearer {{token}}
```

