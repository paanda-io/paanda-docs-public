# Dokument wydania RW,RWP,WZ ...

## User interface

- `v_documentout`  komponent
- https://app.paanda.io/pages/erp/documentout - interface

## General

**documentStatus - status dokumentu**

- `-1` usuniety
- `0`  szkic
- `>0` zatwierdzony
- {app_name} moze byc zastapiony [[app_name]]

## 1 Pobranie pozycji i dokumentu

**Request**

```http
GET {host}/api/erp/document/get/platformaerp/{document_id}
```

**Response**

- data.document - nagłówek   ( SQL PROCEDURE erp.document_get)
- data.documentline - pozycje  ( SQL PROCEDURE erp.documentline_list)



## 2 Wydział



Słowniki są te same jak dla dokumentu przychodowegoPrzykład pozostałych słowników documentin > słowniki



**Request**

Wydział

```http
{host}/api/erp/dictionary/browse/{app_name}/organisationunit
```

**Response**

- data.list  ( SQL PROCEDURE [erp].[dictionary_bynameValue])

  

## 3 Kartotek indeksów dla dokumentu RW



**Obsolete SQL**

```sql 
--Według lokacji i numeru seryjnego

 exec [wms].[item_ListForDocumentOut_dictionary] @search=N'697058841718004716',
 @username=N'test35',@warehouseId=N'ff4df207-38b0-e611-93f6-f01fafe8ab47',
 @mode=1,@documentId=N'fdf4f367-d600-eb11-a98a-060c7c3ef0b7'
 
--OBSOLETE Wdług indeksu (bez rozbicia na lokacje i nr seryjne)
 
 exec [wms].[item_ListForDocumentOut_dictionary] @search=N'697058841718004716',@username=N'test35',@warehouseId=N'ff4df207-38b0-e611-93f6-f01fafe8ab47',
 @mode=5,@documentId=N'fdf4f367-d600-eb11-a98a-060c7c3ef0b7'

--OBSOLETE Wybór dostawy mode10

exec [wms].[item_ListForDocumentOut_dictionary] @search=N'697058841718004716',
@username=N'test35',@warehouseId=N'ff4df207-38b0-e611-93f6-f01fafe8ab47',
@mode=10,@documentId=N'fdf4f367-d600-eb11-a98a-060c7c3ef0b7'
```



**Request**

Według lokacji i numeru seryjnego



```http
GET {host}/api/erp/item/browse/{app_name}/documentout-by-location-serial
?query={ex: itemname,itemcode}&warehouseid={warehouseid}&documentid={documentid}
```

Według indeksu (bez rozbicia na lokacje i nr seryjne)

```http
GET {host}/api/erp/item/browse/{app_name}/documentout-by-item
?query={ex: itemname,itemcode}&warehouseid={warehouseid}&documentid={documentid}
```

Wybór dostawy



```http
GET {host}/api/erp/item/browse/platformaerp/documentin
?query={ex: itemname,itemcode}&warehouseid={warehouseid}&documentid={documentid}
```




**Response**

- data.list - lista firm ( SQL PROCEDURE erp.item_list - uwaga endpoitn generycnzy querystring przekazywany do procedury )



## 5 Dokument,  zapisanie nagłówka , zapisanie pozycji , usuwanie pozycji

**Request**

Zapisanie nagłówka

```http
POST {host}/api/erp/document/set-header/platformaerp/{documentid}
```

Zapisanie pozycji

```http
POST {host}/api/erp/document/set-line/platformaerp/{documentid}/{type? dla dokumentów wydania out}
POST {host}/api/erp/document/set-line/platformaerp/{documentid}/out
```

Usuniecie pozycji

```http
POST {host}/api/erp/document/delete-line/platformaerp/{documentid}
```

**Example JS**

```js
//zapisanie pozycji
this.genericPost('/api/erp/document/set-header/platformaerp/{documentid}', this.api.data.document);

//dodanie pozycji
this.genericPost('/api/erp/document/set-line/platformaerp/{documentid}/out', this.api.data.documentline,this.fetchData);

//usuwanie pozycji
this.genericPost('/api/erp/document/delete-line/platformaerp/{documentLineID}', this.api.data.documentline,this.fetchData);
```

## 6 Zatwierdzenie dokumentu , usunięcie dokumentu

**Request**

Zatwierdzenie

```http
POST {host}/api/erp/dictionary/browse/{app_name}/commisionline-for-pw?query=&commisionId=&warehouseid=
```

Usunięcie

```http
POST {host}/api/erp/document/set-status/platformaerp/{documentid}?status=-1
```


## 7. Obsługa dokumentów o typie  RWP  basedocumenttype ='RWP'

### Wybór zlecenia na nagłówku > patrz documentin

### Wybór Sposobu wyboru indeksów

**LOGIKA BIZNESOWA**

Podczas dodawania pozycji zlecnei Wybór spososobu wyboru zlecenia opcje:
- Automatycznie w ramach zlecenia
- Ręczny wybór pozycji 

**REQUEST**

Ręczny wybór pozycji

```http
GET {host}/api/erp/dictionary/browse/{app_name}/commisionline-for-rwp-manual?query=[commisionname]&commisionid
```

Automatyczny w ramach zlecenia

```http
GET {host}/api/erp/dictionary/browse/{app_name}/commisionline-for-rwp-auto?query=[commisionname]
```

```html
Obsolete
Ręczny wybór pozycji 

https://master.platformacrm.pl/get/p/prompt?topmenu=false&dictName=commisionlinefordocumentout&target=line_autoAssignCommisionLineIdByCommisionId-autoassigncommisionlineidbycommisionid,line_commisionLineID-commisionlineid,line_commisionLineID_dict-commissionlinefullnr,line_commisionID-commisionid,line_manualCommisionLineID-manualcommisionlineid&filters=15b4a9b6-eb39-ea11-a98a-060c7c3ef0b7&filters4=1&q=M00001%2F2020%2F1&_=1601282558491

exec [wms].[commisionline_List_dictionary_documentOut] @search=N'',@username=N'test35',@commisionId=N'15b4a9b6-eb39-ea11-a98a-060c7c3ef0b7',@cutBlockedForOutcomes=1,@linesOnly=N'1'

Automatyczny w ramach zlecenia

https://master.platformacrm.pl/get/p/prompt?topmenu=false&dictName=commisionlinefordocumentout&target=line_autoAssignCommisionLineIdByCommisionId-autoassigncommisionlineidbycommisionid,line_commisionLineID-commisionlineid,line_commisionLineID_dict-commissionlinefullnr,line_commisionID-commisionid,line_manualCommisionLineID-manualcommisionlineid&filters=15b4a9b6-eb39-ea11-a98a-060c7c3ef0b7&filters4=0&q=&_=1601282558493

exec [wms].[commisionline_List_dictionary_documentOut] @search=N'',@username=N'test35',@commisionId=N'15b4a9b6-eb39-ea11-a98a-060c7c3ef0b7',@cutBlockedForOutcomes=1,@linesOnly=N'0'

```

