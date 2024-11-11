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

## Custom Events 

У ваших власних вузлах `ui-template` ви можете генерувати власні події, які будуть зафіксовані будь-яким вузлом `ui-event`, що безпосередньо викликає вбудований оператор `$socket`.

The `$socket.emit` function takes in 3 arguments:

- The event name, in this case, `ui-event`
- The `id` of the `ui-event` node you want to emit this to. You can also use `all` to emit to all `ui-event` nodes.
- The full `msg` you want to send.

So in the case where we want to send to a specific `ui-event` node:

```vue
<v-btn @click="$socket.emit('ui-event', 'ui-event-node-id', msg)">Send Custom Event</v-btn>
```

Or, in the case where we brodcast to *all* `ui-event` nodes:

```vue
<v-btn @click="$socket.emit('ui-event', 'all', msg)">Send Custom Event</v-btn>
```

