# Permissions

Permissions can be assigned on multiple levels

If permission is not specified default require `srs_browse`
To allow anonymous access permission must be set to Anonymous

## Anonymous access

Warning permission `anonymous` will grant access everyone

```xml
<SRS>
    <name>Potwierdzenie zamówienia</name>
    <permission>anonymous</permission>
...
```

## Connection permission 

```xml
<SRS>
    <commands>
        <command permission="MyRequiredPermission" >select 'Visible only for  user with permission MyRequiredPermission' </command>
        <command >select 'Visible for everyone'</command>
    </commands>
</SRS>
```

## Command permission

``` xml
<SRS>
    <commands>
        <command permission="MyRequiredPermission" >select 'Visible only for  user with permission MyRequiredPermission' </command>
        <command >select 'Visible for everyone'</command>
    </commands>
</SRS>
```

## Column permission

``` xml
<SRS>
    <commands>
        <command >select '' Product , 12 Price   </command>
    </commands>

    <columns>
        <column name="Price" permission="vendors"/>
    </columns>
</SRS>
```
