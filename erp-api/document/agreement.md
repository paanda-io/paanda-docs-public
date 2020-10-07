# Umowy

## DB - Objects

- [document].[Agreement] - tabela z umowami
- [erp].[agreement_InsertUpdate] - dodawanie umowy
- [erp].[agreement_get] pobranie umowy
- [erp].[agreement_list]  lista umow

## UI - User interface

v_agreement komponent
https://app.paanda.io/pages/erp/agreement - interface

## API - REST API

### 1 Pobranie  umowy

***Request***

```http
GET {host}/api/erp/agreement/get/{app_name}/{agreementid}
```

Request example 

```http
https://app.paanda.io/api/erp/agreement/get/platformaerp/62443958-11c5-4cda-8d78-d2eab43d9fd0
```

***Response***

data.agreement - nagłówek ( SQL PROCEDURE erp.agreement_get)
