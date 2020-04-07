| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |

## Ведення журналу подій [(Logging)](https://nodered.org/docs/user-guide/logging)

За замовчуванням Node-RED використовує реєстратор (logger), який записує його вихід на консоль. Він також підтримує використання користувацьких модулів реєстрації, що дозволяє відправляти вихідні дані в інше місце.

### Консольний реєстр [(User Guide)](https://nodered.org/docs/user-guide/)

Консольний реєстр може бути налаштований через властивість `logging ` в `settings.js`.

```js
// Configure the logging output
logging: {
    // Console logging
    console: {
        level: "info",
        metrics: false,
        audit: false
    }
}
```

Для налаштування поведінки журналу використовуються 3 властивості:

#### `level`

Деталізація ведення журналу, має наступні опції:

- `fatal` -     слід записати лише ті помилки, які роблять     програму непридатною для використання
- `error` -     записати помилки, які вважаються фатальними     для конкретного запиту
- `warn` -     записувати проблеми, які не є фатальними
- `info` -     запис інформації про загальну роботу     програми
- `debug` -     записувати інформацію, яка є більш     детальним, ніж в info
- `trace` –     дуже детальний запис в журнал
- `off` –     журналювання відсутнє 

Окрім `off`, кожен рівень включає повідомлення на більш високих рівнях наприклад, `warn` рівень включатиме повідомлення `error `та `fatal` .

#### `metrics`

Коли встановлено в `true`, вхідні дані Node-RED дають дані про виконання потоку та використання пам'яті. 

Отримані та відправлені події в кожному вузлі виводяться в журнал. Наприклад, з потоку, який має вузли inject та debug, виводяться наступні записи.

```
9 Mar 13:57:53 - [metric] {"level":99,"nodeid":"8bd04b10.813f58","event":"node.inject.receive","msgid":"86c8212c.4ef45","timestamp":1489067873391}
9 Mar 13:57:53 - [metric] {"level":99,"nodeid":"8bd04b10.813f58","event":"node.inject.send","msgid":"86c8212c.4ef45","timestamp":1489067873392}
9 Mar 13:57:53 - [metric] {"level":99,"nodeid":"4146d01.5707f3","event":"node.debug.receive","msgid":"86c8212c.4ef45","timestamp":1489067873393}
```

Використання пам'яті реєструється кожні 15 секунд.

```
9 Mar 13:56:24 - [metric] {"level":99,"event":"runtime.memory.rss","value":97517568,"timestamp":1489067784815}
9 Mar 13:56:24 - [metric] {"level":99,"event":"runtime.memory.heapTotal","value":81846272,"timestamp":1489067784817}
9 Mar 13:56:24 - [metric] {"level":99,"event":"runtime.memory.heapUsed","value":59267432,"timestamp":1489067784817}audit
```

#### `audit`

Коли audit встановлено в `true`, реєструється доступ до Admin HTTP API. Ця подія включає в себе додаткову інформацію, таку як доступна кінцева точка, IP-адресу та відмітка часу.

Якщо  `adminAuth` активовано, події містять інформацію про користувача, що запитує інофрмацію.

```
9 Mar 13:49:42 - [audit] {"event":"library.get.all","type":"flow","level":98,"path":"/library/flows","ip":"127.0.0.1","timestamp":1489067382686}
9 Mar 14:34:22 - [audit] {"event":"flows.set","type":"full","version":"v2","level":98,"user":{"username":"admin","permissions":"write"},"path":"/flows","ip":"127.0.0.1","timestamp":1489070062519}
```

### Спеціальний модуль реєстрації [(User Guide)](https://nodered.org/docs/user-guide/)

Можна також використовувати спеціальний модуль реєстрації.  Наприклад  вихід `metrics` може бути відправлений в окрему систему для моніторингу продуктивності системи. Щоб використовувати користувальницький реєстратор, змініть `settings.js` додавши посилання на нього.

```js
// Configure the logging output
logging: {
    // Console logging
    console: {
        level: "info",
        metrics: false,
        audit: false
    },
    // Custom logger
    myCustomLogger: {
        level: 'debug',
        metrics: true,
        handler: function(settings) {
            return function(msg) {
                console.log(msg.timestamp, msg.event);
            }
        }
    }
}
```

Властивості `level`, `metrics` і `audit` такі ж самі, як і журналу логів консолі. Властивість `handler` означує користувацький обробник журналу. Це функція, яка викликається один раз під час запуску, переходячи в конфігурацію реєстратора. Вона повинна повернути функцію, яка буде викликатися при формуванню повідомлення в журнал. Можна налаштувати декілька користувацьких реєстраторів - єдине зарезервоване ім'я - `console`.

#### Приклад логера 

У наведеному нижче прикладі додано індивідуальний реєстратор, який надсилає події метрики в екземпляр logstash через TCP-з'єднання. Це дуже швидкий і простий приклад - без обробки помилок або логіки повторної підключення. 

```js
logging: {
    console: {
        level: "info",
        metrics: false,
        audit: false
    },
    logstash: {
        level:'off',
        metrics:true,
        handler: function(conf) {
            var net = require('net');
            var logHost = '192.168.99.100',logPort = 9563;
            var conn = new net.Socket();
            conn.connect(logPort,logHost)
                .on('connect',function() {
                    console.log("Logger connected")
                })
                .on('error', function(err) {
                    // Should attempt to reconnect in a real env
                    // This example just exits...
                    process.exit(1);
                });
            // Return the function that will do the actual logging
            return function(msg) {
                var message = {
                    '@tags': ['node-red', 'test'],
                    '@fields': msg,
                    '@timestamp': (new Date(msg.timestamp)).toISOString()
                }
                try {
                    conn.write(JSON.stringify(message)+"\n");
                }catch(err) { console.log(err);}
            }
        }
    }
}
```



| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |