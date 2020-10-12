# SRS File Format processor

SRS file format processor transform Paanda file definition to data operations. 

## Quickstart REST API

```http
GET {host}/api/srs/{app_name}/{srs_name}/{renderer}?ptype={ptype}&ptoken={bearertoken}&pformat={true}
Authorization: Bearer {{token}}
```

```http
POST {host}/api/srs/{app_name}/{srs_name}/{renderer}?ptype={ptype}&ptoken={bearertoken}&pformat={true}
Authorization: Bearer {{token}}
{
    "param1": "value1",
    "param2": "value2"
}
```


- `app_name` **REQUIRED** application context 
- `srs_name` **REQUIRED** SRS definition name 
- `ptoken`  **OPTIONAL** token reaplacing header token
- `pformat`  **OPTIONAL** pretty print
- `ptype`  **OPTIONAL** type of expeceted response (default JSON)  see targets list
- `renderer`  **OPTIONAL** renderer
- `querystring` **OPTIONAL** all query strings value are passed to processor
- `renderer`  **OPTIONAL** if  contains ANY string SRS is executed against data sources


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

