
status: ALPHA
language: PL
title: "API Umowy"
required-app: paanda, platformaERP

# Umowy

## 1 DB - Objects

-   [document].[agreement] - umowy, umowy ramowe, specyfikacje do zamówień
    
-   [document].[signature] - podpisy elektroniczne do dokumentów
    
    -   signature_id
        
    -   signature_email
        
    -   signature_phone_number
        
    -   signature_first_name
        
    -   signature_last_name
        
    -   signature_company_name
        
    -   signature_company_vat
        
    -   signature_remote_id
        
    -   signature_remote_source
        
    -   signature_sign_date
        
    -   signature_ip
        
    -   signature_hash - document_hash
        
-   [common].[bankAccount] - konta bankowe zamawiającego
    
-   [erp].[bankAccount_List] - pobranie listy kont
    
-   [erp].[signature_List] - pobranie listy podpisów elektronicznych
    
-   [erp].[agreement_InsertUpdate] - zapisanie umowy
    
-   [erp].[agreement_get] pobranie umowy
    
-   [erp].[agreement_list] lista umow
    

## 2 Settings/Variables

-   instance.sales.seller domyslny nabywca `select value from configuration.configuration where configurationID ='instance.sales.seller`
    

## 3 UI - User interface

-   platformaerp :: /pages/erp/v_agreement - komponent
    
-   [https://app.paanda.io/pages/erp/agreement](https://app.paanda.io/pages/erp/agreement) - interface
    

## 10 API - REST API

### 10.1 Pobranie umowy

**_Request_**
```http
GET {host}/api/erp/agreement/get/{app_name}/{agreementid}
```

**_Response structure_**

-   data
    
    -   agreement - nagłówek
        
    -   signature_list - lista podpisów wraz z statusem
        
    -   bankaccount_list - lisa kont bankowych zamawiającego
        

### 10.2 Zapisanie umowy

**_Request_**
```http
GET {host}/api/erp/agreement/set/{app_name}/{agreementid}
```

**_Response_**

STATUS 200
