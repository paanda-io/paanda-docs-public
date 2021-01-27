# FAQ

## connection = "self" and MS SQL SERVER Guid

Youn need to cast GUID to varchar if you want to query command see example

```
<SRS>
<commands>
  <command name="example">

  select 
    cast('1D504B35-2CC5-4079-B954-871D2B8BB56F' as uniqueidentifier) uniqueidentifier_test1,
    cast('6D504B35-2CC5-4079-B954-871D2B8BB56F' as varchar(36)) uniqueidentifier_test2

  </command>

  <command name="test1" connection="self">
  --FAIL RETURN 0 ROWS
  select * from example 
  where  uniqueidentifier_test1 = '1D504B35-2CC5-4079-B954-871D2B8BB56F' 
  </command>

  <command  name="test2" connection="self">
  --OK  RETURN 1 ROW
  select * from example 
  where  uniqueidentifier_test1 = '6D504B35-2CC5-4079-B954-871D2B8BB56F' 
  </command>

</commands>
</SRS>
```

### Incorrect sum
#### Example 1: FAIL
```
<SRS>
  <commands>
    <command name="numbers" >
     select 1.1 num
     union
     select 2.1 num
     union 
     select 3.1 num
    </command>
   
    <command name="example" connection="self">
     select sum(num) from numbers
    </command>
  </commands>
</SRS>
```
Sum return: 6.300000000000001

To solve this problem you need to use round ()

#### Example 2: OK
```
<SRS>
  <commands>
    <command name="numbers" >
     select 1.1 num
     union
     select 2.1 num
     union 
     select 3.1 num
    </command>
   
    <command name="example" connection="self">
     select round(sum(num),2) from numbers
    </command>
  </commands>
</SRS>
```
Sum return: 6.30


### Parameter conversion error in math operation with date
#### Example 1: FAIL
```
<SRS>
  <parameters>
    <param name="A"  label="A:">30</param>
  </parameters>
  
  <commands>
    <command name="example">
      select getdate()+@A
    </command>
  </commands>
</SRS>
```

#### Example 2: OK
```
<SRS>
  <parameters>
    <param name="A" type="number" label="A:">30</param>
  </parameters>
  
  <commands>
    <command name="example">
      select getdate()+@A
    </command>
   </commands>
</SRS>
```

## Query command and numbers



## Query command basic functions replacement

- https://sqlite.org/lang_corefunc.html
