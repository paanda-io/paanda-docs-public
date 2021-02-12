---
status: ALPHA
language: PL
title: "API Dokument przyjęcia"
required-app: paanda, platformaERP
---

# Dokument przyjęcia PZ,PZI,PW ...

## 1 DB - Objects

### Tabele
- [document].[document] - dokument, 
- [document].[documentLine] - pozycje dokumentu

### Procedury
- [erp].[document_get] - pobranie zamówienia i listę pozycji
- [erp].[document_InsertUpdate] - zapis / aktualizacja zamówienia
- [erp].[document_updateDocumentStatus] - aktualizacja statusu dokumentu
- [erp].[documentline_List] - pobranie listy pozycji dokumentu 
- [erp].[documentline_InsertUpdate] - zapis / aktualizacja pozycji zamówienia

### Słowniki:
#### Przykłady słowników
	- Słownik magazynów,
	- Typy dokumentów,
	- Słownik walut,
	- Słownik jednostki miar,
	
**Response**
#### Procedura
	- data.list  ( SQL PROCEDURE [erp].[dictionary_bynameValue])

**Request**

```http
{host}/api/erp/dictionary/browse/{app_name}/{dictionary_name}
```

**Przykład użycia dla `Słownik magazynów (warehouse)`**

```http
GET {host}/api/erp/dictionary/browse/{app_name}/warehouse
```

## 2 Ustawienia / zmienne

### General

**documentStatus - status dokumentu**

- status
  - `-1` usuniety
  - `0`  szkic
  - `>0` zatwierdzony
- `{app_name}` moze byc zastapiony `[[app_name]]`

### Konfiguracja kolumn

- tabela [dbo].[columns ]

##  3 UI - User interface

- `v_documentin`  komponent
- https://app.paanda.io/pages/erp/documentin - interface


## 10 API - REST API
### 10.1 Pobranie pozycji i dokumentu

**Request**

```http
GET {host}/api/erp/document/get/{app_name}/{document_id}
```

**Response**

- data.document - nagłówek   ( SQL PROCEDURE erp.document_get)
- data.documentline - pozycje  ( SQL PROCEDURE erp.documentline_list)

### 10.2 Kartoteka firm 

**Request**

- query wyszukiwanie

```http
GET {host}/api/erp/firm/browse/platformaerp/documentin?query=
```

**Response**

- data.list - lista firm ( SQL PROCEDURE erp.firm_list)

### 10.3 Kartotek indeksów dla dokumentu PZ

**Request**

-  query jest opcjonalne filtrowanie

```http
GET {host}/api/erp/item/browse/platformaerp/documentin?query=pudelko
```

```sql
--DEPRECATED
exec [wms].[item_ListForDocument_dictionary] 
@search=N'3053753438968717823',@username=N'demo',@documentId=N'da1dfb86-426d-eb11-9e6c-e4a471566cb9',@warehouseId=N'aa54e854-0f94-e911-80d8-9c8e994dc647'

--NEW
exec [erp].[item_list] 
@dictionary=N'documentin',@username=N'marcin@kotynia.com',@query=N'BLACHA 1.4828 AISI 309',@warehouseId=N'aa54e854-0f94-e911-80d8-9c8e994dc647'

```

**Response**

- data.list - lista firm ( SQL PROCEDURE erp.item_list)

### 10.4 Dokument,  zapisanie nagłówka , zapisanie pozycji , usuwanie pozycji

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

###  10.5 Zatwierdzenie dokumentu , usunięcie dokumentu

**Request**

Zatwierdzenie

```http
{host}/api/erp/document/set-status/platformaerp/{documentid}
```

Usunięcie

```http
/api/erp/document/set-status/platformaerp/{documentid}?status=-1
```

### 10.6 Pobieranie listy zamówień nie zrealizowanych do dokumentu PZ

**User interface**

Otwarte linie oznaczaja pozycje nie zrealizowane przykład.
Żeby wygenerować przykład należy dodac zamowienie zewnętrzne 
dla firmy anstepnie wystawić dokuemnt PZ/PZI dla tego samego kontrahenta

{host}/#/pages/erp/v-documentin?documentid={documentid}

**Request**

```http
/api/erp/document/open-order-lines/{app_name}/{documentid}
```

### 10.7 Dodanie pozycji zamówienia do dokumentu

**Request**

```http
POST /api/erp/document/orderline-close/{app_name}/{orderlineid}/{documentid}
```

### 10.8 Zlecenia do typu dokumentu PW

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
