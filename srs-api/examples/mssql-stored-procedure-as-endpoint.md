# Sql Server Stored procedure as endpoint

## Example 1 - auto parameters mode

All parameters that will match stored procedure parameters name will be sent

```xml
<SRS>
<title>API task POST</title>
<commands> 
   <command name="api">
		[dbo].[task_set]
   </command>
</commands>

</SRS>
```

## Example 2  - with defined parameters

If any parameter in parameters node then

- only parameters defined in parameters node are sent
- you can pass server side values see srs/parameters ***<param name="task_modified_by" type="server">[[kv.v.user.username]]</param>***

```xml

 <SRS>
  <title>API task POST</title>
   <parameters>
     <param name="team_id"></param>
     <param name="type_id"></param>
     <param name="task_name"></param>
     <param name="task_description"></param>
     <param name="task_internal_notes"></param>
     <param name="task_reporter"></param>
     <param name="task_resolved_at"></param>
     <param name="task_tags"></param>
     <param name="task_modified_by" type="server">[[kv.v.user.username]]</param>
     <param name="task_modified_at"></param>
     <param name="task_id"></param>
     <param name="task_uuid"></param>
     <param name="task_estimate"></param>
     <param name="task_remote_id"></param>
     <param name="task_remote_source"></param>
     <param name="task_assignee"></param>
     <param name="task_image"></param>
   </parameters>
   <commands>
 
   <command name="api">
		[dbo].[task_set]
   </command>

</commands>

</SRS>
```
