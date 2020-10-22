# Communication foundation

## 1. DB OBJECTS


- [dbo].[comment]
  - comment_sent - wysłano
- [dbo].[comment_list] 
- [dbo].[comment_set]

## components

- v_comment.js

## 10 REST API

### 10.1 POST

```http
{host}/api/comments
```

### 10.2 GET Comments (require sys_comments)

```http
{host}/api/comments/browse/{comment_remote_id}/{comment_remote_source?}
```

- [dbo].[comment_list] - procedura 





