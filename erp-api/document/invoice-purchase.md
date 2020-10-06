---
status: ALPHA
language: PL
title: "API Faktura Zakupu / Sprzedaży"
---


# Faktura 

- Faktura zakupu przykład / platformaERP https://master.platformacrm.pl/ERP/invoicePurchase/8c0c19b2-86f2-ea11-a98a-060c7c3ef0b7
- komponent: v_invoice_purchase

## TODO

- [ ] wystawianie faktury z kontekstu dokumentów
- [ ] kopia faktury
- [ ] usuniecie pozycji

## DB obiekty

- [document].invoice
- [document].invoiceline
- [erp].[invoice_InsertUpdate]


## Parametry

- `instance.sales.advanceindex` - Indeks zaliczkowy używany przy wystawianiu zaliczki z zamówienia sprzedażowego"
- `instance.salesparts.advanceindex` - indeks zaliczkowy dl azamowienia sprzedazy czesci
- `instance.purchase.defaultPaymentType`  - (obsolete) Domyślna wartość sposobu płatności na fakturze zakupu

## 2 API Pobranie dokumentu

***REQUEST***

```http
GET {host}/api/erp/invoice/get/{app_name}/{document_id}
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