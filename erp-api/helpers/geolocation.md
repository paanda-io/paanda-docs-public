## Geolocation API

Geolocation API zmienia adres obiektu np: kontrahenta/produktu
na długość i szerokość geograficzną w celu wizualizacji na mapie.

- Wartości zapisuje w kartotece produktu/kontrahenta
- system zabezpiecza, przed wielokrotnym wywołaniem API
- wywołania API generuje "Status badge".

### Wymagania

- Google API key

### Przykłady

```http
GET {{host}}/api/erp/geolocation/check/{app_name}/{type?}
Authorization: Bearer {{token}}
```

Aby go użyć wystarczy umieścić odpowiedni link

```html
<img src="/api/erp/geolocation/check/platformaerp" title="Geolocation API Status"/>
```