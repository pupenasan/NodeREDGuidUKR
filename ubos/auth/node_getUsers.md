# Потік `GET /getUsers`

Отримує інформацію про користувачів в заданому форматі. Використовується на сторінці  [User Management](page_usermanagement.md). 

![image-20230518171325765](media/image-20230518171325765.png)

## get users query

```js
msg.collection = "admins";

msg.payload=[
    {
      $match:{
        deleted:false
      }
    },
    {
      $lookup: {
       "from": "admin_roles",
       "localField": "roles",
       "foreignField":"_id",
       "as": "role_items"
     }
    }
]
return msg;
```

