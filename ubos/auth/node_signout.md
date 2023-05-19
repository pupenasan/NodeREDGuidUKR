# Потік `POST /signout`

Обробляє вихід користувача при вході на сторінку UI [Login](page_login.md). 

```
POST {{main.env.nodeUrl}}/signout
```

![image-20230518154408223](media/image-20230518154408223.png)

## check jwt

```js
msg.cookies={
    user_token: null
}

msg.payload={
    success: true
}

return msg;
```

