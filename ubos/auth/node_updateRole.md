# Потік `PUT /updateRole`

???

![image-20230518164538104](media/image-20230518164538104.png)

## function

```js
msg.collection ="admin_roles"

msg.query={
    _id: objectid(msg.payload._id)
}

msg.payload={
    $set:{
        name: msg.payload.name
    }
}
return msg;
```

