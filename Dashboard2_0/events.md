| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |

# `ui-event`

Цей віджет не відображає жодного вмісту на вашій інформаційній панелі. Натомість він відстежує керовану користувачем поведінку та події на вашій інформаційній панелі та надсилає відповідні дані в редактор Node-RED, коли ці події відбулися.

## Список подій

| Event/Topic  | Payload           | Description                                                  |
| ------------ | ----------------- | ------------------------------------------------------------ |
| `$pageview`  | `{ page, query }` | Надсилається щоразу, коли користувач *переглядає* певну сторінку на інформаційній панелі. Деталізує сторінку, визначену панеллю інструментів, і будь-які параметри запиту, знайдені в URL-адресі. |
| `$pageleave` | `{ page }`        | Надсилається кожного разу, коли користувач *залишає* вказану сторінку на інформаційній панелі |

### Example: Page View (`$pageview`) 

Щоразу, коли користувач переглядає сторінку, вузол `ui-event` видасть:

```js
msg = {
    topic: '$pageview',
    payload: {
        page: {
            name: 'Page Name',
            path: '/page/path'
            id: '1234',
            theme: 'dark',
            layout: 'default',
            _groups: []
        },
        query: {
            key: 'value'
        }
    },
    _client: {
        socketId: '1234',
        socketIp: '127.0.0.1',
    }
}
```

```json
{
    "topic": "$pageview",
    "payload": {
        "page": {
            "id": "94bdcee471fa6f2c",
            "type": "ui-page",
            "name": "CFG",
            "ui": "0676d237defb6e8e",
            "path": "/page4",
            "icon": "home",
            "layout": "grid",
            "theme": "dd535c7d1aebf175",
            "breakpoints": [
                {
                    "name": "Default",
                    "px": "0",
                    "cols": "3"
                }
            ],
            "order": 2,
            "className": "",
            "visible": true,
            "disabled": false,
            "route": {
                "path": "/dashboard/page4",
                "name": "Page:CFG"
            }
        },
        "query": {
        }
    },
    "_client": {
        "socketId": "hp9SywSSIKACuzjDAAAH",
        "socketIp": "127.0.0.1"
    },
    "_msgid": "2ad3ddea857c0f56"
}
```



## Custom Events 

У ваших власних вузлах `ui-template` ви можете генерувати власні події, які будуть зафіксовані будь-яким вузлом `ui-event`, що безпосередньо викликає вбудований оператор `$socket`.

Функція `$socket.emit` приймає 3 аргументи:

- Ім'я події, у цьому випадку `ui-event`.
- `id` вузла  `ui-event`, якому ви хочете це передати. Ви також можете використовувати `all` для надсилання до всіх вузлів `ui-event`.
- `msg` , яке ви хочете надіслати.

Отже, у випадку, коли ми хочемо надіслати на певний вузол `ui-event`:

```vue
<v-btn @click="$socket.emit('ui-event', 'ui-event-node-id', msg)">Send Custom Event</v-btn>
```

Or, in the case where we brodcast to *all* `ui-event` nodes:

```vue
<v-btn @click="$socket.emit('ui-event', 'all', msg)">Send Custom Event</v-btn>
```

