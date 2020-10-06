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
  - `pa_post_single` - post each row as a model
  - `pa_post` - post each row as a mode
  - `pa_blink` - external link to new window
  - `pa_elink` - external link to same window
  - `pa_download` - external link download
  - `default` - internal link

## Example

``` xml
<options>
	<option  css="w3-red" label="Remove Selected" command="documenttypes"  type="pa_post" url="/api/config/delete" />
	<option label="Create account" cssclass="w3-green"   type="pa_elink" url="/#/crm/account" />
	<option label="Create account" cssclass="w3-green"   type="pa_post" url="action:select" />
	<option label="Create account" cssclass="w3-green"   type="pa_post" url="action:unselect" />
</options>
```


### type="pa_post"

Type pa_post require set column in dataset , you can add set column 

``` sql
SELECT cast(0 as bit) 'set' , getdate()
```

Samples

You can find predefined options for v_srs.js section   v-for="option in api.options"

## Display resources add

``` xml
<options>
   	<option css="w3-blue" label="Report time, resources" type="v_timesheet" />
</options>
```
