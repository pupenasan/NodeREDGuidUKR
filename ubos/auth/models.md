[До розділу](README.md)

# Моделі даних в авторизаційному шаблоні

- Parent Module
- Child Module
- Role
- User
- 

## Колекція admin_modules

### Parent Module 

Батьківський модуль - сторінка в меню 1-го (верхнього) рівня, що може включати дочірні.

```js
{
	_id: mogoid,
    name: "name_field.text", //імя модуля
	position: "position_field.text", //позиція в меню
	icon: "icon_field.text",
    deleted: false,
    isParent: true, //чи має дочірні елементи
    childModules:[ //дочірні модулі
        {name: msg.payload.childModule,
         page_id: msg.payload.childModule,
         position: msg.payload.position
        },
        ...
    ]    
}
```

### Child Module 

Дочірній модуль

```js
{
	_id: mongoid,
    name: "name_field.text", //імя модуля
	position: "position_field.text", //позиція в меню
	icon: "icon_field.text",
    deleted: false,
    isParent: false, //дочірній модуль    
}
```

## Колекція admin_roles

### Role

```js
{
    _id: mongoid,
    name: "admin",
    deleted: false,
    permissions: [
      {
        "module": "Management",
        "moduleId": "6464758f1f21a300112a1650",
        "canCreate": true,
        "canRead": true,
        "canEdit": true,
        "canRemove": true
      }
    ],
    "createdAt": "2023-05-16T12:17:20.678Z"
},
```

### User
