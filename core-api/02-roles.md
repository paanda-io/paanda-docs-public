# Roles



### Administrative roles

- app_administrator 
  - create/update/delete  apps 
  - create/delete connections
- sys_administrator - User managment
- srs_administrator - 
- sys_invite - invite new user with given roles except sys_administrator,app_administrator   role
- sys_comments - communication data


### Application roles

For each  installed apps by default there are

- app_[appname] - Execute SRS
- app_[appname]_storage_read - read
- app_[appname]_storage_write 
- app_[appname]_query  - run query against connections 

