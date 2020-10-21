# Barcode API

Barcode API will generate Code128 Barcode

## 10 REST API

### 10.01 GEt BARCODE

- code - Valid EAN 128 CODE
- label [true/false] , default true

***Request***

Http

```http
GET {{host}}/api/erp/barcode?code={code}&label={label}
Authorization: Bearer {{token}}
```

HTML

```html
<img src="/api/erp/barcode?code={code}&label={label}" class="w3-image"  :alt="code">
```

Markdown

```md
![Barcode](/api/erp/barcode?code={code}&label={label})
```

***Response***

Barcode 
