# Authentication and Authorization 

**Paanda use Token Based Authentication**

> Token based authentication works by ensuring that each request to a server is accompanied by a signed token which the server verifies for authenticity and only then responds to the request.

**Token is used to identify your account , Teams, and Roles. Paanda has built-in support for**

- Accounts Management, 
- Teams Management, 
- Roles Management



## login


### Request

``` http
POST {{host}}/account/login 
content-type: application/json

{
    "username": "{{username}}",
    "password": "{{password}}"
}
```

Response:

``` http
HTTP/1.1 200 OK
Connection: close
Date: Fri, 17 Apr 2020 23:10:44 GMT
Content-Type: text/plain; charset=utf-8
Transfer-Encoding: chunked
Content-Encoding: gzip
Vary: Accept-Encoding
X-Rate-Limit-Limit: 1h
X-Rate-Limit-Remaining: 4999
X-Rate-Limit-Reset: 2020-04-18T00:10:42.1970778Z

------------------YOUR-SECURITY-TOKEN-------------------
```