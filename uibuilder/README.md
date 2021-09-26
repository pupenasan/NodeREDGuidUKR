# node-red-contrib-uibuilder

<https://github.com/TotallyInformation/node-red-contrib-uibuilder#node-red-contrib-uibuilder>

Конструктор веб-інтерфейсу користувача Node-RED. uibuilder прагне надати простий у використанні спосіб створення динамічних веб-інтерфейсів за допомогою будь-яких (або без них) front end бібліотек для зручності.

**Основні можливості та переваги:**

- Розроблено як альтернативу офіційній Node-RED Dashboard. Без накладних витрат та обмежень.
- Керується все з адміністративного інтерфейсу Node-RED. Редагуйте ресурси front-end, керуйте пакетами інтерфейсу. Немає необхідності отримувати доступ до командного рядка серверів.
- Керування шаблонами запуску. Доступні внутрішні шаблони для VueJS та bootstrap-vue. Завантажуйте шаблони з інших сховищ за допомогою *degit*. Полегшує обмін шаблонами, які надають цілий додаток або просто мають справу з шаблоном.
- Майте стільки користувацьких інтерфейсів, скільки хочете. Для кожної точки входу потрібен лише 1 вузол. Використовуйте вузли `link` для надсилання даних з інших частин ваших потоків.
- Має інтерфейс керування окремо від інтерфейсу повідомлень. Дізнайтесь, коли браузер підключається або відключається, надсилайте кешовані дані.
- Has a control interface separate to the message interface. Know when a browser connects or disconnects, send cached data.
- Може бути набагато легшим за вагою та зручнішим для мобільних пристроїв, ніж офіційна інформаційна панель Node-RED.
- Автоматично знаходить ці пакетні фреймворки, якщо вони встановлені у вашій папці `userDir`. Робить їх доступними через вбудований веб-сервер Node-RED: vue, bootstrap, bootstrap-vue, Svelte, jquery, moonjs, Reactjs, Riot, Angular, Picnic, Umbrellajs (зверніть увагу, що цей список може розширюватися).
- Використовуйте **будь-який** інтерфейсний фреймворк, який вам подобається. Перевірено принаймні  [JQuery](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/Example:-JQuery), [VueJS](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/Simple-Example-using-VueJS), [MoonJS](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/Example,-MoonJS-with-Mini.CSS), [REACT](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/Example:-ReactJS), [UmbrellaJS](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/Example-Umbrella-JS-and-Picnic-CSS) та [Riot](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/Basic-uibuilder-RIOT-example-displaying-values,-switch-and-select-box). . Просто встановіть за допомогою вбудованого менеджера бібліотек.

- Використовуйте без будь-якого інтерфейсного фреймворка, якщо хочете. Тримайте його легким і простим. Спробуйте це за допомогою шаблону "Пустий".
- Включена front-end бібліотека (uibuilderfe) забезпечує підключення до Node-RED та обробки подій повідомлень.
- Напишіть власний HTML, CSS та JavaScript, щоб визначити ідеальний інтерфейс користувача для ваших потреб.
- Редагуйте власний front-end код у редакторі Node-RED, майже не потребуючи доступу до файлової системи сервера. Автоматичне перезавантаження ваших клієнтів при змінах у коді. Відмінно підходить для швидкої розробки.
- Для роботи майже не потрібно шаблонів у вашому front-end коді.
- Включено розширені приклади потоків VueJS, MoonJS та кешування.
- Опційний перелік доступних файлів на веб-сторінці index.
- Дві докладні веб-сторінки з інформацією для адміністратора включені, щоб допомогти авторам зрозуміти, де все є і що є.
- За замовчуванням використовує власні веб-сервери Node-RED. (Незабаром отримає можливість самостійно працювати в окремому порту за бажання).

**Поточні обмеження такі:**

- Ви повинні написати свій власний HTML, uibuilder (поки) не робить це за вас. *Це за задумом. Я сподіваюся, що колись буде доступний компонентний дизайн, який надасть додаткові можливості та спростить створення інтерфейсу користувача.*

- Ви повинні знати розташування інтернет-бібліотек для встановлених бібліотек і відповідно редагувати HTML. API адміністратора `uibindex` (доступний з інтерфейсу адміністратора будь-якого вузла) показує всі кореневі папки та те, що автори пакунків повідомляють як основну точку входу для всіх активних пакетів. Тепер для спрощеного перегляду екземпляра вузла uibuilder також є спрощена інформація, це доступ за допомогою кнопки на панелі конфігурації.

  Зауважте, що це обмеження `npm` та авторів модулів, а не uibuilder. Якщо автори модулів правильно не визначать точку входу браузера для своїх бібліотек, uibuilder може тільки здогадуватися.

- Ви ще не можете компілювати/стискати власний інтерфейсний код (HMTL, JS, SCSS тощо) для ефективності. *Це буде додано незабаром.*

  Для цього буде використано локальний файл package.json, який містить скрипт "build". Якщо він існує, uibuilder відкриє кнопку build, яка запускатиме сценарій.

uibuilder скоріше альтернатива Node-RED Dashboard. У той час як Dashboard розроблений для того, щоб створити дуже простий інтерфейс користувача, але він торгується з деякими обмеженнями, uibuilder розроблений, щоб дозволити вам робити все, що ви думаєте, з будь-якою структурою (або ні з якою), але у компроміс з тим, щоб написати свій власний front-end код.

uibuilder, як правило, також має бути на **багато** швидшим та ефективнішим у використанні ресурсів, ніж Dashboard, хоча це, очевидно, залежить від того, які інтернет-бібліотеки та фреймворки ви вирішите використовувати.

## Зміст

- [Contents](https://github.com/TotallyInformation/node-red-contrib-uibuilder#contents)

- [1. Additional Documentation](https://github.com/TotallyInformation/node-red-contrib-uibuilder#1-additional-documentation)

- 2. Getting Started

  - [2.1. Install](https://github.com/TotallyInformation/node-red-contrib-uibuilder#21-install)
  - [2.2. Simple flow](https://github.com/TotallyInformation/node-red-contrib-uibuilder#22-simple-flow)
  - [2.3. Edit the source files](https://github.com/TotallyInformation/node-red-contrib-uibuilder#23-edit-the-source-files)
  - [2.4. Install additional front-end libraries](https://github.com/TotallyInformation/node-red-contrib-uibuilder#24-install-additional-front-end-libraries)
  - [2.5. Additional Documentation](https://github.com/TotallyInformation/node-red-contrib-uibuilder#25-additional-documentation)

- [3. Features](https://github.com/TotallyInformation/node-red-contrib-uibuilder#3-features)

- [4. Known Issues](https://github.com/TotallyInformation/node-red-contrib-uibuilder#4-known-issues)

- [5. Discussions and suggestions](https://github.com/TotallyInformation/node-red-contrib-uibuilder#5-discussions-and-suggestions)

- [6. Contributing](https://github.com/TotallyInformation/node-red-contrib-uibuilder#6-contributing)

- [7. Developers/Contributors](https://github.com/TotallyInformation/node-red-contrib-uibuilder#7-developerscontributors)

## 1. Додаткова документація

У [WIKI](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki) доступно набагато більше інформації. Крім того, у папці [docs](https://github.com/TotallyInformation/node-red-contrib-uibuilder/blob/main/docs) також є доступна додаткова технічна документація та документація для розробників, яка буде доступна щойно ви додасте uibuilder на палітру Node-RED, як веб-сайт документації за адресою `<node-red-editor-url>/uibdocs`. На панелі конфігурації є кнопка для цього. Ви також можете отримати доступ до цієї документації [тут](https://totallyinformation.github.io/node-red-contrib-uibuilder).

## 2. Getting Started

### 2.1. Install

To install the current live version, please use Node-RED's Palette Manager.

**NOTE**: As of v3.1.3, npm cannot safely install the  VueJS and bootstrap-vue default dependencies. If you want to use the  provided VueJS templates, you must install these yourself. Either use  uibuilder's library manager or manually install from the command line:

```
#cd <userDir>
npm install vue@"2.*" bootstrap-vue@"2.*"
```

To install a specific uibuilder development or test branch from GitHub, use `npm install TotallyInformation/node-red-contrib-uibuilder#<BRANCH-NAME>` from the command line on the server, having first changed to the `userDir` folder (normally `~/.node-red`). If you just want the `main` branch which contains the latest development build, you can do `npm install TotallyInformation/node-red-contrib-uibuilder`

To install a specific release from npm, use `npm install node-red-contrib-uibuilder@<VERSION>`. In addition to release versions (e.g. 1.2.2), you can also use `latest` and `v1-last`. Sometimes, `next` may also be available. Check out the [Versions tab](https://www.npmjs.com/package/node-red-contrib-uibuilder?activeTab=versions) on the npm site for available versions.

**NOTE**: When installing uibuilder v2+, you may get a warning from the install:

> ```
> npm WARN bootstrap@4.3.1 requires a peer of jquery@1.9.1 - 3 but none is installed. You must install peer dependencies yourself
> ```

It is safe to ignore that warning unless you want to take control of  bootstrap yourself since vue-bootstrap doesn't actually need it.

### 

### 2.2. Простий потік

Після установки,

1. додайте простий потік, що складається з trigger, uibuilder і вузла debug, всі з'єднані по порядку.
2. Тоді розгорніть зміни
3. двічі клацніть на вузлі uibuilder,
4. клацніть URL-адресу веб-сторінки.

Це покаже вам просту сторінку, яка покаже вам відформатований вигляд будь-якого повідомлення, що надсилається з Node-RED у вузол. Для цього не потрібні додаткові бібліотеки або фреймворки, єдині залежності - це завантажити бібліотеку `uibuilderfe.js`, запустити бібліотеку за допомогою ` uibuilder.start() `, а потім створити прослуховувач для вхідних повідомлень.

### 2.3. Редагування ресурсних файлів

На панелі конфігурації вузла в редакторі натисніть "Edit  Source Files", щоб побачити інтерфейсний код. Внесіть деякі зміни, щоб побачити, що станеться.

Якщо вам потрібно більше місця для редактора, натисніть кнопку ⤡ під текстовим редактором. Щоб повернутися, натисніть ту саму кнопку (яка тепер виділена) або клавішу Esc.

Натисніть кнопку Save, щоб зберегти зміни, Reset щоб повернутися до збереженого файлу, Close, щоб вийти з редактора. Зверніть увагу, що кнопка закриття недоступна, поки є незавершені зміни, спочатку натисніть Save або Reset. Червона кнопка "Done" редактора також відключена, поки ще є незавершені зміни.

Ви можете створити новий файл та видалити файли та папки за допомогою відповідних кнопок. Якщо видалити один із файлів  `index.(html|css|js)` за замовчуванням і встановити прапор *Copy Index*(у розширених налаштуваннях), файл буде автоматично замінено файлом шаблону за замовчуванням. Корисно, якщо ви потрапили в повний безлад.

### 2.4. Install additional front-end libraries

Click the "Manage front-end libraries" button. Then click the + add button and type in the name of the package as it is defined in npm.

You can also remove installed libraries from here.

The uibuilder *Detailed Information* API page (link in the  configuration panel) shows details of all packages installed, their URL  for your html pages and their physical location on the server (so that  you can track down the right file to include in your HTML).

#### 2.4.a Using VueJS

If you want to use the VueJS based templates, you will need to install `vue` and `bootstrap-vue` libraries.

The included [VueJS](https://github.com/vuejs/vue#readme), [bootstrap](https://getbootstrap.com/) and [bootstrap-vue](https://bootstrap-vue.js.org/) templates make for a really easy to use initial setup that is very easy to use but powerful to build any kind of web user interface. The  template files should give you some ideas on how to use everything.

### 2.5. Additional Documentation

Check out the [WIKI](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki) for more information, help and examples.

Also check out the [technical documentation](https://totallyinformation.github.io/node-red-contrib-uibuilder) site. This is also available from within the Node-RED Editor by  selecting a uibuilder node and clicking on the link in the help sidebar  or by opening the configuration for a uibuilder node and clicking on the "Tech Docs" button.

*[back to top](https://github.com/TotallyInformation/node-red-contrib-uibuilder#contents)*

## 3. Features

- Один вузол використовується для визначення кінцевої точки (за її URL-адресою). Вузол можна включати в потоки скільки завгодно разів, але кожен екземпляр **повинен** мати унікальну назву шляху до URL-адреси.

- Кожен екземпляр вузла отримує власний простір імен (*namespace*) Socket.IO, що відповідає налаштуванню шляху URL. Зауважте, що Socket.IO ефективно розподілятиме сокети, зберігаючи трафік розділеним простором імен.

   Простір імен (namespace) - це URL-адреса uibuilder (визначена в редакторі) з попереднім "/".

- Існує інтернет-бібліотека `uibuilderfe.min.js` або ` uibuilderfe.js`, яка приховує всі складності використання Socket.IO, щоб ваш власний код FE було легко написати. Він забезпечує просту систему обробки подій, щоб ви могли підписатися на зміни та обробляти їх у міру їх виникнення. Файл `index.js` за замовчуванням містить деталі та приклади використання. Бібліотека написана так, що її можна отримати через html або включити за допомогою кроку збірки (наприклад, webpack).

Ініціалізуйте бібліотеку за допомогою:

```js
uibuilder.start()
```

Обробка вхідних повідомлень від Node-RED проста:

```js
uibuilder.onChange('msg', function(msg){
    console.info('[uibuilder.onChange] property msg changed!', msg)
})
```

Надсилання повідомлення назад до Node-RED-це просто:

```js
uibuilder.send( { 'topic': 'from-the-front', 'payload': 42 } )
```

- Пакети npm можна встановити (або видалити або оновити) за допомогою інтерфейсу адміністратора вузла в Node-RED. Це дозволяє дуже легко керувати наявністю інтернет-бібліотек. Немає необхідності мати доступ до командного рядка серверів. Будь-яка інтернет-бібліотека, доступна як пакет npm, може управлятися таким чином. Встановлені пакети стануть доступними для вашого веб -додатка.

- Зазвичай для створення простого веб-інтерфейсу, керованого даними, потрібно дуже мало коду. Модуль вузла містить файли шаблонів шаблонів html, JavaScript та CSS за замовчуванням, які копіюються у вашу локальну папку src для редагування за необхідності. Він дає вам простий шаблон, який запускає розробку вашого веб-додатка. Доступні додаткові шаблони (навіть зовнішні), які допомагають розпочати вашу розробку.

- Повідомлення, надіслані з Node-RED у ваш веб-додаток, можуть мати властивості `msg.script` та ` msg.style`, які будуть динамічно додавати цей код на веб-сторінку - якщо це дозволено налаштуваннями (за замовчуванням вимкнено).

- Включення атрибута `_socketId` у повідомлення, надіслані з Node-RED, буде надсилатись лише на цей ID .

  Зауважте, що ID пов’язаний із певною вкладкою веб-переглядача і скидається при перезавантаженні сторінки.

  Атрибут `_socketId` додається до будь-якого повідомлення, надісланого від клієнта до Node-RED. Для отримання додаткової інформації див. [WIKI](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/Sending-Messages-to-Specific-Client-Instances) 


- Другий вихідний порт дає доступ до деяких повідомлень керування.

  Це дозволяє додаткову обробку, коли клієнт підключається або відключається, екземпляр (повторно) розгортається або виникає помилка сокета.

  Поширеним використанням цього є надсилання кешованої інформації знову до знову підключеного клієнта (або того, у якого сторінка перезавантажилася).

  Інше використання може включати виведення стандартної інформації при підключенні нового клієнта. Або ви можете використовувати цю інформацію для збереження показників використання. Докладніше дивіться на сторінці  [Control Message Structure](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/Control-Message-Structure)  у WIKI.

- Після розгортання *першого* екземпляра uibuilder у вашому каталозі користувача Node-RED (зазвичай `~/.node-red`) створюється нова папка з фіксованою назвою ` uibuilder`. 

  Якщо ви використовуєте функцію проектів Node-RED, папка буде створена в середині папки вашого проекту.

  Починаючи з v4.0.0, ви можете змінити розташування цієї кореневої папки, вказавши розташування у файлі `settings.js` Node-RED.

```js
    /** Custom settings for all uibuilder node instances */
    uibuilder: {
        /** Optional uibRoot folder. 
         * By default, uibuilder will use `<userDir>/uibuilder`
         * Use this setting to change that.
         */
        uibRoot: process.env.UIBROOT || '/where/i/want/it',
    },
```

- Після розгортання будь-якого нового екземпляра створюється нова підпапка у `uibuilder`. 

  Назва така ж, як шлях до URL-адреси, вказаний у налаштуваннях екземпляра вузла. (за замовчуванням `uibuilder`). Також створюються підпапки `src` та ` dist`. Ім'я `url` може мати максимум 20 символів і не може бути ` templates`, оскільки це зарезервовано.

  Файли в цих папках можна редагувати з панелі конфігурації вузла в редакторі Node-RED. Немає необхідності доступу до командного рядка або іншого файлу на сервері.

  Якщо ви видалите вузол зі своїх потоків, Node-RED запропонує також видалити папку. Якщо ви зміните `url`, Node-RED спробує перейменувати папку.

- Якщо локальна папка `dist` містить файл ` index.html`, папка `dist` буде обслуговуватися, інакше буде подана папка ` src`. Це дозволяє запускати крок збірки (наприклад, webpack/babel). WIKI має інструкції щодо того, як зробити крок збірки.

- Any resource (html, css, js, image, etc) placed within the `dist`/`src` sub-folder is available to the browser client. The default URL would be `http://localhost:1880/uibuilder` (where the path is set as per the point above). That URL will load `index.html`. Resource URL's take the `httpNodeRoot` Node-RED setting into account.

- Будь-який ресурс (html, css, js, зображення тощо), розміщений у підпапці `dist`/` src`, доступний клієнту браузера. URL-адреса за замовчуванням буде `http://localhost:1880/uibuilder` (де шлях встановлено відповідно до точки вище). Ця URL-адреса завантажуватиме `index.html`. URL-адреси ресурсу беруть до уваги налаштування Node-RED `httpNodeRoot`. 

Додатково у кореневій папці uibuilder створюється додаткова "загальна" папка (наприклад, `~/.node-red/uibuilder/common`)

Це доступно для кожного екземпляра вузла і використовується для надання загальних ресурсів доступними для кількох веб-програм.

Перегляньте сторінку [Шляхи URI у WIKI](https://github.com/TotallyInformation/node-red-contrib-uibuilder/wiki/V2-URI-Paths) для отримання детальної інформації про всі URI, доступні для ваших веб-програм.

Ще краще, перегляньте деталі uibuilder та деталі екземпляра на панелі конфігурації uibuilder у редакторі Node-RED, вони покажуть сторінки з більш детальною інформацією.

- Ви можете використовувати окремий веб-сервер від внутрішнього веб-сервера Node-RED, вказавши порт у `settings.js`

  **Основна мета цього полягає в тому, що він дозволяє використовувати зворотний проксі-сервер, щоб безпечно відкрити *лише* кінцеві точки uibuilder, не відкриваючи сам Node-RED. ** Він також дає вам більше контролю над заголовками та іншими налаштуваннями.

  Він як і раніше буде використовувати сервер адміністратора Node-RED, але ваш власний інтерфейсний код та всі встановлені пакети постачальників та проміжне програмне забезпечення (включаючи Socket.IO) тепер використовуватимуть окремий сервер HTTP та додаток ExpressJS.

  Якщо вказати https для Node-RED, ваш користувацький сервер також буде використовувати https і автоматично збиратиме файли сертифіката та ключів з settings.js.

  **ПРИМІТКА**: *всі* екземпляри вузлів uibuilder будуть використовувати той самий веб-сервер. Дозвіл декількох серверів вимагає значних зусиль для розвитку, але знаходиться на відставанні (це дуже довгий шлях вниз).

  Щоб використовувати інший веб -сервер, потрібно додати до частини `module.exports` файлу ` settings.js`:

  ```js
    /** Custom settings for all uibuilder node instances */
    uibuilder: {
        /** Optional HTTP PORT. 
         * If set and different to Node-RED's uiPort, uibuilder will create
         * a separate webserver for its own use.
         */
        port: process.env.UIBPORT || 3000,
    },
  ```

  Зауважте, що вищенаведене дозволить вам використовувати змінну середовища під назвою `UIBPORT` для встановлення порту. Це потрібно зробити перед запуском Node-RED. Налаштування порту не є динамічним.

- Деякі допоміжні функції VueJS тепер включені до передньої бібліотеки. Ідея полягає в тому, щоб подолати розрив у складності між інформаційною панеллю Node-RED та uibuilder для початківців програмістів. Детальніше дивіться в технічній документації.

## 4. Known Issues

Це те, про що слід знати, і я хотів би якось навести порядок.

- v4.0.0 не має повністю працюючої моделі безпеки. Він не повністю перевірений і може не працювати. Не використовуйте цю деталь у виробництві. Все інше нормально.

- Деякі помічники VueJS у інтернет-бібліотеці мають крайові випадки, коли вони не працюють.

- **Socket.IO не захищений за замовчуванням** Використовуйте uibuilder ExpressJS та функцію посереднього програмного забезпечення для належного захисту, перш ніж розглядати можливість використання через Інтернет. **ЗАВЖДИ** налаштовуйте TLS перед налаштуванням автентифікації. Якщо Node-RED використовує HTTPS, Socket.IO також використовуватиме шифрування трафіку HTTPS/WSS.

  Зауважте, однак, що проміжне програмне забезпечення сокета викликається лише при початковому підключенні до сокета. Після оновлення з'єднання до websocket це більше не викликається.

  Я сподіваюся покращити це в наступному випуску.

  Ви також можете обійти це, використовуючи проксі, такий як NGINX або HAproxy, як кінцеву точку TLS. Просто переконайтеся, що ви проксите трафік websocket так само як і стандартний веб-трафік.

  Додаткову інформацію див. У документації з безпеки.

## 5. Discussions and suggestions

The best place to ask questions about uibuilder is the [Node-RED Forum](https://discourse.nodered.org/).

Alternatively, use the [GitHub issues log](https://github.com/TotallyInformation/node-red-contrib-uibuilder/issues) for raising issues or contributing suggestions and enhancements and the [GitHub Discussions page](https://github.com/TotallyInformation/node-red-contrib-uibuilder/discussions) for general questions, suggestions, etc.

Please note that I rarely have time to monitor the [#uibuilder channel](https://node-red.slack.com/messages/C7K77MG06) in Slack any more, it is best to use Discourse or raise an issue.

I do occasionally try to look out for [uibuilder related questions on Stack Overflow](https://stackoverflow.com/search?tab=newest&q=[node-red] uibuilder) but again, time does not always let me do this.

## 6. Contributing

If you would like to contribute to this node, you can contact [Totally Information via GitHub](https://github.com/TotallyInformation) or raise a request in the [GitHub issues log](https://github.com/TotallyInformation/node-red-contrib-uibuilder/issues).

Please refer to the [contributing guidelines](https://github.com/TotallyInformation/node-red-contrib-uibuilder/blob/master/.github/CONTRIBUTING.md) for more information.

## 7. Developers/Contributors

- [Julian Knight](https://github.com/TotallyInformation) - the designer and main author.
- [Colin Law](https://github.com/colinl) - many thanks for testing, corrections and pull requests.
- [Steve Rickus](https://github.com/shrickus) - many thanks for testing, corrections and contributed code.
- [Ellie Lee](https://github.com/ellieejlee) - many thanks for the PR fixing duplicate msgs.
- [Thomas Wagner](https://github.com/Thomseeen) - thanks for the steer and PR on using projects folder if active.
- [Arlena Derksen](https://github.com/boisei0) - thanks for suggestions, bug checks and Issue #59/PR #60.
- [cflurin](https://discourse.nodered.org/u/cflurin) - thanks for the cache example.
- [Scott Page - IndySoft](https://github.com/scottpageindysoft) - thanks for Issue #73/PR #74.
- [Stephen McLaughlin - Steve-Mcl](https://discourse.nodered.org/u/Steve-Mcl) - thanks for the fix for [Issue #71](https://github.com/TotallyInformation/node-red-contrib-uibuilder/issues/71) and for the enhancement idea [Issue #102](https://github.com/TotallyInformation/node-red-contrib-uibuilder/issues/102).
- [Sergio Rius](https://github.com/SergioRius) - thanks for reporting [Issue #121](https://github.com/TotallyInformation/node-red-contrib-uibuilder/issues/121) and providing [PR #122](https://github.com/TotallyInformation/node-red-contrib-uibuilder/pull/122) as a fix.
- [Thorsten von Eicken](https://github.com/tve) - thanks for providing [PR #131](https://github.com/TotallyInformation/node-red-contrib-uibuilder/pull/131) to improve CORS handling for Socket.IO.
- [Lackmann1994](https://github.com/Lackmann1994) - thanks for providing [PR #152](https://github.com/TotallyInformation/node-red-contrib-uibuilder/pull/152) to fix JWT validation.

Many other people have contributed ideas and suggestions, thanks to everyone who does, they are most welcome.