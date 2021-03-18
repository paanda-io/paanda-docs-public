# SRS/options

Options section is optional  

## Attributes

- `name`, required
- `command`, required
- `title`, optional title for name
- `url`, optional URL http://pandaa.io/item/{anycolumnname}/{anycolumnname}
- `label`, optional
- `permission`, optional column level permission
- `css`, optional CSS class
- `type`, optional 
  - `pa_post_single` - execute POST
  - `pa_post` - execute POST, for each row 
  - `pa_blink` - external link to new window
  - `pa_elink` - external link to same window
  - `pa_download` - external link download
  - `default` - internal link

## Example

``` xml
<options>
	<option label="Pokaż wszystkie zamówienia" css="w3-green"  command="orders"  url="/srs/[[app_name]]/301-zamowienia-lista/view?firmid={firmid}&amp;date_to=&amp;date_from=" />
	<option  css="w3-red" label="Remove Selected" command="documenttypes"  type="pa_post" url="/api/config/delete" />
	<option label="Create account" css="w3-green"   type="pa_elink" url="/crm/account" />
	<option label="Create account" css="w3-green"   type="pa_post" url="action:select" />
	<option label="Create account" css="w3-green"   type="pa_post" url="action:unselect" />
</options>
```


### type="pa_post"

Type pa_post require `#clipboard` in description 


```
<srs>
<commands>
	<command>
	     <![CDATA[
	update table set x= @column where y=@column
	   ]]>
	</command>
</commands>
</srs>


## Display resources add

``` xml
<options>
   	<option css="w3-blue" label="Report time, resources" type="v_timesheet" />
</options>
```
