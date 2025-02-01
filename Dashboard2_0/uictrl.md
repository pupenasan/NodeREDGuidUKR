| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |

# `ui-control`

https://dashboard.flowfuse.com/nodes/widgets/ui-control.html

Цей віджет не відображає жодного вмісту на інформаційній панелі. Натомість він надає вам інтерфейс для керування поведінкою інформаційної панелі з редактора Node-RED. Функціональність зазвичай поділяється на дві основні характеристики, керування та події, керування:

-  **Navigation**: керування змушує користувача перейти на нову сторінку
-  **Display**: Показує/Приховує групи та сторінки
-  **Disability**: увімкнути/вимкнути групи та сторінки, вони все ще відображаються, але запобігають взаємодії

## Керування

### Navigation

- Зміна сторінки, явно вказуючи сторінку, на яку ви хочете перейти:

```js
// String
msg.payload = '<Page Name>'

// Object
msg.payload = {
    page: '<Page Name>',
}
```

За допомогою формату об’єкта ви також можете вказати параметри запиту для завантаження сторінки:

```js
msg.payload = {
    page: '<Page Name>',
    query: {
        hello: 'world'
    }
}
```

Це призведе до переходу на сторінку з `?hello=world`, доданим до URL-адреси.

- Перейти до наступної або попередньої сторінки в списку:

```js
// Next Page
msg.payload = "+1"

// Previous Page
msg.payload = "-1"
```

- Ви можете примусово оновити поточний перегляд, надіславши порожній рядок:

```js
msg.payload = ""
```

- Якщо ви хочете запустити навігацію до зовнішнього ресурсу або веб-сайту, ви можете зробити це, передавши властивість `url` у `msg.payload`, наприклад:

```js
msg.payload = {
    url: 'https://nodered.org'
}
```



### Show/Hide 

Ви можете програмно показувати/приховувати групи та сторінки з таким корисним навантаженням в `ui-control`:

```js
msg.payload = {
    pages: {
        show: ['<Page Name>', '<Page Name>'],
        hide: ['<Page Name>']
    }
    groups: {
        show: ['<Page Name>:<Group Name>', '<Page Name>:<Group Name>'],
        hide: ['<Page Name>:<Group Name>']
    }
}
```

Примітка: `pages`  можуть бути підпорядковані `tabs` відповідно до Dashboard 1.0, а `groups` також можуть бути підпорядковані `group` аналогічно до Dashboard 1.0.

### Enable/Disable 

```js
msg.payload = {
    pages: {
        enable: ['<Page Name>', '<Page Name>'],
        disable: ['<Page Name>']
    }
    groups: {
        enable: ['<Page Name>:<Group Name>', '<Page Name>:<Group Name>'],
        disable: ['<Page Name>:<Group Name>']
    }
}
```

## Події

### Connection Status 

Ми дотримуємося конвенції Dashboard 1.0 щодо генерування подій на основі сокетів із вузла `ui-control`.

```js
msg = {
    payload: 'connect',
    socketid: '<socketid>',
    socketip: '<socketip>'
}
```

#### .on('connection') 

Коли новий клієнт інформаційної панелі підключається до Node-RED, вузол інтерфейсу керування видасть:

```js
msg = {
    payload: 'connect',
    socketid: '<socketid>',
    socketip: '<socketip>'
}
```

#### .on('disconnect') 

Коли клієнт Dashboard від’єднується від Node-RED, вузол інтерфейсу керування видасть:

```js
msg = {
    payload: 'lost',
    socketid: '<socketid>',
    socketip: '<socketip>'
}
```

### Change Tab/Page 

Коли користувач змінює активну вкладку або сторінку, вузол керування інтерфейсом видає:

```js
msg = {
    payload: 'change',
    socketid: '<socketid>',
    socketip: '<socketip>',
    tab: '<Page Index>',
    name: '<Page Name>'
}
```

