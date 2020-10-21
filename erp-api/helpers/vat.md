# VAT API

VAT API sprawdza status polskiego kontrahenta w wykazie podmiotów zarejestrowanych jako podatnicy VAT, niezarejestrowanych oraz wykreślonych i przywróconych do rejestru VAT, https://www.podatki.gov.pl/wykaz-podatnikow-vat-wyszukiwarka#

## Wymagane obiekty 

```sql
        CREATE TABLE [dbo].[vat] (
        	[vat_id] [int] IDENTITY(1,1) NOT NULL,
        	[vat_nip] [varchar](20) NULL,
        	[vat_date] [date] NULL,
        	[vat_status] [varchar](50) NULL,
        	[vat_body] [xml] NULL,
         CONSTRAINT [PK_vat] PRIMARY KEY CLUSTERED 
        (
        	[vat_id] ASC
        ))
```

## Weryfikacja status pojedynczego podatnika i opcjonalnie konta bankowego JSON

 "vat_status":"INVALID Bank Account" - nieprawidłowe konto

***Request***

- Wymagany obiekt [dbo].[vat] w paanda.db

```http
GET {{host}}/api/erp/vat/get-status/{VATNumber}/{AccountNumber?}
Authorization: Bearer {{token}}
```

***Response***

```json
{
   "vat_nip":"7272351852",
   "vat_date":"2020-10-21",
   "vat_status":"Czynny",
   "vat_data":{
      "Subject":{
         "Name":"XXXXX XXXXX",
         "Nip":"7272351852",
         "StatusVat":"Czynny",
         "Regon":"100522920",
         "ResidenceAddress":"XXXXX XXXXX XXXXX, XXXXX-XXXXX XXXXX",
         "RegistrationLegalDate":null,
         "RestorationBasis":"Art. 96 ust. 9h",
         "RestorationDate":null,
         "AccountNumbers":{
            "string":"56114020040000310277283312"
         },
         "HasVirtualAccounts":"false"
      }
   }
}
```

## Weryfikacja status pojedynczego podatnika BADGE

"vat_status":"INVALID Bank Account" - nieprawidłowe konto
"vat_status":"Czynny" - OK

***Request***

- Wymagany obiekt [dbo].[vat] w paanda.db

```http
GET {{host}}/api/erp/vat/get-badge/{VATNumber}/{AccountNumber?}
Authorization: Bearer {{token}}
```

***Response***

IMAGE


## Aktualizacja statusu VAT dla platformaERP

System weryfikuje status podatnika raz na 3 dni.

- Wymagany obiekt [dbo].[vat] w połaczeniu
- Wymagany obiekt [firm].[firm]  w połączeniu

***Request***

```http
GET {{host}}/api/erp/vat/check/{app_name}
Authorization: Bearer {{token}}
```

***Request***

Badge with information

- VAT:OK - dane aktualne
- VAT:OK(number) - ilość sprawdzonych podaczas sesji
- VAT:(status błedu) - informacja o błedzie


```html
<img src="/api/erp/vat/check/platformaerp" title="VAT API Status"/>
```


## Deprecated (Wycofane)

### Pobieranie z rejestru REGON

***Request***

```http
/api/regon/nip/{nip}
```

***Response***

JSON



