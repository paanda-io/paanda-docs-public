# srs.targets

- Target section is optional.
- When NOT specified all targets are available
- When specified only targets specified in `srs.targets node are available`

## xml node srs.targets.target attributes

- `type` 
- `renderer` (optional template name)
- `label` - optional, label
- `title` - optional, title
- `permission` - optional, limit target to user with permission

~~~ xml
<SRS>
  <!-- .... removed for clarity-->
  <targets>
        <target  type="ptype" label="PDF" renderer="order-confirmation-print"></target>
  </targets>
</SRS>
~~~

## Target `ptype`


- Basic types
  - `get` (default with cache respect) Returns JSON
  - `post` (always up to date ) Returns JSON
  - `object` Returns JSON as array of objects in `data` node , column names = lower case, table names = original case
    -  `command.type=single` , `command.type=header` result in object 
  - `object-ocase`  Returns JSON as array of objects in `data` node , column names = original case, table names = original case
    -  `command.type=single` , `command.type=header` result in object 
   - `object-command`  Returns single command json match renderer, column names = original case, table names = original case
    -  `command.type=single` , `command.type=header` result in object 
  - `xlsx` Excel  returns application/octet-stream
  - `html` Tables printout friendly, only columns with  export=true by default or desktop=true 
  - `html-all-coll` All columns
  - `txt` Raw text 
  - `svg-badge` REturns Image for first row of table name matching renderer name, 
    - `row[0][0]` - required, value
    - `row[0][1]` - optional, title
    - `row[0][2]` - optional, background color
    - `row[0][3]` - optional, foreground color
  - `svg-table` Returns  image with table
- Preprocessed
  - `deprecated` `md` markdown renderer of `app\[renderer].html` template
  - `deprecated` `pdf` Renders pdf file ,returns application/pdf, renderer of `app\[renderer].html` template
  - `deprecated` `pdfmd` Renders pdf file ,returns application/pdf, renderer of `app\[renderer].html` template
  - `deprecated` `htmltemplate`   Renders html file, renderer of `app\[renderer].html` template



