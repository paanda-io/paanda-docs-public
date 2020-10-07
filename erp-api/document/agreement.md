# Umowy

## 1 DB - Objects

- [document].[Agreement] - tabela z umowami
- [erp].[agreement_InsertUpdate] - zapisanie  umowy
- [erp].[agreement_get] pobranie umowy
- [erp].[agreement_list]  lista umow

## 2 Settings/Variables

- instance.sales.seller domyslny nabywca `select value from configuration.configuration where configurationID ='instance.sales.seller`

## 3 UI - User interface

v_agreement komponent
https://app.paanda.io/pages/erp/agreement - interface


## 10 API - REST API

### 10.1 Pobranie  umowy

***Request***

```http
GET {host}/api/erp/agreement/get/{app_name}/{agreementid}
```

Request example 

```http
https://app.paanda.io/api/erp/agreement/get/platformaerp/62443958-11c5-4cda-8d78-d2eab43d9fd0
```

***Response***

data.agreement - nagłówek (db: erp.agreement_get)



### 10.2 Zapisanie umowy 

***Request***

```http
GET {host}/api/erp/agreement/set/{app_name}/{agreementid}
```

Request example 

```http
https://app.paanda.io/api/erp/agreement/set/platformaerp/62443958-11c5-4cda-8d78-d2eab43d9fd0
```

***Response***

STATUS 200 

