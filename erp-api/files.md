
## FILES API

Pobranie pliku z repozytorium

Opcjonalne parametry  

- szerokość np: ```w=300```
- wysokość ```h=100```
- opcje specjalne ```o=e```  "Entropy crop" 
- name= ```name=test.jpg``` nazwa pliku pobranego

```http
GET {{host}}/api/erp/files/platformaerp/{fileRepositoryID-token}/{remoteID-token}
Authorization: Bearer {{token}}

//Przykład z opcjonalnym parametrem
GET {{host}}/api/erp/files/platformaerp/{fileRepositoryID-token}/{remoteID-token}?w=400
Authorization: Bearer {{token}}
```
