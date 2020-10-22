# Communication foundation

## 1. DB OBJECTS


- [dbo].[comment]
  - comment_sent - wysłano
- [dbo].[comment_list] 
- [dbo].[comment_set]

## 2. SETTINGS


- settings.system.mail_key  (mailgun key)
  - settings.system.mail_from
  - settings.system.mail_domain  (mailgun key)
  - mail_smtp_server 
  - mail_smtp_port
  - mail_smtp_username
  - mail_smtp_password
- `kv.sys.email.template` - mail template file, default: mail-template.md
  - path for templates: wwwroot\templates\
  - supported templates: (.md) MarkDown  , (.html) HTML Template
  - example variables: [[kv.v.api.client]] [[username]] [[kv.v.owner.name]] [[comment_modified_by]] [[comment_text]] [[comment_url]]
- `kv.sys.email.subject` - mail subject, default:Notification  


## components

- v_comment.js

## 10 REST API

### 10.1 TEST EMAIL SENDING

Send single email


***Request***

```http
POST {host}/api/mail/test
```

***Response***

Email massage on authenticated user  mailbox


### 10.2 POST

```http
{host}/api/comments
```

### 10.3 GET Comments (require sys_comments)

```http
{host}/api/comments/browse/{comment_remote_id}/{comment_remote_source?}
```

- [dbo].[comment_list] - procedura 





