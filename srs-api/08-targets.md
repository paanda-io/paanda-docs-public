# SRS/targets

Target section is optional.

## Attributes

- `type` 
- `renderer` (optional template name)
- `label` - optional label
- `title` - optional title

## Target `type`



- Basic types
  - `get` (default with cache respect) Returns JSON
  - `post` (always up to date ) Returns JSON
  - `object` Returns JSON as array of objects in `data` node , column names = lower case, table names = original case
    -  `command.type=single` will convert to object not array 
    -  `command.type=header` will convert to object not array 
  - `object-ocase`  Returns JSON as array of objects in `data` node , column names = original case, table names = original case
    -  `command.type=single` will convert to object not array 
    -  `command.type=header` will convert to object not array 
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
  - `md` markdown renderer of `app\[renderer].html` template
  - `pdf` Renders pdf file ,returns application/pdf, renderer of `app\[renderer].html` template
  - `pdfmd` Renders pdf file ,returns application/pdf, renderer of `app\[renderer].html` template
  - `htmltemplate`   Renders html file, renderer of `app\[renderer].html` template


## Example

~~~ xml
<SRS>
  <!-- .... removed for clarity-->
  <targets>
        <target  type="pdf" label="PDF" renderer="order-confirmation-print"></target>
        <target  type="pdfmd" label="PDF" renderer="order-confirmation-print"></target>
        <target  type="xlsx" label="xlsx"></target>
        <target  type="html" label="html" renderer="order-confirmation-print"></target>
        <target  type="htmlmd" label="html" renderer="order-confirmation-print"></target>
        <target  type="txt" label="txt" renderer="order-confirmation-print"></target>
        <target  type="post"></target>
        <target  type="get"></target>
  </targets>
</SRS>
~~~

