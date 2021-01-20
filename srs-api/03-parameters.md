# SRS/parameters

Parameters section is optional.

## Attributes

- `name` (required) - parameter name
- `label` - parameter label
- `description` - short description
- `command` - optional command - parameter will be applied only to matching command (comma separated values)
- `required` - optional true/false
- `step` - useful for input type range
- `srccommand` - when type="server-xml"  or type="server-xml"
- `type` - optional, default **text** 
  - `server` - server side parameter useful for predefined values cannot be overwritten.
     Useful when want pass table as parameter  cannot be overwritten
  - `server-xml`  
  - `integer` - integer
  - `hidden` - hidden (useful for client side dictionaries, helpers)
  - `select` - dropdown type, see section
  - `autocomplete`  (must contains key value)
  - all input types defined by HTML 5 spec. https://www.w3schools.com/tags/att_input_type.asp for example
  text, number, password, hidden, color, date, checkbox ...



### Parameters

Processing order 

1. Server side parameters ( cannot be override)
2. Query String
3. Supplied Parameters

- SQL injections Using parameters is safe  and recommended.
To better understand what is SQL injection and why we do not allow processing commands read
https://owasp.org/www-community/attacks/SQL_Injection

``` xml
 <param name="username" type="server">[[kv.v.user.username]]</param>
```

## Server Side Variables

There are few predefined variables available.

Built in variables marked in double brackets  `[[kv.v.variable1]]`

- `[[kv.v.owner.name]]` Owner Name, also in footer
- `[[kv.v.owner.contact]]` Owner contact, also in footer
- `[[kv.v.owner.footer]]` Footer additional text
- `[[kv.v.owner.language]]` Default language
- `[[kv.v.user.username]]` - username
- `[[kv.v.user.userid]]` user id
- `[[kv.v.user.roles]]` Roles in brackets [role1] [role2] [role3]



### Examples `type="select"` 

```xml
<SRS>
  <title>Select Example</title>

  <parameters>
    <param name="leadUserID" type="select"></param>
  </parameters>


  <commands>
    <command name="view" label="Firmy"  >
      <![CDATA[
	SELECT  
		f.firmNR, 
		vat_status,
		f.taxcode,
		f.firmname name, 
		f.firmNameShort, 
		f.firmTypeID, 
		f.leadUserID, 
	
		f.www, 
		f.groupID, 
		UPPER(f.countryCode) countryCode, 	
 		f.city, 
 		 f.streetName + ' ' + isnull(f.houseNumber,'') + ' ' + isnull(f.flatNumber,'')  streetName,
		f.postCode,

		f.countryState,
		f.phoneNumber, 
		f.email, 
		f.account, 
		f.accountInsurance,
		f.classifications, 
		f.discountCategoryID, 
		f.discountValue,
		f.modDate, 
		f.modUsername,
		f.firmid,latitude,longitude	,
		vat_date
	FROM firm.firm f left join vat on f.taxcode =vat.vat_nip
	WHERE status >-1
		and (@firmTypeID IS NULL OR f.firmTypeID = @firmTypeID)
		AND (@leadUserID  IS NULL OR f.leaduserid = @leadUserID)
		and (@COUNTRYCODE IS NULL OR f.countrycode = @COUNTRYCODE)
		and (@firmname IS NULL OR f.firmname like @firmname)
		AND (@discountCategoryID IS NULL OR f.discountCategoryID = @discountCategoryID)
		AND (@city IS NULL OR f.city  like @city)
	ORDER BY moddate desc 
	  
	]]>
    </command>
    <command name="leadUserID" type="hidden"> 
     	select userID,username from [user].[user]
    </command>

  </commands>
</SRS>
```


### Examples type="server-xml"

Definition
```xml
  <param name="account" type="server-xml" srccommand="teams"></param>
```

Result XML

``` xml
<data>
  <table name="view7" label="Available accounts">
    	<rows>
    		<i>
			<teamuser_id>53</teamuser_id>
			<user_id>3a604586-e518-4261-b7d9-658722a978a7</user_id>
			<team_id>058fe275-6545-4f3b-854f-cb7093b2bc59</team_id>
			<teamuser_created_at>2019-02-20T01:04:00</teamuser_created_at>
			<teamuser_created_by>marcin@kotynia.com</teamuser_created_by>
		</i>
		<i>
			<teamuser_id>55</teamuser_id>
			<user_id>3a604586-e518-4261-b7d9-658722a978a7</user_id>
			<team_id>e34f9da5-8820-4248-9b8c-a4038eafa2ee</team_id>
			<teamuser_created_at>2019-02-20T01:04:00</teamuser_created_at>
			<teamuser_created_by>marcin@kotynia.com</teamuser_created_by>
		</i>
	</rows>
  </table>
</data>
```

Result XML SQL Server Reading

``` sql
SELECT
    x.Rec.query('./team_id').value('.', 'uniqueidentifier') AS 'team_id'
FROM @account.nodes('data/table/rows/i') as x(Rec)
```





### Build dictionary


  if parameter match command name 
  - server side  variable example
    ```xml
    <param name="username" type="server" >[[kv.v.user.username]]</param>
    ```
 - DEFAULT example data from table and column
  if parameter.name match command name and default match 
    ```xml
    <param name="command.name" type="number" default="column.name"></param>
    ```



### Dynamic default value

```xml
<SRS>  
<parameters>
	<param name="BillingAddress"></param>
	<param name="BillingCountry"></param>
     <param name="date_from" type="date"  srccommand="parameters"></param>
    <param name="date_to" type="date" srccommand="parameters"></param>
    
</parameters>

<commands>
	<!-- Important command.name must be parameters -->
	<command name="parameters" type="server" >
	select 
	convert(varchar,DATEADD(month, DATEDIFF(month, 180, getdate()), 0), 23)  date_from,
	convert(varchar,EOMONTH(getdate()) , 23)  date_to
   </command>

      
	<command>
  		SELECT 
		,[InvoiceDate]
			  ,[BillingAddress]
			  ,[BillingCity]
			  ,[BillingState]
			  ,[BillingCountry]
			  ,[BillingPostalCode]
			  ,[Total]
		FROM  [dbo].[Invoice]
		where  
			(@BillingAddress is null or BillingAddress like @BillingAddress)
			and (@BillingCountry is null or BillingCountry = @BillingCountry)
	</command>
  </commands>
  
</SRS>


```






### Basic example

``` xml
<SRS>  
<parameters>
	<param name="BillingAddress"></param>
	<param name="BillingCountry"></param>
</parameters>

  <commands>
	<command connection="Chinook">
  		SELECT 
		,[InvoiceDate]
			  ,[BillingAddress]
			  ,[BillingCity]
			  ,[BillingState]
			  ,[BillingCountry]
			  ,[BillingPostalCode]
			  ,[Total]
		FROM  [dbo].[Invoice]
		where  
			(@BillingAddress is null or BillingAddress like @BillingAddress)
			and (@BillingCountry is null or BillingCountry = @BillingCountry)
	</command>
  </commands>
  
</SRS>
```


