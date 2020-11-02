# paanda.io - public documentation

https://paanda.io

## Basics

- [REST API introduction](/core-api)  
- [REST API Authentication](/core-api/01-authentication.md)  
- [Builtin Roles](/core-api/02-roles.md) 

## Engine

Paanda is built on three layer concept, every operation is available as rest API


- **DATA ACCESS**     SRS file format , Extract Transform Load data.
  - [Connections](/srs-api/02-connections.md)  
  - [Parameters](/srs-api/03-Parameters.md)  
  - [Commands](/srs-api/04-commands.md)  
  - [Columns](/srs-api/05-columns.md)  
  - [Options](/srs-api/06-options.md)  
  - [Targets](/srs-api/08-targets.md)
  - [Permissions](/srs-api/09-permissions.md)
  - [Renderer](/srs-api/11-renderer.md)
- **CORE**
  - [REST Examples SRS file format processor](/srs-api/12-rest-examples.md) 
  - USER MANAGMENT LAYER
    - ACCOUNTS
    - TEAMS
    - ROLES
  - STORAGE 
- **App**
  - [User Interface and app structure](/ui-api/README.md) 
  Supports: Live preview, custom UI for every app

## Extensions

### ERP/MRP API (PL)

- [ERP WSTĘP](/erp-api)  
- Documents
  - [REST API Dokument przyjęcie PZ,PZI..](/erp-api/document/documentin.md) 
  - [REST API Dokument Wydania RW,RWP](/erp-api/document/documentout.md))
  - [REST API Faktura zakupu, Faktura VAT](/erp-api/document/invoice.md))
  - [REST API ZAMÓWIENIE](/erp-api/document/order.md)
  - [REST API UMOWY I PODPISY](/erp-api/document/agreement.md)
  - Zlecenie Produkcyjne
  - Zlecenie Serwisowe
- [ERP Helpers](/erp-api/helpers)  
  - [Currency Exchange](/erp-api/helpers/currencyexchange.md)
  - [Geolocation](/erp-api/helpers/geolocation.md)
  - [Barcode](/erp-api/helpers/barcode.md)
  - [QRCODE](/erp-api/helpers/qrcode.md)
  - [VAT](/erp-api/helpers/vat.md)
  
## Versions

| FEATURE | CLOUD | DATA CENTER | SERVER |
| --- | --- | --- | --- |
| --- | Availabe at paanda.io | Dedicated server | Your infrastructure |
| Connection Manager | YES | YES | YES |
| EXCEL provider | YES | YES | YES |
| SQL Server Provider | YES | YES | YES |
| Oracle Provider | - | - | YES |
| PostgreSQL Provider | - | - | YES |
| File system provider | - | - | YES |
| Own UI | - | YES | YES |

