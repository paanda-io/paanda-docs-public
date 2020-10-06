# Digital Asset Management



**Paanda has built in support for** 

- public assets
- documents and media files
- workspaces for teams



**Foundations** 

| Category     | Details                                                      | Available  |
| ------------ | ------------------------------------------------------------ | ---------- |
| Flexibility  | Support for common Media Types: Video, Images, PDF, Excel, Word, Text Files, Markdown and others | Cloud      |
| Flexibility  | Multiple storages for one instance                           | Cloud      |
| Availability | Video Media Converter *.MOV to *.MP4 for common support in modern browsers | On-Premise |
| Performance  | Image Optimization and scaling                               | Cloud      |
| Performance  | Support for Etag, Last-Modified Http Headers for better cache handling | Cloud      |
| Performance  | Lazy loading for images                                      | Cloud      |
| Security     | Object usage tracking                                        | Cloud      |
| Security     | Smart rate Limits                                            | Cloud      |





###  `/api/storage` Workspace for documents and application files  

**Usage scenarios**

- Creating workspaces with documents, files 
- Storing application files
- Using as a CMS Assets store

**Extra Features**

- GITHUB support as a source control provider
### `/api/files` for built in editors  (on Premise version only)

Zero configuration store for adhoc use.

### `/api/crm/files`   (on Premise version only)

Dedicated CRM store with additional roles control.

### `/client/` (on Premise version only)

Anonymous access store dedicated for public web assets (*.css, *.js ,*.pdf ,...), with on the fly image optimization and compressed files handling



**Usage scenarios**



- create custom application Interface

- create Themes

- Override existing components / files

  

#### Example 1, loading image

``` http
GET {{host}}/client/images/logo.png HTTP/1.1

HTTP/1.1 200 OK
Connection: close
Date: Thu, 16 Apr 2020 23:27:58 GMT
Content-Type: image/png
Content-Length: 75093
Last-Modified: Thu, 16 Apr 2020 16:02:18 GMT
ETag: "1d6140867570455"
X-Rate-Limit-Limit: 1h
X-Rate-Limit-Remaining: 4998
X-Rate-Limit-Reset: 2020-04-17T00:27:48.4706748Z

```

What happened here

1. Check if file exist in storage "client"
2. if exist serve file
3. if not exist check if file exist in default Client  and serve

#### Example 2, loading style file css




``` http
GET {{host}}/client/css/site.css HTTP/1.1

HTTP/1.1 200 OK
Connection: close
Date: Thu, 16 Apr 2020 23:27:58 GMT
Content-Type: image/css
Content-Length: 75093
Last-Modified: Thu, 16 Apr 2020 16:02:18 GMT
ETag: "1d6140867570455"
X-Rate-Limit-Limit: 1h
X-Rate-Limit-Remaining: 4998
X-Rate-Limit-Reset: 2020-04-17T00:27:48.4706748Z

```

What happened here

1. Check if file exist in storage "client" `/css/site.css`
2. Check if compressed version exist `/css/site.min.css`
3. if exist serve compressed file
4. if not exist check if file exist in default Client
5. If Exist  serve compressed fil
