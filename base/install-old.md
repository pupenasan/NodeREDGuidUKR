| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |

**Цей розділ є частково проробленим.**

## Як встановити та запустити

[Джерело](https://nodered.org/docs/getting-started/)

Нижче наведені посилання на посібники, які допоможуть Вам встановити і запустити Node-RED всього за кілька хвилин.

Виберіть, де ви хочете запустити Node-RED, чи на своєму локальному комп’ютері, пристрої, такі як Raspberry Pi, або в хмарі, і дотримуйтесь інструкцій, наведених нижче.

|                          Платформа                           | Пояснення                                                    |
| :----------------------------------------------------------: | ------------------------------------------------------------ |
| ![](media/platform-local.png)<br />[**Локальний запуск.**](https://nodered.org/docs/getting-started/local) | Встановлення Node-RED на локальний комп'ютер                 |
| ![](media/platform-device-pi.png)<br />[**Raspberry Pi.**](https://nodered.org/docs/getting-started/raspberrypi) | Почніть використовувати наш сценарій установки "все в одному" для могутнього Raspberry Pi |
| ![](media/platform-local-docker.png)<br />[**Docker.**](https://nodered.org/docs/getting-started/docker) | Запуск Node-RED з використанням Docker                       |
| ![](media/platform-local-dev.png) <br />[**Install from git.**](https://nodered.org/docs/getting-started/development) | Компілювання Node-RED з джерельного коду. Отримайте найновіший код розробки та почніть надавати внесок. |
| ![](media/platform-device.png)<br />[**BeagleBone Boards.**](https://nodered.org/docs/getting-started/beaglebone) | Запуск Node-RED на платах BeagleBone                         |
| ![](media/platform-android.png)<br />[**Android.**](https://nodered.org/docs/getting-started/android) | Трохи експериментально, але ви можете працювати на пристроях Android за допомогою Termux. |
| ![](media/platform-cloud.png)<br />[**IBM Cloud.**](https://nodered.org/docs/getting-started/ibmcloud) | Розгортання Node-RED з каталогу IBM Cloud за пару кліків     |
| ![](media/platform-cloud.png)<br />[**AWS.**](https://nodered.org/docs/getting-started/aws) | Почніть працювати на Elastic Beanstalk або EC2               |
| ![](media/platform-cloud.png)<br />[**Microsoft Azure.**](https://nodered.org/docs/getting-started/azure) | Запуск у екземплярі віртуальної машини Azure                 |



----

## Встановлення та запуск на локальній машині

[Джерело](https://nodered.org/docs/getting-started/local#running) 

### Вимоги

Для встановлення Node-RED локально на ПК Ви повинні встановити [пітримувану версію Node.js](https://nodered.org/docs/faq/node-versions).

### Встановлення з npm

Щоб встановити Node-RED, ви можете скористатися командою `npm`, що постачається з node.js:

```bash
sudo npm install -g --unsafe-perm node-red
```

Якщо ви використовуєте Windows, не запускайте команду з `sudo`. Більше інформації про встановлення Node-RED на Windows можна знайти [нижче](#встановлення-та-запуск-на-windows).

Більше інформації про встановлення Node-RED на Raspberry PI можна знайти [нижче](#встановлення-та-запуск-на-raspberry-pi).

Ця команда встановить Node-RED як глобальний модуль разом із залежностями.

Ви можете підтвердити, що це вдалося, якщо кінець виводу команди виглядає аналогічно наступному:

```bash
+ node-red@1.1.0
added 332 packages from 341 contributors in 18.494s
found 0 vulnerabilities
```

### Running

Після встановлення як глобальний модуль ви можете використовувати команду `node-red`, щоб запустити Node-RED у своєму терміналі. Ви можете використовувати `Ctrl-C` або закрити вікно терміналу, щоб зупинити Node-RED.

Якщо Node-RED інстальовано як глобальний пакунок npm, можна просто використати команду `node-red`:

```bash
$ node-red

Welcome to Node-RED
===================

30 Jun 23:43:39 - [info] Node-RED version: v1.1.0
30 Jun 23:43:39 - [info] Node.js  version: v10.21.0
30 Jun 23:43:39 - [info] Darwin 18.7.0 x64 LE
30 Jun 23:43:39 - [info] Loading palette nodes
30 Jun 23:43:44 - [warn] rpi-gpio : Raspberry Pi specific node set inactive
30 Jun 23:43:44 - [info] Settings file  : /Users/nol/.node-red/settings.js
30 Jun 23:43:44 - [info] HTTP Static    : /Users/nol/node-red/web
30 Jun 23:43:44 - [info] Context store  : 'default' [module=localfilesystem]
30 Jun 23:43:44 - [info] User directory : /Users/nol/.node-red
30 Jun 23:43:44 - [warn] Projects disabled : set editorTheme.projects.enabled=true to enable
30 Jun 23:43:44 - [info] Creating new flows file : flows_noltop.json
30 Jun 23:43:44 - [info] Starting flows
30 Jun 23:43:44 - [info] Started flows
30 Jun 23:43:44 - [info] Server now running at http://127.0.0.1:1880/red/
```

Далі доступ до редактору Node-RED відбувається через браузер http://localhost:1880.

Вихід з журналу надає вам різні відомості:

- Версії Node-RED та Node.js
- Будь-які помилки, які виникають при спробі завантаження вузлів палітри
- Розташування вашого файла налаштувань та каталогу користувачів
- Назва файлу потоків, який він використовує.

Node-RED використовує ``flows_<hostname>.json` як файл потоків за замовчуванням. Ви можете змінити це, надавши ім'я файлу потоку як аргумент команді `node-red` [command](https://nodered.org/docs/getting-started/local#command-line-usage).

### Використання командного рядку

Node-RED може запускатися з використанням команди `node-red`. Ця команда може приймати кілька аргументів:

```bash
node-red [-v] [-?] [--settings settings.js] [--userDir DIR]
         [--port PORT] [--title TITLE] [--safe] [flows.json|projectName]
         [-D X=Y|@file]
```

| Опція                    | Опис                                                         |
| ------------------------ | ------------------------------------------------------------ |
| `-p`, `--port PORT`      | виставляє TCP port який прослуховує середовище виконання. За замовченням: `1880` |
| `--safe`                 | Запускає Node-RED без запуску потоків. Це дозволяє відкривати потоки в редакторі та вносити зміни без запущених потоків. Після розгортання змін потоки запускаються. |
| `-s`, `--settings FILE`  | Використовувати вказаний файл налаштувань. За замовченням  `settings.js` в `userDir` |
| `--title TITLE`          | Встановити назву вікна процесу                               |
| `-u`, `--userDir DIR`    | Встановлює користувацький каталог користувача. За замовчуванням: `~/.node-red` |
| `-v`                     | активувати детальне ведення журналу                          |
| `-D X=Y|@file`           | [Override individual settings](https://nodered.org/docs/getting-started/local#override-individual-settings) |
| `-?`, `--help`           | показати помічник                                            |
| `flows.json|projectName` | Якщо функція Projects не включена, це встановлює файл потоку, з яким потрібно працювати. Якщо функція Projects включена, це означує, який проект слід відкрити. |

Node-RED використовує `flows_<hostname>.json` як файл потоків за замовчуванням. Якщо комп'ютер, на якому ви працюєте, може змінити ім'я хоста, тоді вам слід переконатися, що ви надаєте статичне ім'я файлу; або як аргумент командного рядка, або використовуючи параметр `flowFile` у вашому [файлі  налаштувань](https://nodered.org/docs/user-guide/runtime/settings-file).

#### Перезаписування індивідуальних налаштувань

*Починаючи з Node-RED 1.1.0*

Ви можете змінити окремі налаштування в командному рядку, використовуючи опцію `-D` (або ` --define`).

Наприклад, для зміни рівня реєстрації ви можете використовувати:

```
-D logging.console.level=trace
```

Ви також можете надати власні налаштування у вигляді файлу:

```
-D @./custom-settings.txt
```

Файл повинен містити перелік параметрів, які слід перекрити:

```
logging.console.level=trace
logging.console.audit=true
```

#### Передача аргументів до базового процесу Node.js 

Бувають випадки, коли потрібно передавати аргументи до базового процесу Node.js. Наприклад, під час роботи на таких пристроях, як Raspberry Pi або BeagleBone Black, які мають обмежений об'єм пам'яті.

Для цього потрібно використовувати сценарій запуску `node-red-pi` замість ` node-red`. *Примітка*: цей сценарій недоступний у Windows.

Крім того, якщо запускається Node-RED за допомогою команди `node`, ви повинні надати аргументи для процесу Node.js перед тим, як вказати ` red.js` та аргументи, які ви хочете передати самому Node-RED.

Наступні дві команди показують ці два підходи:

```bash
node-red-pi --max-old-space-size=128 --userDir /home/user/node-red-data/
node --max-old-space-size=128 red.js --userDir /home/user/node-red-data/
```

### Оновлення Node-RED  

Якщо ви встановили Node-RED за допомогою сценарію Pi, ви можете повторно його оновити. Сценарій доступний [тут](https://nodered.org/docs/hardware/raspberrypi).

Якщо ви встановили Node-RED як глобальний пакет npm, ви можете оновити до останньої версії за допомогою наступної команди:

```bash
sudo npm install -g --unsafe-perm node-red
```

Якщо Ви використовуєте Windows, не вказуйте слово `sudo`.

## Встановлення та запуск на Windows

[Джерело](https://nodered.org/docs/getting-started/windows)

Нижче наведено конкретні вказівки щодо налаштування Node-RED в середовищі Microsoft Windows. Інструкції стосуються Windows 10, але також повинні працювати для Windows 7 та Windows Server з 2008R2. Не рекомендується використовувати версії до Windows 7 або Windows Server 2008R2 через відсутність поточної підтримки.

*Примітка*: Деякі з наступних інструкцій згадують "командний рядок". Там, де це використовується, воно стосується або Windows cmd, або термінальних оболонок PowerShell. [Рекомендується використовувати PowerShell](https://support.microsoft.com/en-us/help/4027690/windows-powershell-is-replacing-command-prompt) у всіх новіших версіях Windows, оскільки це надає вам доступ до команд та імен папок, ближчих до тих, що мають Linux/Mac.

### Швидкий старт

#### 1. Встановіть Node.js

Завантажте останню версію 12.x LTS Node.js з офіційної [домашньої сторінки Node.js](https://nodejs.org/uk/). Він запропонує вам найкращу версію для вашої системи.

Запустіть завантажений файл MSI. Для встановлення Node.js потрібні права місцевого адміністратора; якщо ви не місцевий адміністратор, вам буде запропоновано встановити пароль адміністратора при встановленні. Приймайте за замовчуванням при установці. Після завершення інсталяції закрийте будь-які відкриті командні підказки та відкрийте їх знову, щоб переконатися у тому, що нові змінні середовища прийняті.

Після встановлення відкрийте командний рядок і запустіть наступну команду, щоб переконатися, що Node.js і npm встановлені правильно.

З Powershell: `node --version; npm --version`

З cmd: `node --version && npm --version`

Ви повинні отримати відповідь, схожу на:

```
v12.15.0
6.14.5
```

#### 2. Встановлення Node-RED

Встановлення Node-RED як глобальний модуль додає команду `node-red` до вашого системного шляху. Виконайте наступне в командному рядку:

```bash
npm install -g --unsafe-perm node-red
```

#### 3. Run Node-RED

Як тільки встановлено, можна [запускати Node-RED](#запуск-на-windows).

------

### Альтернативне встановлення на Windows

ToDo

In this section, we provide you with information on alternative ways  to install Node.js, npm and the Windows Build Tools needed to install  some Nodes for Node-RED on Windows.

*Note* : You should *not* use an administrative (a.k.a.  "elevated") command prompt unless specifically instructed to. You will  very likely need to be quite familiar with command prompts as you learn  about Node-RED and Node.js and it will be worth while reading some of  the [Microsoft articles on PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/getting-started/fundamental/using-windows-powershell). the [PowerShell Tutorial](http://powershelltutorial.net/) and [PowerShell One-Liners](https://www.red-gate.com/simple-talk/sysadmin/powershell/powershell-one-liners-help,-syntax,-display-and--files/) sites may also be helpful.

Standard installations of Node.js on Windows require local  administrator rights. Download the appropriate version from the official [Node.js home page](https://nodejs.org/en/). It will offer  you the best version. While you can use either 32 bit or 64 bit versions on 64 bit Windows, it is recommended to use the 64bit version of Node.  If for some reason, you need a different installation, you can use the [Downloads Page](https://nodejs.org/en/download/).

There are two potentially useful alternatives to installing Node.js with the MSI installer.

1. Using the Chocolatey package manager

   [Chocolatey](https://chocolatey.org/) is a package  manager for Windows similar to APT or yum on Linux and brew on the  Macintosh platforms. If you are already using Chocolatey, you may want  to use this tool to install Node.js (e.g. using the `nodejs-lts` package).  Note however, that many packages have uncertain management  and that these packages may use different folder locations than those  mentioned above.

2. Using a Node version manager

   Using a Node.js version manager such as [nvm-windows](https://github.com/coreybutler/nvm-windows) can be very helpful if you are doing Node.js development and need to  test against different versions. Keep in mind that you will need to  reinstall global packages and may need to re-install local packages when when you switch the version of Node you are using.

*Note* : Microsoft maintain a parallel version of Node that uses  the Microsoft Chakra Core JavaScript engine instead of V8. This is not  recommended for Node-RED as it has not been tested.

#### npm on Windows

When you install Node.js, you are also installing the npm package  manager. You may see some instructions on the web that recommend  installing later releases of npm than the one that comes with the  Node.js release.  This is **not** recommended as it is too  easy to later end up with an incompatible version. Node.js releases are  very regular and that is sufficient to keep npm updated.

Встановлюючи Node.js, ви також встановлюєте менеджер пакунків npm. Ви можете побачити в Інтернеті кілька інструкцій, які рекомендують встановлювати пізніші випуски npm, ніж ті, що постачаються з випуском Node.js. Це **не** рекомендується, тому що згодом занадто легко закінчитись несумісною версією. Випуски Node.js є дуже регулярними, і цього достатньо, щоб npm оновлювався.

#### Sharing Node-RED between Users

ToDo

Node.js is installed into the `Program Files` folder as you would expect. However, if you install a global *package* like Node-RED using `npm -g`, it is installed into the `$env:APPDATA\npm` folder (`%APPDATA%\npm` using cmd) for the **current** user.  This is less than helpful if you are installing on a PC with  multiple user logins or on a server and installing using an admin login  rather than the login of the user that will run Node applications like  Node-RED.

*Note* : To see what a folder name like `%APPDATA%`  translates to, you can simply type it into the address bar of the  Windows File Explorer. Alternatively, in PowerShell, type the command `cd $Env:APPDATA`(`cd %APPDATA%` using cmd).

To fix this, either give permissions to the folder to other users and make sure that the folder is included in their `path` user environment variable.

Alternatively, change the global file location to somewhere  accessible by other users. Make sure that you use the user that will be  running Node-RED to make these changes.  For example, to change the  location to `$env:ALLUSERSPROFILE\npmglobal` using PowerShell:

```
mkdir $env:ALLUSERSPROFILE\npmglobal
npm config set prefix $env:ALLUSERSPROFILE\npmglobal
```

You will then want to change the npm cache folder as well:

```
mkdir $env:ALLUSERSPROFILE\npmglobal-cache
npm config set cache $env:ALLUSERSPROFILE\npmglobal-cache --global
```

If using the above changes, you can add the new *prefix* folder to the *PATH* System variable and remove the old folder from the user’s Path variable.  To change the PATH Environment variable, type `environment` into the start menu or Cortana and choose *Edit Environment Variables*.

For each of the users running Node-RED, check that the above settings for the other users are correct.

#### Installing Node.js Windows Build Tools

ToDo

Many Node.js modules used by Node-RED or installed nodes have binary  components that will need compiling before they will work on Windows. To enable npm to compile binaries on the Windows platform, install the  windows-build-tools module using the [command prompt as an Administrator](https://technet.microsoft.com/en-gb/library/cc947813(v=ws.10).aspx):

```
npm install --global --production windows-build-tools
```

If you wish to have the built-in Python v2.7 install exposed for use, use the command:

```
npm install --global --production --add-python-to-path windows-build-tools
```

*Notes*:

- Not all Node.js modules will work under Windows, check the install output carefully for any errors.
- During the install some errors may be reported by the `node-gyp` command. These are typically *non-fatal* errors and are related to optional dependencies that require a compiler in order to build them. **Node-RED will work without these optional dependencies**. If you get fatal errors, first check that you installed the `windows-build-tools` module and that you have closed and opened your command prompt window.

### Запуск на Windows

Після встановлення найпростіший спосіб запустити Node-RED - використовувати команду `node-red` у командному рядку: Якщо ви встановили Node-RED як глобальний пакет npm, ви можете використовувати команду node-red:

```
node-red
```

Це виведе журнал Node-RED до терміналу. Ви повинні тримати термінал відкритим для того, щоб Node-RED працював.

Зауважте, що запуск Node-RED створить нову папку у вашій папці  `%HOMEPATH%` під назвою ` .node-red`. Це ваша папка `userDir`, розгляньте це як домашню папку для конфігурації Node-RED для поточного користувача. Ви часто будете бачити це в документації як `~/.node-red`. Символ  `~` - це скорочення до домашньої папки користувача в Unix-подібних системах. Ви можете використовувати таке саме посилання, якщо використовуєте PowerShell в якості командного рядка, як це рекомендовано. Якщо ви використовуєте більш стару оболонку `cmd`, це не працюватиме.

Тепер Ви можете створити [перший потік](https://nodered.org/docs/tutorials/first-flow).

#### Використання PM2

Якщо ви використовуєте Windows для розробки потоків або вузлів NED-RED, вам може бути корисно використовувати [PM2](http://pm2.keymetrics.io/) для запуску Node-RED. Це може бути налаштовано для автоматичного перезавантаження при зміні файлів, завжди тримати Node-RED у режимі запуску та керувати виведенням журналу.

#### Запуск Node-RED при запуску

Якщо ви хочете використовувати Windows як виробничу платформу для Node-RED, вам доведеться налаштувати завдання планувальника завдань Windows. Робити так:

1. Перейдіть до меню "Пуск" і введіть "планувальник завдан" і натисніть на результат.
2. Клацніть на «Створити завдання…» у меню праворуч. Виконайте кроки, щоб створити нове завдання.

Переконайтеся, що ви використовуєте логін користувача, який ви використовували для налаштування та виконували початковий запуск Node-RED. Ви можете використовувати тригер "При запуску", щоб завжди запускати Node-RED при запуску системи. Скористайтеся дією "Запустіть програму" з деталями, встановленими на  `C:\Users\<user>\AppData\Roaming\npm\node-red.cmd` (замінивши `<user>` фактичним іменем користувача).

Ви можете переконатися, що він запускається лише за наявності мережі. Ви також можете перезапустити, якщо завдання не вдалося. Можливо, перезапускайте щохвилини, але лише 3 рази - якщо воно не розпочнеться до цього часу, помилка є фатальною і потребує іншого втручання. Ви можете перевірити несправності, заглянувши в журнал подій. Якщо ви хочете отримати доступ до журналів під час запуску таким чином, вам слід внести зміни до файлу node-red.cmd, щоб перенаправити std та виводи помилок у файл (створення альтернативного файлу запуску було б краще, щоб він не був перезаписаний оновленнями).

## Встановлення та запуск на Raspberry Pi

[Джерело](https://nodered.org/docs/getting-started/raspberrypi)

### Вимоги

Якщо ви використовуєте Raspbian, тоді ви повинні мати Raspbian Jessie як мінімальну версію. Raspbian Buster - це поточно підтримувана версія.

### Встановлення та оновлення Node-RED

Ми надаємо сценарій для встановлення Node.js, npm та Node-RED на Raspberry Pi. Сценарій також може бути використаний для оновлення наявної інсталяції, коли є новий випуск.

Виконавши таку команду, ви завантажите та запустите скрипт. Якщо ви хочете спочатку переглянути вміст сценарію, ви можете його переглянути  [тут](https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered).

```bash
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
```

Цей сценарій буде працювати в будь-якій **ОС Debian**, включаючи **Ubuntu** та **Diet-Pi**. Вам може знадобитися спочатку запустити `sudo apt install build-basic git`, щоб переконатися, що npm зможе створити будь-які бінарні модулі, які потрібно встановити.

Цей сценарій:

- видаліть попередньо упаковану версію Node-RED та Node.js, якщо вони є
- встановити поточний реліз Lode.js LTS за допомогою [NodeSource](https://github.com/nodesource/distributions/blob/master/README.md). Якщо він виявить, що Node.js вже встановлений з NodeSource, він забезпечить принаймні Node 8, але в іншому випадку залиште його в спокої
- встановити останню версію Node-RED за допомогою npm
- опціонально можна встановити набір корисних вузлів, специфічних для Pi
- налаштовує Node-RED для запуску як служби та надання набору команд для роботи зі службою

Node-RED також упакований для сховищ Raspbian і відображається у їхньому списку "Рекомендованого програмного забезпечення". Це дозволяє встановити його за допомогою `apt-get install nodered` і включає в себе пакунок Raspbian версію Node.js, але *не включає* `npm`.

Хоча використання цих пакунків зручно спочатку, ми **настійно рекомендуємо** використовувати замість цього наш сценарій встановлення.

### Локальний запуск

Як і у випадку локального запуску Node-RED що наведено вище, Ви можете використовувати команду `node-red` для запуску Node-RED в терміналі. Потім його можна зупинити натисканням клавіші `Ctrl-C` або закриттям вікна терміналу.

Через обмежену пам’ять Raspberry Pi, вам потрібно буде запустити Node-RED з додатковим аргументом, щоб повідомити базовий процес Node.js звільнити невикористану пам'ять раніше, ніж це було б інакше.

Для цього слід використовувати альтернативну команду `node-red-pi` та передати аргумент `max-old-space-size`.

```bash
node-red-pi --max-old-space-size=256
```

### Запуск як служби

Сценарій установки для Pi також налаштовує його на запуск як служби. Це означає, що він може працювати у фоновому режимі та бути включеним для автоматичного запуску під час завантаження.

Для роботи зі службою надаються наступні команди:

- `node-red-start` -- це запускає службу Node-RED та відображає її вихідний журнал. Натискання `Ctrl-C` або закривання вікна *НЕ* зупиняє службу; вона буде залишатися запущеною на задньому фоні 
- `node-red-stop` - зупиняє службу Node-RED 
- `node-red-restart` - зупиняє і перезапускає службу Node-RED 
- `node-red-log` - тут відображається вихід журналу служби

Ви також можете запустити службу Node-RED на робочому столі Raspbian, вибравши опцію `Menu -> Programming -> Node-RED`.

### Автостарт при запуску

Якщо ви хочете, щоб Node-RED запускався, коли Pi включається або перезавантажується, ви можете включити службу до автоматичної запуску, виконавши команду:

```bash
sudo systemctl enable nodered.service
```

Для відключення автозапуску служби треба виконати командк:

```bash
sudo systemctl disable nodered.service
```

### Відкриття редактору

Після запуску Node-RED ви можете отримати доступ до редактора у веб-переглядачі.

Якщо ви використовуєте браузер на робочому столі Pi, ви можете відкрити адресу: http://localhost:1880.

Ми рекомендуємо використовувати браузер поза PI і вказувати його на Node-RED, що працює на Pi. Однак ви можете використовувати вбудований браузер, і якщо так, ми рекомендуємо Chromium або Firefox-ESR але *НЕ* Epiphany

Під час перегляду з іншої машини слід використовувати ім'я хоста або IP-адресу Pi: `http://<hostname>:1880`. Ви можете знайти IP-адресу, запустивши  `hostname -I` на Pi.



---

## Стара версія

## Інсталяція та запуск

До початку інсталяції Node-RED, у вас повинен бути встановлений Node.js. Ми радимо встановлювати Node.js версій **LTS 8.x** **або 10.x**. Node-RED не підтримує Node.js **6.x** або більш ранні версії.

​      Інструкції зі встановлення на різних платформах і ОС:

- [Raspberry Pi](https://nodered.org/docs/hardware/raspberrypi)
- [BeagleBone Black](https://nodered.org/docs/hardware/beagleboneblack)
- [Windows](https://nodered.org/docs/platforms/windows)

Користувачі Linux та OS X мають встановити [запаковану версію](https://nodejs.org/en/download/package-manager/) **для своєї конкретної ОС, або завантажити останню Версію Довгострокової Підтримки (**Long Term Support (LTS)) із [сайту](https://nodejs.org/en/download/).

Команда щоб перевірити свою версію Node.js

```
node -v
```

Інші варіанти ОС доступні [тут](https://nodejs.org/dist/latest-v8.x/).

Найпростіший спосіб встановлення Node-RED – використання менеджера (npm), що йде у складі Node.js. Інсталяція його, як глобального модуля, додає команду `node-red у ваш системний шлях:`

```bash
sudo npm install -g --unsafe-perm node-red
```

Примітка: sudo потрібна лише під час інсталяції на Linux або OS X. При роботі з Windows, див. [інструкції з інсталяції з Windows](https://nodered.org/docs/platforms/windows).

Після завершення інсталяції ви готові [запустити Node-RED](https://nodered.org/docs/getting-started/running).

### Альтернативний метод інсталяції

#### Завантажити останню версію

Ви можете завантажити останню версію [звідси](https://github.com/node-red/node-red/releases/latest). Zip-файл містить кореневий каталог під назвою формату `node-red-X.Y.Z` де `X.Y.Z` – номер версії. Після розпаковки, із кореневого каталога, виконайте команду:

```
npm install --production
```



#### Запуск з локально інстальованого Linux та Mac OS X

До команди `node-red`  все ще можна отримати доступ, навіть якщо Node-RED не був встановлений як глобальний пакет npm.

Якщо у вас встановлено в npm Node-RED, цей скрипт буде  `node_modules/node-red/bin/node-red`, по відношенню до каталогу, в якому ви запустили ` npm install`. Якщо ви встановили версію з zip-файлу, скрипт буде`node-red-X.Y.Z/bin/node-red`, по відношенню до каталогу, в який було розгортання.

Спершу зробіть сценарій запуску `node-red`:

```
chmod +x <node-red-install-directory>/bin/node-red
```

Тоді ви можете запустити Node-RED за допомогою:

```
<node-red-install-directory>/bin/node-red
```

#### Запуск з локально інстальованого Windows

У Windows запустіть таку команду з того самого каталогу, в якому ви запустили `npm install ', або розпакували zip-файл:

```
node node_modules/node-red/red.js
```

#### Збереження користувацьких даних 

За замовчуванням Node-RED зберігає ваші дані в каталозі `$HOME/.node-red`. З міркувань зворотної сумісності, якщо Node-RED виявляє дані користувачів у своєму каталозі встановлення, він використовуватиме їх замість цього. Документація [upgrading](https://nodered.org/docs/getting-started/upgrading)  включає в себе розділ про переміщення даних із каталогу встановлення Node-RED.

Щоб замінити, який каталог використовувати, можна використовувати командний рядок `--userDir`.

### Запуск Node-RED при старті ОС

Існує багато методів запуску, зупинки та моніторингу програм під час завантаження. Користувачам Raspberry Pi *сильно* рекомендується дотримуватися [цих інструкцій](https://nodered.org/docs/hardware/raspberrypi).

Linux users that have a Debian flavour (e.g. Ubuntu, Mint, Debian, etc) are recommended to use the [Adding Autostart capability using SystemD](https://nodered.org/docs/hardware/raspberrypi#adding-autostart-capability-using-systemd) instructions from the Raspberry Pi docs though you will need to edit the downloaded `/lib/systemd/system/nodered.service` file to suit your *user id* and environment.

Користувачам Debian (наприклад, Ubuntu, Mint, Debian тощо), рекомендується використовувати [Додавання можливості автозапуску за допомогою SystemD](https://nodered.org/docs/hardware/raspberrypi#adding-autostart-capability-using-systemd) інструкцій з документів Raspberry Pi, хоча вам потрібно буде відредагувати завантажений файл `/lib/systemd/system/nodered.service` відповідно до вашого *користувача id* та оточення.

The guide below sets out what we believe to be the most straight-forward for the majority of users. For Windows, PM2 does not autorun as a service - you may prefer the [NSSM option](https://nodered.org/docs/getting-started/running#alternative-options) below.

#### Using PM2

[PM2](https://github.com/Unitech/pm2) is a process manager for Node.js. It makes it easy to run applications on boot and ensure they are restarted if necessary.

*Note* : PM2 is released under GNU-AGPL-3.0 license - please check the terms of the license before deploying.

##### 1. Install PM2

```
sudo npm install -g pm2
```

*Note* : `sudo` is required if running as a non-root user on Linux or OS X. If running on Windows, you will need to run in a [command shell as Administrator](https://technet.microsoft.com/en-gb/library/cc947813(v=ws.10).aspx), without the `sudo` command. 

If running on Windows, you should also ensure `tail.exe` is on your path, as described [here](https://github.com/Unitech/PM2/blob/development/ADVANCED_README.md#windows).

##### 2. Determine the exact location of the `node-red` command.

If you have done a global install of node-red, then on Linux/OS X the `node-red` command will probably be either: `/usr/bin/node-red` or `/usr/local/bin/node-red`. The command `which node-red` can be used to confirm the location.

If you have done a local install, it will be `node_modules/node-red/bin/node-red`, relative to where you ran `npm install` from.

##### 3. Tell PM2 to run Node-RED

The following command tells PM2 to run Node-RED, assuming `/usr/bin/node-red` as the location of the `node-red` command.

The `--` argument must appear before any arguments you want to pass to node-red.

```
pm2 start /usr/bin/node-red -- -v
```

*Note* : if you are running on a device like the Raspberry Pi or BeagleBone Black that have a constrained amount of memory, you must pass an additional argument: 

```
pm2 start /usr/bin/node-red --node-args="--max-old-space-size=128" -- -v
```

*Note* : if you want to run as the root user, you must use the `--userDir` option to specify where Node-RED should store your data. 

This will start Node-RED in the background. You can view information about the process and access the log output using the commands:

```
pm2 info node-red
pm2 logs node-red
```

More information about managing processes under PM2 is available [here](https://github.com/Unitech/pm2#process-management).

##### 4. Tell PM2 to run on boot

PM2 is able to generate and configure a startup script suitable for the platform it is being run on.

Run these commands and follow the instructions it provides:

```
pm2 save
pm2 startup
```

for newer Linux systems that use **systemd** use

```
pm2 startup systemd
```

*Temporary Note:* There's an [open issue](https://github.com/Unitech/PM2/issues/1321) on PM2 on GitHub which highlights an issue that has been introduced recently. Linux users need to manually edit the generated `/etc/init.d/pm2-init.sh` file and replace 

```
export PM2_HOME="/root/.pm2"
```

to point at the correct directory, which would be like: 

```
export PM2_HOME="/home/{youruser}/.pm2"
```

##### 5. Reboot

Finally, reboot and check everything starts as expected.

#### Alternative options

There are many alternative approaches. The following are some of those created by members of the community.

- [A      systemd script (used by the Pi pre-install)](https://raw.githubusercontent.com/node-red/raspbian-deb-package/master/resources/nodered.service) by @NodeRED (linux)
- [A systemd      script](https://gist.github.com/Belphemur/3f6d3bf211b0e8a18d93) by Belphemur (linux)
- [An init.d script](https://gist.github.com/bigmonkeyboy/9962293)     by dceejay (linux)
- [An init.d      script](https://gist.github.com/Belphemur/cf91100f81f2b37b3e94) by Belphemur (linux)
- [A Launchd script](https://gist.github.com/natcl/4688162920f368707613)     by natcl (OS X)
- [Running as a      Windows service using NSSM](https://gist.github.com/dceejay/576b4847f0a17dc066db) by dceejay
- [Running      as Windows/OS X service](http://www.hardill.me.uk/wordpress/2014/05/30/running-node-red-as-a-windows-or-osx-service/) by Ben Hardill



## Добавлення вузлів ([Adding Nodes](https://nodered.org/docs/getting-started/adding-nodes))

Node-RED поставляється з основним набором корисних вузлів, але є ще багато доступних як для проекту Node-RED, так і для широкої спільноти. Ви можете шукати доступні вузли в [Node-RED library](http://flows.nodered.org).

### Використовуючи редактор

Ви можете встановити вузли безпосередньо в редакторі, вибравши в головному меню опцію  `Manage Palette` ([Palette Manager](https://nodered.org/docs/user-guide/editor/palette/manager)). На вкладці "Nodes" перераховані всі встановлені модулі. Він показує, що ви використовуєте та чи доступні оновлення для будь-якого з них. На вкладці «Install» ви можете шукати каталог доступних модулів вузлів та встановлювати їх.

### Встановлення з npm

To install a node module from the command-line, you can use the following command from within your user data directory (by default, `$HOME/.node-red`):

```
npm install <npm-package-name>
```

You will then need to restart Node-RED for it to pick-up the new nodes.

Recent versions of `npm` will automatically add the module to the dependencies section of the `package.json` file in your user directory.

### Встановлення індивідуальних файлів вузлів 

Під час розробки також можна встановити вузли, скопіювавши їхні файли `.js` та` .html` у каталог `nodes` у вашому каталозі даних користувачів. Якщо ці вузли мають будь-які npm-залежності, вони також повинні бути встановлені в каталозі даних користувачів. Це рекомендується тільки для цілей розробки.

### Оновлення вузлів 

Найпростіший спосіб перевірити наявність оновлень вузлів - це відкрити [Palette Manager](https://nodered.org/docs/user-guide/editor/palette/manager) у редакторі. Потім ви можете застосувати ці оновлення за потребою.

Ви також можете перевірити наявність оновлень з командного рядка, використовуючи `npm`. У вашому каталозі користувача `~/.node-red` виконайте команду:

```
npm outdated
```

Це дозволить виділити будь-які модулі, у яких доступні оновлення. Щоб встановити останню версію будь-якого модуля, запустіть команду:

```
npm install <name-of-module>
```

Whichever approach you take, you will need to restart Node-RED to load the updates.

*Note* : the reason for using the `--unsafe-perm` option is that when node-gyp tries to recompile any native libraries it tries to do so as a "nobody" user and then fails to get access to certain directories. This causes the nodes in question (for example, serialport) not to be installed. Allowing it root access during install allows the nodes to be installed correctly during the upgrade.

## Оновлення версії Node-RED ([Upgrading](https://nodered.org/docs/getting-started/upgrading))

Якщо ви встановили Node-RED як глобальний пакет npm, ви можете оновити до останньої версії за допомогою наступної команди:

```bash
sudo npm install -g --unsafe-perm node-red
```

Якщо ви використовуєте Windows, запускайте команду без `sudo`

## Створення першого потоку ([Creating your first flow](https://nodered.org/docs/getting-started/first-flow))

To Do

 

## Створення другого потоку([Creating your second flow](https://nodered.org/docs/getting-started/second-flow))

To Do

 

## Запуск на Docker ([Running under Docker](https://nodered.org/docs/platforms/docker))

To Do

 

## Запуск на Windows ([Running on Windows](https://nodered.org/docs/platforms/windows))

To Do

 

 

## Конфігурування [(Configuration)](https://nodered.org/docs/configuration)

To Do

| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |