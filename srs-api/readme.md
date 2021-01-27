# SRS

## Introduction

SRS is an core Paanda module  which extract transform and load data from various data sources.

- SRS definition is a xml file, stored in local filesystem or git repository,  format comes with sensible defaults to get up and running quickly and once you move towards a more advanced setup can be done.
- SRS can be executed using REST API or  Paanda UI,   and produce output for example JSON/HTML/PDF/Excel 
- SRS are grouped in applications
- SRS can inherit canfiguration from `global.xml` file


## Data

- `srs.permission` - command available for any role specified, roles separated by `,` 
  - `permission` - if equals `anonymous` available for not authenticated user
  


## "Hello world" example
 
 
``` xml
<srs>
    <title>Hello World</title>
    <description>Markdown Support</description>
    <permission>VIP</permission>
    <cache><!--cache in seconds--></cache>
    <commands>
   <command name="hello">
      <![CDATA[
      select 'Hello World'
      ]]>
   </command>
  </commands>  
    <!--<connections></connections>-->
    <!--<parameters>
        <param name="columnname" type="text" description="desc" />
    </parameters>-->
    <columns><!--see SRS/columns documentation on sidebar--></columns>
    <options><!--see SRS/options documentation on sidebar--></options>
    <targets><!--see SRS/targets documentation on sidebar--></targets>
</srs>

```

