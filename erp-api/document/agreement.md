# Umowy

## User interface

v_agreement komponent
https://app.paanda.io/pages/erp/agreement - interface

## 1 Pobranie  umowy

***Request***

GET {host}/api/erp/agreement/get/{app_name}/{agreementid}

***Response***

data.document - nagłówek ( SQL PROCEDURE erp.agreement_get)
data.documentline - pozycje ( SQL PROCEDURE erp.documentline_list)
