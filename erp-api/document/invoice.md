---
status: ALPHA
language: PL
title: "API Faktura Zakupu / Sprzedaży"
required-app: platformaERP
---
## TODO

- [x] wystawianie faktury z kontekstu dokumentów
- [ ] kopia faktury
- [ ] usuniecie pozycji

# Faktura 

## 1 DB - Objects

### Tabele
- [document].invoice
  - invoiceCategory - typ dokumentu
  - invoiceIssueDate - data wystawienia faktury
- [document].invoiceline

### Procedury
- [erp].[invoice_InsertUpdate]
- [erp].[invoice_get]
- [erp].[invoiceLine_InsertUpdate]
- [erp].[invoiceline_list]


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

localhost:/pages/erp/v-invoice-purchase?app_name=platformaerp - tworzenie nowego dokumentu


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

## 3 API Zapisanie nagłówka i pozycji

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


## 4 TODO API kopiowanie faktury

```sql
            sql.execute("[document].[invoice_copy]"
                , new { username = cc.auth.profile.userName(), sourceInvoiceID = sourceInvoiceID, invoiceID = invoiceID, invoiceIssueDate = invoiceIssueDate, resultInvoiceType = resultInvoiceType, copyAutoAssignItemTaxRatesAndCalculateTax = copyAutoAssignItemTaxRatesAndCalculateTax });

```
