# SRS/commands

Command is a standard SQL query specific to connection type.
For Example on `mssql` Connection you can run all Microsoft SQL Server specific code

## Attributes


- `name` - **optional**name of dataset default value 1,2,3,4,5
- `connection` - **optional** connection name by default use default APP connection
  - `connection="self"`  is a special kind of provider you can query different commands (from diferent connection) like databases
- `label` - **optional** display label
- `title` - **optional** title on hover
- `type` - **optional**
  - empty  **(default)**  - render as a table at client
  - server - server side only used to compute properties, not returned
  - hidden - hidden returned
  - header - render  as header at client - only not empty values are rendered
  - single - render as vertical  list at client - only not empty values are rendered
  - form - render table as form as client

## Hello World example

> Examples require chinook-database schema available https://github.com/lerocha/chinook-database

> First column should be unique

~~~ xml
<SRS>
 <commands>
  <command name="test" >
   select 'Hello World'
  </command>
  <command name="test1" >
   <![CDATA[
   /*If you are using XML reserved characters: > < command should be in CDATA block*/
   select 'Hello <-_->'
   ]]>
  </command>
 </commands>
</SRS>
~~~

## Known Issues

Using `connection="self"` in some cases can badly understand numeric types to fix that you need to override column type for example:

``` xml
<column name="commisionstartdate" type="tdecimal"  />
```
