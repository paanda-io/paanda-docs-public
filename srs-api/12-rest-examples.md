# REST SRS Examples

## General Scheme

- `app_name` application context **REQUIRED**
- `srs_name` SRS definition name **REQUIRED**
- `renderer` renderer **OPTIONAL**
- `querystring` **OPTIONAL** param1=value&param2=value2

If **renderer**  contains ANY string SRS is executed against data sources


```http
GET {host}/api/srs/{app_name}/{srs_name}/{renderer}?{querystring}&ptype={type ex:xlsx,html,svg}
```

```http
POST {host}/api/srs/{app_name}/{srs_name}/{renderer}?{querystring}
```

***GET BADGE***

```http
GET {{host}}/api/srs/{app_name}/view?ptype=svg
```



## Example definition with parameters

> Example  require Chinook Database see more at https://github.com/lerocha/chinook-database 

``` xml
 <SRS>
 <title>
 Hello paanda
 </title>

 <parameters>
  <param name="BillingAddress" ></param>
  <param name="InvoiceDate_from" type="date"></param>
  <param name="InvoiceDate_to" type="date"></param>
 </parameters>

<commands>
<command>
<![CDATA[

SELECT top 3
   [InvoiceDate]
   ,[BillingAddress]
   ,[BillingCity]
   ,[BillingState]
   ,[BillingCountry]
   ,[BillingPostalCode]
   ,[Total]
FROM  [dbo].[Invoice]
where  
   (@BillingAddress is null or BillingAddress like @BillingAddress)
   and (@InvoiceDate_from is null or InvoiceDate >= @InvoiceDate_from)
   and (@InvoiceDate_to is null or InvoiceDate <= @InvoiceDate_to)
]]>
</command>
</commands>
  
</SRS>
```

## Run Definition

Nothing happens here just return definition without executing any command

```http
GET {{host}}/api/srs/examples/hello-parameters HTTP/1.1
Authorization: Bearer {{token}}
```

## Execute JSon

Any renderer will execute command  

```http
GET {{host}}/api/srs/examples/hello-parameters/1 HTTP/1.1
Authorization: Bearer {{token}}
```

## Execute EXCEL

```http3
GET {{host}}/api/srs/examples/hello-parameters/1?ptype=xlsx HTTP/1.1

Authorization: Bearer {{token}}
```

## Example API request

```htttp
GET {host}/api/srs/{app_name}/{srs_name}/{srs renderer]}?[parameters]&ptype=[target type]&ptoken=[bearertoken]
```

```htttp
POST {host}/api/srs/{app_name}/{srs_name}/{srs renderer]}?[parameters]&ptype=[target type]&ptoken=[bearertoken]
```
