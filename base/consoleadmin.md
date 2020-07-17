| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |

## Адміністратор командного рядку 

[Джерело](https://nodered.org/docs/node-red-admin)

Інструмент командного рядка [node-red-admin](http://npmjs.org/package/node-red-admin) дозволяє віддалено керувати екземпляром Node-RED.

### Усановка [(User Guide)](https://nodered.org/docs/user-guide/)

Встановіть це глобально, щоб зробити `node-red-admin` Команда доступна на вашому шляху:

Install this globally to make the `node-red-admin` command available on your path:

```
npm install -g node-red-admin
```

*Примітка* : `sudo` потрібен, якщо він працює як некористувацький користувач на Linux/OS X. Якщо він працює на Windows, вам доведеться запускати в [command shell as Administrator](https://technet.microsoft.com/en-gb/library/cc947813(v=ws.10).aspx), без команди `sudo`.

*Note* : `sudo` is required if running as a non-root user on Linux/OS X. If running on Windows, you will need to run in a [command shell as Administrator](https://technet.microsoft.com/en-gb/library/cc947813(v=ws.10).aspx), without the `sudo` command.

### Об’єкт та вхід [(User Guide)](https://nodered.org/docs/user-guide/)

Щоб дистанційно керувати екземпляром Node-RED, інструмент має вказуватись на екземпляр Node-RED, до якого ви хочете отримати доступ. За замовчуванням він передбачає`http://localhost:1880`. Щоб змінити це, використовуйт команду `target` :

To remotely administer a Node-RED instance, the tool must first be pointed at the Node-RED instance you want it to access. By default, it assumes `http://localhost:1880`. To change that, use the `target` command:

```
node-red-admin target http://node-red.example.com/admin
```

Якщо [автентифікація](https://nodered.org/docs/security) увімкнено, ви повинніввести `login`:

If [authentication](https://nodered.org/docs/security) is enabled, you must then `login`:

```
node-red-admin login
```

Ці команди створюють файл з назвою` ~/.node-red/.cli-config.json` що зберігає об’єкт та отримує інформацію про токен.

These commands create a file called `~/.node-red/.cli-config.json` that stores the target and access token information.

*Примітка*  : Параметр `hash-pw`  *не* вимагає, щоб інструменту для входу в систему і може бути запущений у будь-який час.

*Note* : The `hash-pw` option does *not* require the tool to be logged in and can be run at any time.

### Інші команди [(User Guide)](https://nodered.org/docs/user-guide/)

Інструмент надає наступні команди:

- `list` -     Перелік усіх встановлених вузлів
- `info` -     Показати додаткову інформацію про модуль або набір вузлів
- `enable` -     Увімкнути вказаний модуль або набір вузлів
- `disable` -     Вимкнути вказаний модуль або вузол
- `search` -     Пошук NPM для модулів Node-RED, що  стосуються даного пошукового терміна
- `install` -     Встановити модуль з NPM
- `remove` -     Видалити модуль NPM
- `hash-pw` -     Створити хеш пароля, який можна використовувати з `adminAuth` і `httpNodeAuth` налаштуванням

| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |