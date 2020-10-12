# Paanda - public documentation

## Basics

- [REST API introduction](/core-api)  
- [REST API Authentication](/core-api/01-authentication.md)  
- [Builtin Roles](/core-api/02-roles.md) 

## Engine

Paanda is built on three layer concept, every operation is available as rest API


- **DATA ACCESS**     SRS file format , Extract Transform Load data.
  - [FORMAT SPECIFICATION](/srs-api)  
- **CORE**
  - [SRS file format processor](/srs-api/12-rest-examples.md) 
  - USER MANAGMENT LAYER
    - ACCOUNTS
    - TEAMS
    - ROLES
  - STORAGE 
- **UI**
  - [User Interface](/ui-api/README.md) 
  Supports: Live preview, custom UI for every app

## CUSTOM EXTENSIONS

### ERP API (PL)

- [ERP WSTĘP](/erp-api)  
- [REST API Dokument przyjęcie PZ,PZI..](/erp-api/document/documentin.md) 
- [REST API Dokument Wydania RW,RWP](/erp-api/document/documentout.md))
- [REST API Faktura zakupu, Faktura VAT](/erp-api/document/invoice.md))
- [REST API ZAMÓWIENIE](/erp-api/document/order.md)
- [REST API UMOWY I PODPISY](/erp-api/document/agreement.md)
- Zlecenie Produkcyjne
- Zlecenie Serwisowe
- [REST API ERP HELPERS QRCODE, BARCODE, VAT , GEOLOCATION](/erp-api/helpers)  

## Versions

| FEATURE | CLOUD | DATA CENTER | SERVER |
| --- | --- | --- | --- |
| --- | Availabe at paanda.io | Dedicated server | You infrastructure |
| Connection Manager | YES | YES | YES |
| EXCEL provider | YES | YES | YES |
| SQL Server Provider | YES | YES | YES |
| Oracle Provider | - | - | YES |
| PostgreSQL Provider | - | - | YES |
| File system provider | - | - | YES |
| Own UI | - | YES | YES |

