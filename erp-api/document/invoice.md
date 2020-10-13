---
status: ALPHA
language: PL
title: "API Faktura Zakupu / Sprzedaży"
required-app: platformaERP
---
## INFO

Na razie w procedurze [erp].[invoice_InsertUpdate] @invoiceCategory jest ustawione na (5). Większe wartości mogą wyrzucać błąd (Potrzebna zmiana wielkości w tabeli docelowej).

## TODO

- [x] wystawianie faktury z kontekstu dokumentów
- [ ] kopia faktury

API kopiowanie faktury

```sql
  sql.execute("[document].[invoice_copy]"
  , new { username = cc.auth.profile.userName(), sourceInvoiceID = sourceInvoiceID, invoiceID = invoiceID, invoiceIssueDate = invoiceIssueDate, 
  resultInvoiceType = resultInvoiceType, copyAutoAssignItemTaxRatesAndCalculateTax = copyAutoAssignItemTaxRatesAndCalculateTax });
```

- [ ] usuniecie pozycji

# Faktura 

## 1 DB - Objects

### Tabele
- [document].invoice - nagłówek faktury
  - invoiceCategory - typ dokumentu
  - invoiceIssueDate - data wystawienia faktury
- [document].invoiceline - pozycje faktury

### Procedury
- [erp].[invoice_InsertUpdate] - dodanie / aktualizacja nagłówka
- [erp].[invoice_get] - pobranie danych z faktury
- [erp].[invoiceLine_InsertUpdate] - dodanie / akutalizacja pozycji faktury
- [erp].[invoiceline_list] - lista pozycji faktury

### Słowniki:
#### Przykłady słowników
	- Słownik magazynów (warehouse),
	- Typy faktur (purchaseInvoiceTypes),
	- Słownik walut (currency),
	- Słownik jednostki miar (itemUnit),
  - Słownik stawek podatku (taxrate),
  - Słownik sposobów dostawy (termsofdelivery),
  - Słownik wydziałów (organisationunit),
  - Słownik sposobów płatności (paymenttype)
	
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

## 2. Ustawienia / zmienne / parametry

### General

- {app_name} moze byc zastapiony [[app_name]]

### Parametry
- `instance.sales.advanceindex` - Indeks zaliczkowy używany przy wystawianiu zaliczki z zamówienia sprzedażowego"
- `instance.salesparts.advanceindex` - indeks zaliczkowy dla zamowienia sprzedaży czesci
- `instance.purchase.defaultPaymentType`  - (obsolete) Domyślna wartość sposobu płatności na fakturze zakupu

## 3 UI - User Interface

- Faktura zakupu przykład / platformaERP https://master.platformacrm.pl/ERP/invoicePurchase/8c0c19b2-86f2-ea11-a98a-060c7c3ef0b7
- komponent: v_invoice_purchase
- localhost/pages/erp/v-invoice-purchase?app_name=platformaerp - (client) interface faktury
- Wymagany app_name

### Przykład

```localhost:5500/pages/erp/v-invoice-purchase?app_name=platformaerp``` - tworzenie nowego dokumentu

## 10 API - REST API

## 10.1 API Pobranie faktury

***REQUEST***

```http
GET {host}/api/erp/invoice/get/{app_name}/{invoice_id}
```

***RESPONSE***

- JSON
  - invoice
  - invoiceline

***DB***

- [erp].[invoice_get]
- [erp].[invoiceline_list]

## 10.2 API Zapisanie nagłówka i pozycji

**Request**

Zapisanie nagłówka

```http
POST {host}/api/erp/invoice/set-header/{app_name}/{invoiceid}
```

Zapisanie pozycji

```http
POST {host}/api/erp/invoice/set-line/{app_name}/{invoiceid}
```

***DB***

- [erp].[invoice_InsertUpdate]
- [erp].[invoiceLine_InsertUpdate]



