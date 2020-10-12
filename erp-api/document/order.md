
---
status: ALPHA
language: PL
title: "API Zamówienia"
required-app: paanda, platformaERP
---

# Dokument zamówienia ZZW, ZP, ZS, ZO...

## Zamówienia

## 1 Obiekty Bazy Danych

### Tabele
- [document].[order] - zamównienia, 
  - orderID
  - orderNR
  - orderFullNR
  - orderTypeID
  - orderExpectedDate
  - orderMemo
  - orderStatus
  - deliveryFirmID
  - isPriceVisible
  - paymentTypeID
  - deliveryWayID
  - currencyID
  - paymentTime
  - warehouseID
  - currencyExchangeRate
  - termsOfDelivery
- [document].[orderLine]
  - orderLineID
  - orderID
  - itemUnitOrderID
  - itemID
  - itemPrice
  - itemQuantity
  - itemValue
  - itemTaxRate
  - itemConvertUnitID
### Procedury
- [erp].[order_get] - pobranie zamówienia i listę pozycji
- [erp].[order_InsertUpdate] - zapis / aktualizacja zamówienia
- [erp].[UpdateOrderStatus] - 
- [erp].[orderLine_document] - 
- [erp].[orderLine_InsertUpdate] - zapis / aktualizacja pozycji zamówienia
- [erp].[orderline_List] - 
### Słowniki:
 - Słownik magazynów,
 - Słownik sposobu dostawy,
 - Słownik walut,
 - Słownik sposobu płatności,
 - Słownik jednostek miary,
 - Słownik typów dokumentów zamówienia,
 - Słownik stawek VAT.

**Przykład użycia dla `warehouse`**

```http 
GET {host}/api/erp/dictionary/browse/{app_name}/warehouse
```

## 2 Ustawienia / Zmienne 

**orderStatus - status dokumentu zamówienia**

## General 

- status
  - `-1` usuniety
  - `0`  szkic
  - `>0` zatwierdzony
- `{app_name}` moze byc zastapiony `[[app_name]]`

## 3 UI - User Interface

- `v_order`  komponent
- https://app.paanda.io/pages/erp/v-order - interface

## 4 Nagłówek zamówienia 

Rodzaj zamówienia - `description`

Data wystawienia zamówienia - `orderDate`

Data faktury - `orderExpectedDate`

Miejsce dostawy/odbioru - `deliveryFirmID` **Endpoint miejsc dostaw/odbioru**

Adres dostawy - na razie nieobsłużone

Magazyn - `warehouseID` **Słownik Magazynów**

Nr zamówienia klienta - `orderfullnr2` ?

Uwagi faktury - `commentsToInvoice`

Warunki dostawy - `termsOfDelivery`

Firma - `firmID` **Endpoint firm** 

NIP - `taxCode`

Sposób płatności - `paymentTypeID`  **Słownik sposobu płatności**

Sposób dostawy - `deliveryWayID` **Słownik sposobu dostawy**

Waluta - `currencyID` **Słownik walut**

Data kursu - `currencyExchangeDate`

Kurs - `currencyExchangeRate`

## 10 API - REST API
### 10.1 Pobranie pozycji zamówienia (orderlines) i nagłówek zamówienia (order)

**Request**

```http
GET {host}/api/erp/order/get/{app_name}/{orderID}
```

**Response**

- data.order - nagłówek zamówienia  ( SQL PROCEDURE erp.order_get)
- data.orderline - pozycje zamówienia  ( SQL PROCEDURE erp.orderline_List)

### 10.2 Kartoteki:

**Request**

### Kartkoteki Firm:

```http
GET {host}/api/erp/firm/browse/{app_name}/order
```

### Kartoteki Miejsc dostawy/odbioru:

```http
GET {host}/api/erp/firm/browse/{app_name}/orderDelivery
```

### 10.3 Zapisanie nagłówka 

**Request**

Zapisanie nagłówka

```http
POST {host}/api/erp/order/set-header/{app_name}/{orderid}
```


**Example JS**

```js

//zapisanie nagłówka
this.genericPost('/api/erp/order/set-header/{app_name}/{orderid}', this.api.data.order);

```

### 10.4 Zatwierdzenie zamówienia , usunięcie zamówienia

**Request**

Zatwierdzenie

```http
{host}/api/erp/order/set-status/{app_name}/{orderid}
```

Usunięcie

```http
{host}/api/erp/order/set-status/{app_name}/{orderid}?status=-1
```

### 10.5 Tabela pozycji zamówień:

Indeks Mag. - `orderline.itemcode`  
Nazwa - `orderline.itemOrderName`  
JM. - `orderline.dictionaryValue`  
Ilość - `orderline.itemQuantity`  
Cena - `orderline.itemPrice`  
Zrealiz. - Co tutaj ?  
Wartość Netto - `orderline.itemValue`  
Oczekiwana/ Potwierdzona data - `orderline.orderLineExpectedDate`  

### 10.6 Dodawanie/ usuwanie pozycji zamówienia

Zapisanie pozycji

```http
POST {host}/api/erp/order/set-line/{app_name}/{orderid}
```

Usuniecie pozycji

```http
POST {host}/api/erp/order/delete-line/{app_name}/{orderLineID}
```

**Example JS**

```js

//usuniecie pozycji
this.genericPost('/api/erp/order/delete-line/{app_name}/{orderLineID}', this.api.data.orderline[index],this.fetchData);

//zapisanie pozycji
this.genericPost('/api/erp/order/set-line/{app_name}/{orderid}', this.api.data.orderline, this.fetchData);

```


### 10.7 Pobranie listy indeksów do dodawania pozycji w zamównieniu

*Request*

> Wymagane podanie orderid wtedy zostanie przypisana waluta i firma zamówienia , mozna też przekazać firmid

```http
GET {host}/api/erp/dictionary/browse/{app_name}/items-for-order?true&query=PUDELKO3&orderid=3506685c-3128-484e-8e2a-36d3097217f2
```


### 10.8 Profil użytkownika np zeby dostac user_app_name

*Request*

```
GET {host}/account/profile
```



