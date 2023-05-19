# Потік `GET /getRoles`

Обробляє запит на перелік ролей AdminRoles, наприклад зі сторінки [AdminRoles](page_adminroles.md)

![image-20230518155521788](media/image-20230518155521788.png)

## function

```js
msg.collection="admin_roles"
msg.payload={
    deleted: false
}
return msg;
```

