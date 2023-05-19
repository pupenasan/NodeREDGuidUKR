# Потік `PUT /updateChildModule`

Змінює позицію дочірнього модулю в меню батьківського модулю. Налаштовується на сторінці [Modules](page_modules.md). 

```json
{
	"_id": "{{TableParent.selectedRow._id}}",
	"position": "{{positionChild_edit.text}}",
	"name": "{{TableChild.selectedRow.name}}"
}
```

![image-20230518165707755](media/image-20230518165707755.png)

## query

```js
msg.collection = "admin_modules";

msg.query = {
    "_id": objectid(msg.payload._id),
    "childModules.name": msg.payload.name
};

msg.payload = {
    $set: {
        "childModules.$.position": msg.payload.position
    }
}
return msg;
```

