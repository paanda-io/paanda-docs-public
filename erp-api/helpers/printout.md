---
status: ALPHA
language: PL
title: "API Wydruki ERP"
required-app: paanda, platformaERP
---

# Wydruki ERP
## 1 DB - Objects

- [configuration].[printout]
  - componentname ex: order,document,invoice ...
  - documenttype ex: RW,PZ,RWP,PW,ZW ...
  - action - url of action ex: `http://{host}:8081/jasperserver/rest_v2/reports/Reports/{path}/{printoutname}.pdf?paramId={id}&username=sys&REPORT_LOCALE=pl_PL&userLocale=pl_PL&db={db}&j_username=someusername&j_password=somepassword`
    - {db} 
    - {username}
    - {printoutname}
    - {id}
    - {any query string parameter}
    

## 2 Settings/Variables

N/A  

## 3 UI - User interface

N/A   
    
## 10 API - REST API


### 10.1 List of available printouts

**_Request_**
```http
GET {host}/api/erp/print/list/[[app_name]]/{componentname}/{documentType?}
```

**_Response structure_**

Json

### 10.2 Execute printout

**_Request_**
```http
GET {host}/api/erp/print/get/[[app_name]]/{printout_uuid}/{document token}
```

**_Response_**

application/PDF


### 10.3 REnder to application/pdf client side

**_Request_**
```http
GET {host}/api/print/url?url={encoded url}&ptoken={optional token}
```

**_Response_**

application/PDF

