# Communication foundation

## 1. DB OBJECTS


- [dbo].[comment]
  - comment_sent - wysłano
- [dbo].[comment_list] 
- [dbo].[comment_set]

## 2. SETTINGS

Supported mail provider in order of importance

- Mailgun (settings.system)
  - mail_key  (mailgun key)
  - mail_domain  (mailgun key)
- SMTP (settings.system)  
  - mail_smtp_server 
  - mail_smtp_port - default 25
  - mail_smtp_username
  - mail_smtp_password
  - mail_smtp_usessl - default true
- Common mail
  - mail_from  - email address
  - mail_replyto - email address
- `kv.v.owner.name` - from Name
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





