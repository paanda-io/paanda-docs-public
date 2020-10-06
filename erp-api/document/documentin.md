# Dokument przyjęcia PZ,PZI,PW ...

## User interface

- `v_documentin`  komponent
- https://app.paanda.io/pages/erp/documentin - interface

## General

**documentStatus - status dokumentu**

- status
  - `-1` usuniety
  - `0`  szkic
  - `>0` zatwierdzony
- `{app_name}` moze byc zastapiony `[[app_name]]`


## 1 Pobranie pozycji i dokumentu

**Request**

```http
GET {host}/api/erp/document/get/{app_name}/{document_id}
```

**Response**

- data.document - nagłówek   ( SQL PROCEDURE erp.document_get)
- data.documentline - pozycje  ( SQL PROCEDURE erp.documentline_list)

## 2 Kartoteka firm 

**Request**

- query wyszukiwanie

```http
GET {host}/api/erp/firm/browse/platformaerp/documentin?query=
```

**Response**

- data.list - lista firm ( SQL PROCEDURE erp.firm_list)

## 3 Kartotek indeksów dla dokumentu PZ

**Request**

-  query jest opcjonalne filtrowanie

```http
GET {host}/api/erp/item/browse/platformaerp/documentin?query=pudelko
```

**Response**

- data.list - lista firm ( SQL PROCEDURE erp.item_list)



## 5 Dokument,  zapisanie nagłówka , zapisanie pozycji , usuwanie pozycji

**Request**

Zapisanie nagłówka

```http
POST {host}/api/erp/document/set-header/{app_name}/{documentid}
```

Zapisanie pozycji

```http
POST {host}/api/erp/document/set-line/platformaerp/{documentid}
```

Usuniecie pozycji

```http
POST {host}/api/erp/document/delete-line/platformaerp/{documentid}
```

**Example JS**

```js
//zapisanie pozycji
this.genericPost('/api/erp/document/set-header/platformaerp/{documentid}', this.api.data.document);

//Usuwanie pozycji
this.genericPost('/api/erp/document/set-line/platformaerp/{documentid}', this.api.data.documentline,this.fetchData);

//usuwanie pozycji
this.genericPost('/api/erp/document/delete-line/platformaerp/{documentLineID}', this.api.data.documentline,this.fetchData);
```

## 6 Zatwierdzenie dokumentu , usunięcie dokumentu

**Request**

Zatwierdzenie

```http
{host}/api/erp/document/set-status/platformaerp/{documentid}
```

Usunięcie

```http
/api/erp/document/set-status/platformaerp/{documentid}?status=-1
```

##  7 Pobieranie listy zamówień nie zrealizowanych do dokumentu PZ

**User interface**

Otwarte linie oznaczaja pozycje nie zrealizowane przykład.
Żeby wygenerować przykład należy dodac zamowienie zewnętrzne 
dla firmy anstepnie wystawić dokuemnt PZ/PZI dla tego samego kontrahenta

{host}/#/pages/erp/v-documentin?documentid={documentid}

**Request**

```http
/api/erp/document/open-order-lines/{app_name}/{documentid}
```

## 8 Dodanie pozycji zamówienia do dokumentu

**Request**

```http
POST /api/erp/document/orderline-close/{app_name}/{orderlineid}/{documentid}
```

## 9 Słowniki



### Konfiguracja kolumn

- tabela [dbo].[columns ]

### Lista słowników przykłady 

agreementType , area , attributegroup, attributeRelationtype ,campaignLineStatus, campaignStatus , commisionCategory,contactPosition,countrycode, currency, deliverycode, **deliveryWay**, discountcategory, **firmType**, iEventStatus, itemcategory, itemgroup, itemsubcategory**itemUnit**, language, eadSource, leaduser ocationtype, MPK, offerrelationtype, offerType, operationType, opportunityStage, organisationUnit, packtype, paymentSheduleType, paymenttype, pkwiu, productFaultType, system, system.accountingAccountName, system.accountingVat, system.agreementStatus, system.commisionstatus, system.dictionaryname, system.distanceRateKM, system.documentstatus, system.inventoryStatus, system.invoiceStatus, system.offerStatus, **system.orderStatus**, **system.orderType (obsolete usedocument.documenttype)**, system.permission, system.role, system.sale, system.service, **system.taxrate**, team, technologyType,termsofdelivery

**Request**

```http
{host}/api/erp/dictionary/browse/{app_name}/{dictionary_name}
```

**Response**

- data.list  ( SQL PROCEDURE [erp].[dictionary_bynameValue])

### Słownik magazynów

**Request**

```http
GET {host}/api/erp/dictionary/browse/platformaerp/warehouse
```

### Typy dokumentów

**Request**

```http
{host}/api/erp/dictionary/browse/{app_name}/documenttype?query=documentin
```

###  Słownik walut

```http
{host}/api/erp/dictionary/browse/{app_name}/currency
```

###  Słownik jednostki miar

```http
{host}/api/erp/dictionary/browse/{app_name}/itemunit
```

## 11 Zlecenia do dokumentu pw



**Request**

Wybor zlecenia na naglowku [erp].[commision_List_dictionary]

```
{host}/api/erp/dictionary/browse/{app_name}/open-commision?query=
```



Wybor zlecenia na pozycji 

```
{host}/api/erp/dictionary/browse/{app_name}/commisionline-for-pw?query=&commisionId=&warehouseid=
```

Wybor lokacji na pozycji

```
{host/api/erp/dictionary/browse/{app_name}/location-by-warehouse?warehouseid=&query=&locationtypeid=&itemId=
```
