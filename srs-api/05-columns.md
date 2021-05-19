# SRS/columns

Optional XML element with column additional formatting

## Example

``` xml
<SRS>
<!-- ... removed for clarity -->
<columns>
	<column name="product" type="tlink" width="300" mobile="true" url="/mportal/417-portal-product/tasks?id={productID}"/>
	<column name="imsprofil_social" hidden="false" label="Instagram" type="turl_blank" url="https://www.instagram.com/{imsprofil_social}" />
</columns>
</SRS>
```

## Attributes

> Important notice ampersand (&) must be replace with &amp; in attributes

- `desktop` > `mobile` > `export` [true/false], show/hide column on desktop / mobile / export (excel)
- `title`, optional title for name
- `url`, optional URL http://pandaa.io/item/{anycolumnname}/{anycolumnname} , 
  - supported variebles `[[app_name]]` `[[kv.v.*]]`
- `label`, optional
- `name`, required
- `required`, optional true/false 
- `type` , additional formatting
- `permission`, optional column level permission
- `css`  - custom style for element, Example `background-color:red`

## Column `type`

### Default

List of autodiscover types from database schema

- `tguid` 
- `tdate` - Date / column.css - style attribute 
- `tbool` - Bool / column.css - style attribute 
- `tinteger`  example 2 (Number)  / column.css - style attribute 
- `tdecimal` , example 2.02  (Decimal)  / column.css - style attribute 
- `tstring`
  - column.css - style attribute 

### Custom

List of custom types from database schema

- `tinput_number` - input number
  - column.css - style attribute 
- `tinput_text`  - text number
  - column.css - style attribute 
- `tinput_bool`  - checkbox number 
  - column.css - style attribute 
- `tlink` -  link
  - column.css - style attribute 
  - column.url - url 
- `tlink_tag`  - build tag link with color based on text
- `tlink_icon`  - internal paanda client link with icon font awesome 4 icon
  - column.url - url 
  - column.css - font awesome 4 class  https://fontawesome.com/v4.7.0/icons/ example `fa fa-bar-chart`
- `tlink_download` - dedicated for files download
- `tcomputed` , example : {column1} * {column2} /2 ,  getComputed(column.url,row,table.columns)
- `turl_blank` - external link in new window
- `turl_post` - send standard javascript object to url
  - column.url - url 
  - column.css - style attribute 
- `tcolor_progress`
- `turl_progress`
- `tformat_bytes` - Human readable size input bytes
- `tformat_k` - Human readable size for large numbers, REturn 10K, 20M
- `ttag` - build tag list with color based on text
- `tmarkdown`, renders markdown server side
- `tjson`, renders xml to json server side
- `tstring_multi` -- multiline Text with Line breaks similar to HTML `pre` tag
- `timg` - image token from repository `example: ea4cc594-fd85-ea11-80e1-9c8e994dc647.jpg`  / column.css - style attribute 
  - column.url - url 

	
####  Examples:  `timg` 

get file from files 
```xml
<column name="logo" type="timg" url="/api/files/26EFEED6-CDEF-E911-80DA-9C8E994DC647.png?w=150" />
```

examples get img logo 
```xml
<column name="logo" type="timg" url="/client/images/logo.png?w=150" />
```

examples get qrcode
```xml
<column name="qr" type="timg" label="Order code" css="width:100px" url="/api/system/qrcode?code={qr}" />
```

examples get BAR code
Supported type =  Code128 , ean13, Code93
```xml
<column name="qr" type="timg" label="Order code" css="width:100px" url="/api/system/barcode?code={qr}&type=code128" />
```

get avatar

```xml
<column name="mail_to_avatar"  label="To" type="timg" mobile="false"	url="/account/avatar/{mail_to_avatar}"  />
```
  
### Examples:  `turl_blank`  - external linking

```xml
<!--Redirect to external page-->
<column name="COMMISIONNAME" title="test" label="test"  type="turl_blank" url="http://test.com/test?commisionID={commisionID}" />
```

### Examples:  `tstring_multi`  - external linking

SQL Server Example:

``` sql
SELECT 'Hello' + CHAR(13) + CHAR(10) + 'World'
```

### Examples `tstring_multi`

Text with Line breaks similar to HTML `pre` tag

SQL Server Example:

``` sql
SELECT 'Hello' + CHAR(13) + CHAR(10) + 'World'
```


## Appendix , special column names

You can set color for text and background using special column names

Example colors:

- https://htmlcolorcodes.com/color-chart/material-design-color-chart/

System colors:

- blue #0074D9
- red #FF4136
- green #2ECC40
- grey #9e9e9e
- dark grey #616161


###  `pa_background`  Hexadecimal color for background

### `pa_color`  Hexadecimal color for text









