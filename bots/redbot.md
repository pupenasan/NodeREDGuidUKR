# RedBot 

<https://github.com/guidone/node-red-contrib-chatbot>

За допомогою **RedBot** ви можете візуально створити повнофункціональний чат-бот для **Telegram**, **Facebook Messenger**, **Viber**, **Twilio** та **Slack** за допомогою Node-RED . ~~Майже~~ навички кодування не потрібні.

[![RedBot](media/node-red-screenshot.png)](https://github.com/guidone/node-red-contrib-chatbot/blob/master/docs/images/node-red-screenshot.png)

## Документація

1. [RedBot nodes](https://github.com/guidone/node-red-contrib-chatbot/wiki/RedBot-nodes)
2. [Examples](https://github.com/guidone/node-red-contrib-chatbot/wiki#examples)
3. [Advanced examples](https://github.com/guidone/node-red-contrib-chatbot/wiki#advanced-examples)
4. [Chat context](https://github.com/guidone/node-red-contrib-chatbot/wiki/Chat-Context)
5. [Changelog](https://github.com/guidone/node-red-contrib-chatbot/wiki/Changelog)

## Швидкий старт

Наступним кроком є створення чат -бота, я рекомендую використовувати **Telegram**, оскільки налаштування простіше (**Telegram** дозволяє проводити опитування для отримання повідомлень, тому необов’язково створювати сертифікат https). Використовуйте **@BotFather **, щоб створити чат -бота, [дотримуйтесь інструкцій тут](https://core.telegram.org/bots#botfather), а потім скопіюйте свій доступ до **токена**.

Потім відкрийте свій **Node-RED** і додайте `Telegram Receiver` на панелі конфігурації, додайте нового бота та вставте **маркер**

[![Telegram Receiver](media/example-telegram-receiver.png)](https://github.com/guidone/node-red-contrib-chatbot/raw/master/docs/images/example-telegram-receiver.png)

Тепер додайте вузол `Повідомлення` та під’єднайтесь до `Telegram Receiver`

[![Simple Message](media/example-simple-message.png)](https://github.com/guidone/node-red-contrib-chatbot/raw/master/docs/images/example-simple-message.png)

Нарешті, додайте вузол `Telender Sender`, не забудьте вибрати на панелі конфігурації того самого бота ` Telegram Receiver`, це має бути остаточний макет

[![Example Simple](media/example-simple.png)](https://github.com/guidone/node-red-contrib-chatbot/raw/master/docs/images/example-simple.png)

Тепер у вас є корисний бот, який відповідає на будь -яке отримане повідомлення *Привіт!*. Ми можемо зробити набагато краще.