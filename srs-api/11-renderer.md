# Renderer

Renderer allow render data with template

## Example target

- HTML
- HTMLMD - html with markdown extension
- PDF
- PDFMD - pdf with markdown extension

For a full list see targets  [08-targets.md](08-targets.md) 

Sample target

``` xml
...
  <targets>
    <target  type="pdf" label="PDF" renderer="order-confirmation-print"></target>
  </targets>
...
```

## Snippets

### Get value

``` js
{{ get('table name','column name') }}
```

### Get table by name

``` js
{{ getTable('issuer') }}
```

### Get table columns

``` js
{{ getTable('header').columns }}
```

### Get table rows

``` js
{{ getTable('issuer') }}
```

### Get column index

``` js
{{ getColIndex('lines','pos') }}
```

## Example 1

``` html
<div style="font-size:0.7em">
	<!--################## HEADAR ######################-->
<table style="width:100%; margin-top:30px">

    <tr>
        <td style="width:50%;text-align:center;vertical-align:top">
            <div style="margin-bottom:20px;margin-top:20px;"><img src="/client/images/logo.png" width="200"/> </div>

			 <template v-for="col in getTable('issuer').columns">
                  <div>{{ getTable('issuer').rows[0][col.ordinal]}}</div>
             </template>
			
        </td>
        <td style="width:50%; vertical-align:top">
            <div style="font-size:2.5em"><b>ORDER CONFIRMATION</b></div>
            <div>POTWIERDZENIE ZAMÓWIENIA</div>

            <table style="margin-top:50px;">
                <template v-for="col in getTable('header').columns">
                    <tr v-if="getTable('header').rows[0][col.ordinal]">
                        <td style="white-space:nowrap">{{col.name}}</td>
                        <td><b>{{ getTable('header').rows[0][col.ordinal]}}</b></td>
                    </tr>
                </template>
            </table>

        </td>
    </tr>
</table>


<div style="height:50px">&nbsp;</div>

<!--################## BODY ######################-->
<table class="w3-table w3-bordered">
    <thead>
        <tr>
            <th>#</th>
            <th>Part No. / Description</th>
            <th>Dispatch</th>
            <th style="text-align:right; white-space:nowrap;">Catalog Price<br/>Discount(%)</th>
            <th style="text-align:right;">Price</th>
            <th style="text-align:right;">Qty</th>
            <th style="text-align:right;">Total</th>
        <tr>
    </thead>

    <tbody>
        <tr v-for="row in getTable('lines').rows">
            <td>{{row[getColIndex('lines','pos') ]}}</td>
            <td>
                <div><b>{{row[getColIndex('lines','partno')]}}</b> {{row[getColIndex('lines','sn')]}}
			{{row[getColIndex('lines','name')]}}</div><div>{{row[getColIndex('lines','namepl')]}}</div>
            </td>
            <td>{{row[getColIndex('lines','dispatch')] | formatDate}}</td>

            <td>
                <div style="text-align:right;">{{row[getColIndex('lines','initialnetprice')] | formatPrice}}</div>
                <div style="text-align:right;">{{row[getColIndex('lines','discount') ]}}%</div>
            </td>
            <td style="text-align:right;"><b>{{row[getColIndex('lines','price')] | formatPrice}}</b></td>
            <td style="text-align:right;">{{row[getColIndex('lines','qty')]}}</td>
            <td style="text-align:right;">{{row[getColIndex('lines','netsum')] | formatPrice}}</td>
        </tr>
    </tbody>
</table>


<div style="text-align:right; font-size:1.5em;margin-top:20px;" >
    TOTAL NET VALUE {{totals('lines','netsum') | formatPrice}}  {{get('header','Currency')}} 
</div>


<div v-if="getTable('footer').rows.length>0" style="width:100%; margin-top:50px;">


            <table >
		    <tr><td colspan="2"><b>SHIPPING ADDRESS</b></td></tr>
           		<template v-for="col in getTable('footer').columns">
                 <tr v-if="getTable('footer').rows[0][col.ordinal]">
                        <td style="white-space:nowrap">{{col.name}}</td>
                        <td><b>{{ getTable('footer').rows[0][col.ordinal]}}</b></td>
                    </tr>
                </template>
            </table>
	
</div>

<!--################## LINES######################-->

</div>

```

## Example 2

``` xml
<SRS>
  <name>Potwierdzenie zamówienia</name>
	<permission>erp_orders_print</permission>
  <parameters>
    <param name="orderid" type="text" label="ORDER ID" ></param>
  </parameters>

 
  <commands>
    <command name="issuer" >
    	select 
       		firmName,
       		replace(countryCode,'pl','Poland'),
        	postCode +' ' + city,
     		streetName,
	 	houseNumber,
       		www,
       (
	select value from configuration.configuration where configurationID='instance.sales.emailservice')
	from firm.firm 
	where firmID = (select value from configuration.configuration where configurationID='instance.sales.seller'
	    )
    </command>
    
    <command name="header" >
      <![CDATA[
      
	select 
  		o.orderFullNR 'Order No',
 		convert(varchar(10),o.orderDate,120)  Date,
		convert(varchar(10),  o.orderexpecteddate,120)   Dispatch,
  		f.firmnr ' Customer',
 		f.firmname ' Customer Name',
   		f.postCode + ' ' + f.city 'Customer City' ,
   		f.streetName 'Customer Street' ,
  		f.taxcode 'Customer Tax',
  		o.addUsername Contact,
  		upper(o.currencyID) Currency,
		o.orderfullnr2 'Your ref.', 
    		o.orderMemo Notes --,o.*,
	from document.[order] o 
		inner join firm.firm f on o.firmid =f.firmid  
		inner join common.dictionary payment on o.paymentTypeID = payment.dictionaryKeyGuid
		inner join common.dictionary delivery on o.deliveryWayID = delivery.dictionaryKeyGuid
	where o.orderid = @orderid
	]]>
    </command>

    
        <command name="footer" >
      <![CDATA[
      
	select 
  		f.firmnr 'Customer',
  		f.firmname 'Name',
   		f.postCode + ' ' + f.city 'City' ,
   		f.streetName 'Street' ,
   		upper(d.dictionaryvalue) 'Country'
	from document.[order] o 
		inner join firm.firm f on o.[deliveryFirmID] =f.firmid  
		left join   common.dictionary d on d.dictionaryname ='countrycode' and d.dictionarykey= f.countryCode
	where o.orderid = @orderid
	]]>
    </command>
    
    <command name="lines" >
      <![CDATA[
      

	select  
		orderordinalNumber pos,
		i.itemcode partno,
		ol.itemSerialNumber sn,
		'[PL] ' + ol.itemOrderName namepl,
		'[EN] ' + isnull(ol.itemordernameforeign,i.[itemNameCommercialForeign]) name,
		ol.deliveryConfirmationDate dispatch,
		cd.dictionaryValue unit,
		ol.initialnetprice,
		ol.discountRate discount,	
		ol.itemPrice price,
		ol.itemQuantity qty,	
		ol.itemValue netsum
 	from document.orderline ol
		inner join wms.item i on ol.itemid =  i.itemID
		inner join common.dictionary cd on ol.itemUnitOrderID = cd.dictionaryKeyGuid
	where ol.orderid =  @orderid
	order by orderordinalNumber 
	]]>
    </command>
  </commands>

  <targets>
    <target  type="pdf" label="PDF" renderer="order-confirmation-print"></target>
    <target  type="html" label="html"  renderer="order-confirmation-print"></target>
    <target  type="pdfsource"   renderer="order-confirmation-print"></target>
  </targets>

  
</SRS>
```

## Example  order-confirmation-print.html


``` html
<div style="font-size:0.7em">
	<!--##################NAGLOWEK######################-->
<table style="width:100%; margin-top:30px">

    <tr>
        <td style="width:50%;text-align:center;vertical-align:top">
            <div style="margin-bottom:20px;margin-top:20px;"><img src="/images/logo.png" width="200"/> </div>

			 <template v-for="col in getTable('issuer').columns">
                  <div>{{ getTable('issuer').rows[0][col.ordinal]}}</div>
             </template>
			
        </td>
        <td style="width:50%; vertical-align:top">
            <div style="font-size:2.5em"><b>ORDER CONFIRMATION</b></div>
            <div>POTWIERDZENIE ZAMÓWIENIA</div>

            <table style="margin-top:50px;">
                <template v-for="col in getTable('header').columns">
                    <tr v-if="getTable('header').rows[0][col.ordinal]">
                        <td style="white-space:nowrap">{{col.name}}</td>
                        <td><b>{{ getTable('header').rows[0][col.ordinal]}}</b></td>
                    </tr>
                </template>
            </table>

        </td>
    </tr>
</table>
<!--##################NAGLOWEK######################-->

<!--##################NAGLOWEK2######################-->


<div style="height:50px">&nbsp;</div>

<!--################## LINES######################-->
<table class="w3-table w3-bordered">
    <thead>
        <tr>
            <th>#</th>
            <th>Part No. / Description</th>
            <th>Dispatch</th>
            <th style="text-align:right; white-space:nowrap;">Catalog Price<br/>Discount(%)</th>
            <th style="text-align:right;">Price</th>
            <th style="text-align:right;">Qty</th>
            <th style="text-align:right;">Total</th>
        <tr>
    </thead>

    <tbody>
        <tr v-for="row in getTable('lines').rows">
            <td>{{row[getColIndex('lines','pos') ]}}</td>
            <td>
                <div><b>{{row[getColIndex('lines','partno')]}}</b> {{row[getColIndex('lines','sn')]}}
			{{row[getColIndex('lines','name')]}}</div><div>{{row[getColIndex('lines','namepl')]}}</div>
            </td>
            <td>{{row[getColIndex('lines','dispatch')] | formatDate}}</td>

            <td>
                <div style="text-align:right;">{{row[getColIndex('lines','initialnetprice')] | formatPrice}}</div>
                <div style="text-align:right;">{{row[getColIndex('lines','discount') ]}}%</div>
            </td>
            <td style="text-align:right;"><b>{{row[getColIndex('lines','price')] | formatPrice}}</b></td>
            <td style="text-align:right;">{{row[getColIndex('lines','qty')]}}</td>
            <td style="text-align:right;">{{row[getColIndex('lines','netsum')] | formatPrice}}</td>
        </tr>
    </tbody>
</table>


<div style="text-align:right; font-size:1.5em;margin-top:20px;" >
    TOTAL NET VALUE {{totals('lines','netsum') | formatPrice}}  {{get('header','Currency')}} 
</div>


<div v-if="getTable('footer').rows.length>0" style="width:100%; margin-top:50px;">


            <table >
		    <tr><td colspan="2"><b>SHIPPING ADDRESS</b></td></tr>
           		<template v-for="col in getTable('footer').columns">
                 <tr v-if="getTable('footer').rows[0][col.ordinal]">
                        <td style="white-space:nowrap">{{col.name}}</td>
                        <td><b>{{ getTable('footer').rows[0][col.ordinal]}}</b></td>
                    </tr>
                </template>
            </table>
	
</div>

<!--################## LINES######################-->

</div>

```
