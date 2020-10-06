## VAT API

VAT API sprawdza status polskiego kontrahenta w wykazie podmiotów zarejestrowanych jako podatnicy VAT, niezarejestrowanych oraz wykreślonych i przywróconych do rejestru VAT, https://www.podatki.gov.pl/wykaz-podatnikow-vat-wyszukiwarka#

- Wartości zapisuje
- system zabezpiecza, przed wielokrotnym wywołaniem API
- wywołania API generuje "Status badge".

```http
GET {{host}}/api/erp/vat/check/{app_name}/{type?}
Authorization: Bearer {{token}}
```

```html
<img src="/api/erp/vat/check/platformaerp" title="VAT API Status"/>
```
