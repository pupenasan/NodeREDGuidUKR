| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |

**Цей розділ є частково проробленим.**

## Інсталяція та запуск ([Installation](https://nodered.org/docs/getting-started/installation))

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

Інші варіанти доступні [тут](https://nodejs.org/dist/latest-v8.x/).

Найпростіший спосіб встановлення Node-RED – використання менеджера (npm), що йде у складі Node.js. Інсталяція його, як глобального модуля, додає команду `node-red у ваш системний шлях:`

```
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

## Запуск ([Running](https://nodered.org/docs/getting-started/running)) 

To Do

If you have installed Node-RED as a global npm package, you can use the `node-red` command:

```
$ node-red
 
Welcome to Node-RED
===================
 
25 Mar 22:51:09 - [info] Node-RED version: v0.18.4
25 Mar 22:51:09 - [info] Node.js  version: v8.11.1
25 Mar 22:51:09 - [info] Loading palette nodes
25 Mar 22:51:10 - [warn] ------------------------------------------
25 Mar 22:51:10 - [warn] [rpi-gpio] Info : Ignoring Raspberry Pi specific node
25 Mar 22:51:10 - [warn] ------------------------------------------
25 Mar 22:51:10 - [info] Settings file  : /home/nol/.node-red/settings.js
25 Mar 22:51:10 - [info] User Directory : /home/nol/.node-red
25 Mar 22:51:10 - [info] Server now running at http://127.0.0.1:1880/
25 Mar 22:51:10 - [info] Creating new flows file : flows_noltop.json
25 Mar 22:51:10 - [info] Starting flows
25 Mar 22:51:10 - [info] Started flows
```

You can then access the Node-RED editor by pointing your browser at http://localhost:1880.

There are specific instructions available for certain hardware platforms:

- [Raspberry Pi](https://nodered.org/docs/hardware/raspberrypi)
- [BeagleBone Black](https://nodered.org/docs/hardware/beagleboneblack)

### Command-line usage

```
Usage: node-red [-v] [-?] [--settings settings.js] [--userDir DIR] [flows.json]
 
Options:
  -s, --settings FILE  використовувати вказаний файл налаштувань 
  -u, --userDir  DIR   використовувати вказану користувацьку директорію
  -v                   активувати детальне ведення журналу
  -?, --help           показати помічник
```



#### Running from a local install - Linux & Mac OS X

The `node-red` command can still be accessed even if Node-RED hasn’t been installed as a global npm package.

If you have npm installed Node-RED, this script will be `node_modules/node-red/bin/node-red`, relative to the directory you ran `npm install` in. If you have installed from a release zip file, the script will be `node-red-X.Y.Z/bin/node-red`, relative to the directory you extracted the zip into.

First make the `node-red` start script executable:

```
chmod +x <node-red-install-directory>/bin/node-red
```

Then you can start Node-RED with:

```
<node-red-install-directory>/bin/node-red
```

#### Running from a local install - Windows

On Windows, run the following command from the same directory you ran `npm install` in, or that you extracted the release zip file:

```
node node_modules/node-red/red.js
```

#### Storing user data

By default, Node-RED stores your data in the directory `$HOME/.node-red`. For backwards compatibility reasons, if Node-RED detects user data in its install directory, it will use that instead. The [upgrading](https://nodered.org/docs/getting-started/upgrading) documentation includes a section on migrating your data out of the Node-RED install directory.

To override what directory to use, the `--userDir` command-line option can be used.

#### Passing arguments to the underlying Node.js process

There are occasions when it is necessary to pass arguments to the underlying Node.js process. For example, when running on devices like the Raspberry Pi or BeagleBone Black that have a constrained amount of memory.

To do this, you must use the `node-red-pi` start script in place of `node-red`. *Note*: this script is not available on Windows.

Alternatively, if are running Node-RED using the `node` command, you must provide arguments for the node process before specifying `red.js` and the arguments you want passed to Node-RED itself.

The following two commands show these two approaches:

```
node-red-pi --max-old-space-size=128 --userDir /home/user/node-red-data/
node --max-old-space-size=128 red.js --userDir /home/user/node-red-data/
```

### Starting Node-RED on boot

There are many methods of starting, stopping and monitoring applications at boot time. Raspberry Pi users are *strongly* recommended to follow [these instructions](https://nodered.org/docs/hardware/raspberrypi).

Linux users that have a Debian flavour (e.g. Ubuntu, Mint, Debian, etc) are recommended to use the [Adding Autostart capability using SystemD](https://nodered.org/docs/hardware/raspberrypi#adding-autostart-capability-using-systemd) instructions from the Raspberry Pi docs though you will need to edit the downloaded `/lib/systemd/system/nodered.service` file to suit your *user id* and environment.

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