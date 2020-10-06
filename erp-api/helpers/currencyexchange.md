# Curency EXchange RATE API

Zródłem kursów jest NBP tabela A dla walut PLN > EUR,USD,...

##  Kursy walut

**Request**

with date

```
{host}/api/erp/currency/rates/pln/{currency ex:eur}?date={isodate ex:2020-01-01}
```

default, day before

```
{host}/api/erp/currency/rates/pln/{currency ex:eur}
```



**Response**

```
{"table":"A","currency":"euro","code":"EUR","rates":[{"no":"181/A/NBP/2020","effectiveDate":"2020-09-16","mid":4.4528}]}
```

