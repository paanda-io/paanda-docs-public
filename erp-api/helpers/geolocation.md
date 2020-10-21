## Geolocation API

Geolocation API uzupełnia geolocation_latitude ,geolocation_longitude w tabeli dbo.geolocation

## 1. DB Objects 

```sql
CREATE TABLE [dbo].[geolocation](
	[geolocation_id] [int] IDENTITY(1,1) NOT NULL,
	[geolocation_latitude] [decimal](18, 9) NULL,
	[geolocation_longitude] [decimal](18, 9) NULL,
	[geolocation_remote_id] [int] NULL,
	[geolocation_remote_uuid] [uniqueidentifier] NULL,
	[geolocation_remote_source] [varchar](36) NULL,
	[geolocation_address] [nvarchar](200) NULL,
	[geolocation_date] [smalldatetime] NULL,
 CONSTRAINT [PK_geolocation] PRIMARY KEY CLUSTERED 
(
	[geolocation_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = OFF, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

```

## 2. Requirements

- Google API key

## 10 REST API

### 10.1 Resolve 50 locations from  [dbo].[geolocation]


***Request***


Http

```http
GET {host}/api/erp/geolocation/resolve/{app_name}
Authorization: Bearer {{token}}
```

HTML

```html
<img src="/api/erp/geolocation/resolve/{app_name}"  alt="GEOLOCATION">
```

Markdown

```md
![GEOLOCATION STATUS](/api/erp/geolocation/resolve/{app_name})
```

***Response***

IMAGE

Aby go użyć wystarczy umieścić odpowiedni link

```html
<img src="/api/erp/geolocation/check/platformaerp" title="Geolocation API Status"/>
```








