# SRS/connections

Connection node is optional, by default SRS inherit connection from APP


Connection in SRS are stored in plain text.
For security reasons It's recommended to use Paanda Connections Manager.
Connections stored in connection manager are secured and are not stored in plain text.

## Attributes

- `name` Name of the connection
- `type` ( DEFAULT `mssql` ) connection type

## Connection types

### Connection Types 

- `mssql` Microsoft SQL Server, Azure SQL DB, Amazon RDS
- `self` Virtual connection to command result
- `file_system` Local/Remote File System  (DATA CENTER AND	SERVER VERSIONS ONLY)
- `excel` EXCEL ( `.xlsx` ) files as a database   (DATA CENTER AND	SERVER VERSIONS ONLY)
- `postgresql` PostgreSQL    (DATA CENTER AND	SERVER VERSIONS ONLY)
- `oracle` Oracle   (DATA CENTER AND	SERVER VERSIONS ONLY)

## Providers documentation

### `mssql` provider

Standard SQL Server provider connect to Microsoft® SQL Server | Microsoft® Azure SQL | Amazon RDS for SQL server.

### `file_system` provider (alpha)

System can query file system like SQL database.

Parameters:

- Path (required)
- Server (optional) remote server
- User(optional)  remote server user
- Password (optional)  remote server password
- SearchPattern=*.* (optional, default = *.*) 
- SubDirectories=true (optional, default = false)

``` xml
<connections>
    <!--Abolute path-->
    <connection name="dropbox" type="files">Server=myServer;Path="c:\git\platforma-docs" SearchPattern=*.*; SubDirectories=true</connection>
    <!--Sample with relative path to data folder-->
    <connection name="dropbox" type="FileSystem">Server=myServer;Path="\test1";SearchPattern=*.*; SubDirectories=true</connection>
</conenctions>

```

Available fields

- `CreationTime` text,
- `CreationTimeUtc` text,
- `DirectoryName` text,
- `Name` text,
- `Length` Numeric,
- `FullName` text,
- `Extension` text,
- `Content` text,  `(read only ".html" ,".md", ".txt", ".sql", ".xml", ".json")`
- `Slug` text

### `excel` provider

Parameters:

- Path (required)
- Server (optional) remote server
- User(optional)  remote server
- Password (optional)  remote server
- hasHeader (optional)  true/false

``` xml
<connections>
    <connection name="dropbox" type="excel">Path="\test.xlsx";</connection>
    <connection name="dropbox" type="excel">Server="test";Path="\test.xlsx";</connection>
</connections>
```
