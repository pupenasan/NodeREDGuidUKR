[Статті](README.md)

# Автентифікація Node-RED за допомогою JSONWebToken

Ориігнальна стаття

-  [Authenticating Node-RED with JSONWebToken Part1](https://www.compose.com/articles/authenticating-node-red-with-jsonwebtoken/)
- [Authenticating Node-RED using JSONWebToken - Part 2](https://www.compose.com/articles/authenticating-node-red-using-jsonwebtoken-part-2/)

[Node-RED](http://nodered.org/) чудово підходить для [потужного прототипування](https://www.compose.com/articles/power-prototyping-with-mongodb-and-node-red-2/), але як утримати поганих хлопців (або широку громадськість, якщо на те пішло) від використання ваших кінцевих точок без дозволу? Коли прийшов час подумати про автентифікацію, [JSONWebToken (JWT)](https://jwt.io/) — це елегантний і простий спосіб перевірити ідентифікатор ваших користувачів на вході.

Автентифікація не обов’язково обмежується HTTP та веб-викликами. JSONWebToken можна використовувати для автентифікації даних з будь-якого джерела. Отже, якщо ви хочете почати з HTTP, а потім переходити до WebSockets або RabbitMQ пізніше ви зможете автентифікуватися за допомогою того самого методу.

Використовувати JSONWebToken у Node-RED легко завдяки бібліотеці вузлів [node-jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) і вузла  [node-red-contrib-auth](https://www.npmjs.com/package/node-red-contrib-auth). У першій статті, що складається з двох частин, ми використаємо ці бібліотеки, щоб швидко та легко додати криптографічно безпечну автентифікацію до нашої програми Node-RED. У другій частині ми покажемо вам, як використовувати це з вашою базою даних Compose MongoDB для створення токенів автентифікації користувача.

У цій статті ми використаємо пакет *node-red-contrib-auth*, ви можете встановити його прямо з Node-RED.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1480717219/dq9mmogvyoaapneifm2p.gif)

## Кодування даних у JSONWebToken

Ми почнемо з перетягування вузла введення на полотно Node-RED. Наразі ми будемо використовувати вхідний вузол *http*, але майте на увазі, що це можна зробити з будь-яким типом вхідного вузла. Спочатку перетягніть вузол введення *HTTP* на полотно та двічі клацніть його, щоб налаштувати. Встановіть *URL* вузла на `/encrypt` і метод на *GET*.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1480717352/yljupcdbbs3gn3u3mieq.gif)

Далі ми знайдемо вузол *JWT* на палітрі та перетягнемо його на полотно поруч із вузлом введення *HTTP*. Двічі клацніть його, щоб відкрити панель конфігурації, а потім клацніть піктограму олівця поруч зі спадним меню з написом `Add new JsonWebToken_config`. Дайте конфігурації унікальне ім’я та введіть довільний набір символів у розділі `secret`. Ви хочете, щоб секрет був випадковим і неможливим для вгадування – це буде ключ, який ви використовуєте для шифрування та дешифрування JSONWebToken.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1480717965/mmmwtlc94idohqnqavl4.gif)

Вузол *JWT* кодуватиме будь-які дані в об’єкті `msg.payload` у криптографічно захищений JSONWebToken, використовуючи секрет шифрування, який ви налаштували. Нарешті, він передасть цей JSONWebToken на вихід через об’єкт `msg.token`, піклуючись про збереження оригінального `msg.payload`.

Оскільки ми хочемо, щоб JSONWebToken надсилався на вихідний вузол, давайте додамо сюди вузол `change` і передамо `msg.token` до `msg.payload`. 

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1480718232/weaah06rqtkyn2prsdr9.gif)

Тепер давайте перетягнемо вихідний вузол *HTTP Response* на полотно. Це гарантує, що будь-які запити, зроблені до вхідного вузла, отримають відповідь. Коли ми отримуємо доступ до цього маршруту, будь-які дані, передані у вхідний вузол *HTTP* як параметр рядка запиту, автоматично додаються до об’єкта `msg.payload`. Потім він пройде через вузол *JWT* і виведе зашифрований маркер, який буде повернуто у відповідь.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1480718330/t7eh1lamac78dxbfgnyy.gif)

## Декодування даних із JSONWebTokens

Вузол *JWT* шифруватиме дані, передані йому в `msg.payload`, але він також намагатиметься розшифрувати JSONWebTokens, передані йому в об’єкті `msg.token`. Щоб декодувати маркер, вам потрібно буде використати той самий ключ, що використовувався для шифрування оригінального маркера.

Для цього прикладу ми створимо вузол введення *HTTP*, який розшифровуватиме JSONWebToken і повертатиме розшифровані дані у вузлі *HTTP Response*. Перетягніть вузол введення *HTTP* на полотно та двічі клацніть його, щоб налаштувати. Встановіть *URL* вузла на `/decrypt` і метод на *GET*:

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1480718441/nujboqww5cjfhvunoxyb.gif)

Потім перетягніть той самий вузол *JWT* на полотно поруч із вузлом введення *HTTP*. Двічі клацніть його, щоб налаштувати вузол і переконайтеся, що ви вибрали ту саму конфігурацію зі спадного списку, яку ви використовували для шифрування маркера раніше.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1480718551/p3abrjmctgsqy1nh4y2n.gif)

Наразі у нас є вузол *JWT*, який очікує розшифрування будь-яких даних, переданих до нього через об’єкт `msg.token`, і вузол *HTTP input*, який передає дані *POST* через `msg.req.body`. об'єкт. Тепер нам потрібен вузол `function` для передачі відповідного параметра з `msg.req.body` до `msg.token`. Перетягніть новий вузол `function` на полотно між вузлом введення *HTTP* і вузлом *JWT* та додайте такий код:

```javascript
msg.token = msg.req.body.access_token;  
return msg;  
```

Це передбачає, що маркер, який ви хочете розшифрувати, надсилається в об’єкті JSON, який виглядає так:

```json
{ "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiam9obiIsImlhdCI6MTQ4MDcyNjIzOH0.QMAH5MrAGbpnwr_mCycE3Qx_YKLujMxYDc1SNbfURtsckear"}
```

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481091302/kfqkeewmeevfmqx3p2rw.gif)

Оскільки розшифроване значення повертається до об’єкта `msg.token`, нам потрібно буде додати другу *функцію* з іншого боку вузла *JWT*, щоб передати розшифровані значення об’єкту `msg.payload` . Перетягніть новий функціональний вузол на полотно та двічі клацніть його, щоб додати такий код:

```javascript
msg.payload = msg.token;  
return msg;  
```

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481091429/ymf3qnd8nliyrhbpf39y.gif)

Нарешті, перетягніть вихідний вузол *HTTP Response* на полотно та з’єднайте вузли.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481091576/yn2ifcfxdc76ojhkbcdx.gif)

Ви можете випробувати наш абсолютно новий кодер/декодер JSONWebToken за допомогою наступних команд *CURL*, не забувши замінити наведені нижче значення своїми власними значеннями.

```shell
$ curl -i -H "Accept: application/json" http://localhost/encrypt?name=john
```

який зашифрує ім’я в JSONWebToken, який виглядає приблизно так:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiam9obiIsImlhdCI6MTQ4MDcyNTg2NH0.Rz-0Smq_ulmriXLVO9weN_CnO4CnwPh35ktAbmAdhZg  
```

Розшифровка виглядає приблизно так:

```shell
% curl -H "Content-Type: application/json" -X POST -d '{"access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiam9obiIsImlhdCI6MTQ4MDcyODYxMH0.D0fU4Wg3wNeH0Ui9A0JU1_flFXNpvntk_LfqtCLsAOY"}' http://localhost/decrypt
```

і виведе значення, закодоване в маркері:

```json
{"name":"john","iat":1480728610}
```

У цій частині статті розглянули захист даних за допомогою JSONWebTokens у Node-RED. Ви можете використовувати JSONWebToken для шифрування конфіденційної інформації, як-от даних користувача, які потрібно безпечно передавати через незахищені мережі. У наступній частині статті ми розглянемо використання JSONWebTokens для авторизації та автентифікації дій користувачів у програмі Node-RED за допомогою MongoDB на Compose.

## Встановлення вузл *node-red-contrib-mongodb2*

Щоб обробити вхід користувача, нам спочатку потрібно підключитися до екземпляра MongoDB, який зберігає наших користувачів. Ми використаємо вузол `node-red-contrib-mongodb2` для встановлення з’єднання. Встановіть пакет  `node-red-contrib-mongodb2`.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1480725462/qnfed19xt6gsvqzvqwbg.gif)

## Налаштуйте кінцеві точки

Давайте почнемо зі створення простого процесу автентифікації користувача. Потік автентифікації користувача складатиметься з трьох кінцевих точок: форми *для входу*, яка приймає ім’я користувача та пароль, *маршруту для обробки входу*, який перевірятиме облікові дані користувачів і повертатиме JSONWebToken з інформацією про цих користувачів, і захищений маршрут, який вимагає від користувача надати маркер, перш ніж отримати до нього доступ.

Спочатку ми перетягнемо три вузли введення *HTTP* на полотно. Налаштуйте перший вузол за допомогою методу **GET** і URL-адреси **/login**. Цей маршрут надасть користувачеві форму входу.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481096670/vpchbrbbkususfiukrvt.gif)

Налаштуйте другий вузол за допомогою методу **POST** і URL-адреси **/process_login**. Сюди буде надіслано облікові дані користувача для перевірки та JSONWebToken, згенерований із цих облікових даних.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481096673/lwax4peqabgtwg2hlfjl.gif)

Нарешті, налаштуйте останній вузол введення *HTTP* за допомогою методу **GET** і URL-адреси **/protected**. Це буде маршрут, який буде недоступним, якщо користувач не автентифікований.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481096677/neoeu05aij9649u9p1yf.gif)

## Створіть форму входу

Далі ми створимо просту форму входу в HTML з текстовим полем імені користувача та пароля та кнопкою відправки. Перетягніть вузол `template` на полотно з палітри та розмістіть його біля виходу вузла *HTTP in* з URL-адресою */login*.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481097021/ncthoc1u21kioekqrnto.gif)

Потім двічі клацніть вузол template та додайте HTML-форму з дією **/process_login** і методом **POST**.

```javascript
<html>  
   <head>
   </head>
   <body>
      <form action="/process_login" method="POST">
         <label for="username">Login</label>
         <input name="username" type="text" />
         <br />
         <label for="password">Password</label>
         <input name="password" type="password" />
         <br />
         <input type="submit" />
      </form>
   </body>
</html>  
```

Нарешті, перетягніть вузол *HTTP-відповіді* на полотно та підключіть усе.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481128359/riuf1qnkzdh4cgg2sval.gif)

## Додайте обробку входу за допомогою *mongodb2*

Перше, що вам знадобиться, це екземпляр MongoDB. Ви можете розгорнути [Compose MongoDB database with SSL enabled](https://www.compose.com/articles/connecting-to-the-new-mongodb-at-compose/)  або запустити свій власний локальний екземпляр MongoDB. Розпочати нове розгортання на Compose – це найпростіший спосіб розпочати роботу.

Потім підключіться до свого розгортання MongoDB за допомогою вузла *mongodb2*. Інструкції щодо цього можна знайти в [попередній статті цієї серії](https://www.compose.com/articles/authenticating-node-red-with-jsonwebtoken/). Після того, як ви налаштували свій вузол *mongodb2*, нам потрібно додати користувача до нашої бази даних. Ми зробимо це за допомогою вузла *inject*, який дозволить нам вставляти дані в потік, натиснувши кнопку.

Перетягніть вузол *inject* на полотно та двічі клацніть його, щоб налаштувати. У розділі *payload* клацніть спадне меню **timestamp** та виберіть **{} JSON**. Потім вставте таку інформацію про користувача в текстове поле в *payload* (ви можете замінити власну інформацію, якщо хочете):

```json
{ "username": "admin", "password": "secret", "firstName": "John", "lastName": "O'Connor", "email": "johnwoconnor@compose.io" }
```

Наразі ми будемо зберігати цей пароль у вигляді звичайного тексту, оскільки ми використовуємо простий механізм автентифікації. На практиці ви ніколи не захочете зберігати свої паролі у вигляді відкритого тексту – замість цього ви захочете зашифрувати свій пароль за допомогою чогось на зразок [bcrypt](https://www.compose.com/articles/you-may-get-pwned-at-least-protect-passwords-with-bcrypt/).

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482254806/rpz6lr2sw5oofinuz9fw.gif)

Потім перетягніть вузол *mongodb2* на полотно та двічі клацніть його, щоб налаштувати. Введіть **Users** в розділі *Collection* конфігурації та виберіть **insert** зі спадного меню *Operation*.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481129759/lmv8jyliffsgsokolyyo.gif)

Ми також розмістимо вузол *debug* біля виводу вузла *mongodb2*, щоб ми могли бачити будь-які повідомлення, які повертаються з вузла. Підключіть все та натисніть **Deploy**.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481130303/uyzicvdkdtbq85rju9ao.gif)

Нарешті, давайте введемо нашого нового користувача в базу даних. Натисніть кнопку, приєднану до вузла *inject*, щоб надіслати об’єкт JSON, який ви визначили вище, до бази даних. Ви можете ще раз перевірити, чи існує користувач, перейшовши на консоль Compose і переглянувши колекцію.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1481130700/adbayclxlsweruimdoct.gif)

Тепер, коли у нас є деякі дані в базі даних, ми можемо отримати ці дані та безпечно зберігати та передавати їх за допомогою JSONWebToken.

## Зашифруйте дані користувача в JSONWebToken

Давайте почнемо з використання нашої обробки входу, щоб отримати користувача з бази даних. Перетягніть вузол *function* на полотно біля вузла введення *HTTP* за допомогою методу *POST* і маршруту */login*. Потім двічі клацніть, щоб додати такий код до функції:

```js
msg.userData = msg.payload;  
msg.payload = {  
    username: msg.userData.username
};
return msg;  
```

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482178539/cya2clzdohyrafzuyhqj.gif)

Це збереже дані форми, які передаються у функцію, в об’єкт `msg.userData`. Потім ми змінимо `msg.payload`, щоб його можна було передати у вузол *mongodb2* як запит до бази даних. Потім перетягніть новий вузол *mongodb2* біля результату *function* та двічі клацніть його, щоб налаштувати. Використовуйте операцію **findOne** і введіть **Users** у полі **collection** (переконайтеся, що назва колекції відповідає колекції, до якої ви вставили користувача раніше).

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482255084/zznpkoqgsuozogsabisy.gif)

JSONWebToken не залежить від механізму входу, який ви використовуєте. Заради простоти ми наразі ігноруватимемо фактичну перевірку пароля й просто припустимо, що вхід був успішним. На практиці ви можете вибрати будь-який метод автентифікації для підтвердження облікових даних користувача.

Якщо у вас уже є JSONWebToken *Token Configuration* маркера з попередньої статті цієї серії, ви можете пропустити наступний абзац. В іншому випадку вам потрібно буде створити *Token Configuration*.

Щоб створити конфігурацію маркера, вам спочатку потрібно знайти вузол *JSONWebToken* на палітрі та перетягнути його на полотно. Двічі клацніть його, щоб відкрити панель конфігурації, а потім клацніть піктограму олівця поруч зі спадним меню з написом Add new JsonWebToken_config. Дайте конфігурації унікальне ім’я та введіть довільний набір символів у секретному розділі. Ви хочете, щоб секрет був випадковим і неможливим для вгадування – це буде ключ, який ви використовуєте для шифрування та дешифрування JSONWebToken.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482249817/hlxb36mothskpzdsj8fg.gif)

Тепер, коли у вас є *Token Configuration*, ви можете передати дані користувача у вузол *JSONWebToken*, щоб зашифрувати їх. Якщо ви ще цього не зробили, перетягніть вузол *JSONWebToken* на полотно після виведення вузла *mongodb2* і двічі клацніть його, щоб налаштувати. Виберіть *Конфігурацію маркера*, яку ви створили раніше, зі спадного меню та назвіть вузол *encrypt* (або будь-який інший, який ви дійсно хочете).

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482255448/kejin0aq4ngjacgy4u42.gif)

Тепер, коли ми налаштували наш JSONWebToken, ми можемо почати його використовувати. Вузол *JSONWebToken* зберігає зашифрований маркер в об’єкті `msg.token`. Оскільки ми хочемо надіслати маркер як вихід, ми перемістимо `msg.token`, створений вузлом `JSONWebToken`, до `msg.payload` за допомогою вузла *change*. Двічі клацніть вузол *change* і налаштуйте його, щоб SET  для `msg.payload` значення `msg.token`.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482184324/bpexrm0463gxdwrv5yja.gif)

Оскільки ми почали з вузла введення *HTTP*, нам потрібно додати вузол *HTTP-response*, щоб завершити відповідь. Перетягніть вузол *HTTP-response* на полотно поруч із вузлом *JSONWebToken*, з’єднайте їх усі разом і натисніть **DEPLOY**. Коли ви надішлете форму входу, згенерований маркер буде повернено як відповідь.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482184664/uo5zobo8qmlnqh6iqbzk.gif)

Тепер, коли ми налаштували форму входу, перейдіть до своєї форми входу, перейшовши за адресою `http://yourserver/login` у своєму браузері, замінивши `yourserver` місцем установки Node-RED. Введіть *admin* у розділ *ім’я користувача* форми входу та будь-що в якості пароля (наразі ми ігноруємо пароль). Коли ви натискаєте **submit**, вас має бути перенаправлено на веб-сторінку з вашим JSONWebToken, яка виглядає приблизно так:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1ODQ4NDI2NWVmYTY0MDAwMWM2ZDBlZDAiLCJ1c2VybmFtZSI6ImFkbWluIiwiaWF0IjoxNDgyMTg0NDI0fQ.86PuteGK1JxpfsHhhckkqElbcseoCjAqpe083kRzCko
```

Цей JSONWebToken містить зашифровані дані для вашого користувача, і їх можна розшифрувати лише за допомогою того самого секретного ключа, який ви використовували для шифрування. Давайте подивимося, як працює цей процес дешифрування.

## Розшифруйте дані користувача з JSONWebToken

Ваш JSONWebToken із попереднього розділу тепер містить зашифровані дані про вашого користувача. Щоб розшифрувати дані, нам просто потрібно знову запустити їх через вузол *JSONWebToken*. Якщо ви використовуєте той самий ключ і *Token Configuration*, вузол *JSONWebToken* розшифрує всі дані, що зберігаються в об’єкті `msg.token`.

Тепер давайте перевіримо це на нашому */protected* маршруті. Перейдіть до `yourserver/protected` у веб-браузері та передайте JSONWebToken як параметр рядка запиту під назвою *token*, тому виклик нашого маршруту `/protected` може виглядати приблизно так:

```
yourserver/protected?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1ODQ4NDI2NWVmYTY0MDAwMWM2ZDBlZDAiLCJ1c2VybmFtZSI6ImFkbWluIiwiaWF0IjoxNDgyMTg1MDcyfQ.KxmCfxj8rGKbkZu_Wfu75lHRIPjWjpH_apY58HnJgS0
```

Як нагадування, переконайтеся, що ви замінили `yourserver` місцем встановлення Node-RED.

Node-RED розмістить параметр рядка запиту `token` в об’єкт `msg.payload.token`. Оскільки *JSONWebToken* очікує, що маркер буде в об’єкті `msg.token`, нам потрібно буде перемістити його за допомогою вузла *function*. Перетягніть вузол *function* на полотно та двічі клацніть його, щоб налаштувати. Оскільки у функції є два виходи, нам також потрібно буде оновити розділ *outputs* внизу конфігурації *function*. Змініть значення в полі введення з `1` на `2`. Потім додайте наступний код до вузла функції:

```javascript
if (msg.payload.token) {  
   msg.token = msg.payload.token;
   node.send(msg);
} else {
   msg.statusCode = 403;
   node.send([null, msg]);
}
```

Тут ми використовуємо API `node.send` для умовного надсилання повідомлення на один із двох виходів функції. Перша частина умовного оператора надсилатиме `msg.token` до вузла *JSONWebToken*, а інша повертатиме користувачеві повідомлення про помилку, встановлюючи `msg.statusCode` значення 403 (Unauthorized) і передаючи його безпосередньо до Вузол *HTTP-response*.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482187819/fhocs3jinuppyk9dgnmu.gif)

Коли умова помилки оброблена, ми перетягнемо вузол *JSONWebToken* на полотно та двічі клацнемо його, щоб налаштувати. Переконайтеся, що ви вибрали ту саму конфігурацію зі спадного меню, яку використовували для шифрування маркера.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482188292/nwt4hvqnrf0aiwkwkhfd.gif)

*JSONWebToken* повертає розшифроване повідомлення в об’єкт `msg.token`. Оскільки ми хочемо надіслати його назад користувачеві, нам потрібно буде передати його в об’єкт `msg.payload`. Давайте зробимо це, перетягнувши вузол *change* поруч із вузлом *JSONWebToken* і встановивши для `msg.payload` значення з `msg.token`.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482188557/g5jbdmjodjdnpbnrahqm.gif)

Нарешті, ми перетягнемо вузол *HTTP-response* і з’єднаємо їх усі разом. Оскільки ми маємо два виходи з нашого вузла *function*, переконайтеся, що перший вихід функції підключено до вузла *JSONWebToken*. У вас уже має бути другий вихід, підключений до вузла *HTTP-response*. Потім натисніть **DEPLOY**, щоб розгорнути зміни.

![img](https://res.cloudinary.com/dyyck73ly/image/upload/v1482188957/vup6rexdhjmtr30xexaq.gif)

Давайте перевіримо це, викликавши наш маршрут `/protected` і передавши наш JSONWebToken за допомогою параметра рядка запиту *token*. Остаточний маршрут виглядає так:

```
http://yourdomain/protected?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1ODQ4NDI2NWVmYTY0MDAwMWM2ZDBlZDAiLCJ1c2VybmFtZSI6ImFkbWluIiwiaWF0IjoxNDgyMTg1MDcyfQ.KxmCfxj8rGKbkZu_Wfu75lHRIPjWjpH_apY58HnJgS0
```

і має отримати такий результат:

```javascript
{"_id":"58484265efa640001c6d0ed0","username":"admin","iat":1482185072}
```

# Підсумок

Тепер, коли ви зібрали всі частини разом, ви можете почати підключати безпечні програми, які підключаються до локальної або хмарної бази даних, наприклад Compose MongoDB. Є деякі покращення, які ми все ще можемо зробити, як-от безпечне зберігання та перевірка облікових даних користувачів, але це має стати хорошою відправною точкою.