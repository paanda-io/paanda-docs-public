# SRS File Format processor

SRS file format processor transform Paanda file definition to data operations. 

## Quickstart REST API

```http
GET {host}/api/srs/{app_name}/{srs_name}/{command.name}?ptype={ptype}
Authorization: Bearer {{token}}
```

```http
POST {host}/api/srs/{app_name}/{srs_name}/{{command.name}?ptype={ptype}
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
- `ptype`  **OPTIONAL** type of rendered  [see target:type](/srs-api/08-targets.md#target-type)
- `command.name`  **OPTIONAL** preferred command.name or target.renderer
- `querystring` **OPTIONAL** all query strings value are passed to processor


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

