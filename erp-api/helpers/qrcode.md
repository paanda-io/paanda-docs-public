# QRCode API

## Summary


## 10 REST API

### 10.01 GET QRCODE


***Request***

Http

```http
GET {host}/api/erp/qrcode?code={code}
Authorization: Bearer {token}
```

HTML

```html
<img src="/api/erp/qrcode?code={code}" class="w3-image"  alt="QRCODE">
```

Markdown

```md
![QRCODE](/api/erp/qrcode?code={code})
```

***Response***

QRCODE 
