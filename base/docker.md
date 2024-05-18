# Запуск під Docker

https://nodered.org/docs/getting-started/docker

У цьому посібнику передбачається, що ви маєте базові знання про Docker і [командний рядок Docker](https://docs.docker.com/engine/reference/commandline/cli/). У ньому описуються деякі з багатьох способів запуску Node-RED під Docker і підтримка кількох архітектур (amd64, arm32v6, arm32v7, arm64v8 і s390x).

Починаючи з Node-RED 1.0, репозиторій на [Docker Hub](https://hub.docker.com/r/nodered/node-red/) було перейменовано на `nodered/node-red`.

### Швидкий старт

Щоб запустити Docker у найпростішій формі, просто запустіть:

```
docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red
```

Давайте розберемо цю команду:

- `docker run`  - запустити цей контейнер, спочатку збираючи локально, якщо необхідно
- `-it`  - приєднайте термінальний сеанс, щоб ми могли бачити, що відбувається
- `-p 1880:1880`  - підключіть локальний порт 1880 до відкритого внутрішнього порту 1880       
- `-v node_red_data:/data`  - монтуйте том докера під назвою `node_red_data` до каталогу контейнера /даних, щоб усі зміни, внесені до потоків, зберігалися
- `--name mynodered` - дайте цій машині дружню місцеву назву
- `nodered/node-red` -  образ, на основі якого – наразі Node-RED v1.2.0      

Виконання цієї команди має дати вікно терміналу з запущеним екземпляром Node-RED.

```
    Welcome to Node-RED
    ===================

    10 Oct 12:57:10 - [info] Node-RED version: v1.2.0
    10 Oct 12:57:10 - [info] Node.js  version: v10.22.1
    10 Oct 12:57:10 - [info] Linux 4.19.76-linuxkit x64 LE
    10 Oct 12:57:11 - [info] Loading palette nodes
    10 Oct 12:57:16 - [info] Settings file  : /data/settings.js
    10 Oct 12:57:16 - [info] Context store  : 'default' [module=memory]
    10 Oct 12:57:16 - [info] User directory : /data
    10 Oct 12:57:16 - [warn] Projects disabled : editorTheme.projects.enabled=false
    10 Oct 12:57:16 - [info] Flows file     : /data/flows.json
    10 Oct 12:57:16 - [info] Creating new flow file
    10 Oct 12:57:17 - [warn]

    ---------------------------------------------------------------------
    Your flow credentials file is encrypted using a system-generated key.

    If the system-generated key is lost for any reason, your credentials
    file will not be recoverable, you will have to delete it and re-enter
    your credentials.

    You should set your own key using the 'credentialSecret' option in
    your settings file. Node-RED will then re-encrypt your credentials
    file using your chosen key the next time you deploy a change.
    ---------------------------------------------------------------------

    10 Oct 12:57:17 - [info] Starting flows
    10 Oct 12:57:17 - [info] Started flows
    10 Oct 12:57:17 - [info] Server now running at http://127.0.0.1:1880/

    [...]
```

Потім ви можете перейти до `http://{host-ip}:1880`, щоб отримати знайомий робочий стіл Node-RED.

Перевага цього полягає в тому, що, давши йому назву (`mynodered`), ми можемо маніпулювати ним легше, а виправивши порт хоста, ми знаємо, що ми знаходимося на знайомому місці. Звичайно, це означає, що ми можемо запускати лише один екземпляр за раз... але крок за кроком, люди.

Якщо ми задоволені тим, що бачимо, ми можемо від'єднати термінал за допомогою `Ctrl-p` `Ctrl-q` - контейнер продовжуватиме працювати у фоновому режимі. 

Щоб повторно під’єднатися до терміналу (щоб переглянути журналювання), виконайте:

```
docker attach mynodered
```

Якщо вам потрібно перезапустити контейнер (наприклад, після перезавантаження чи перезапуску демона Docker):

```
docker start mynodered
```

і зупиніть його знову, коли потрібно:

```
docker stop mynodered
```

### Варіації образів

Образи Node-RED базуються на [офіційних образах Node JS Alpine Linux](https://hub.docker.com/_/node/), щоб вони були якомога меншими. Використання Alpine Linux зменшує розмір створеного образу, але видаляє стандартні залежності, необхідні для компіляції рідного модуля. Якщо ви хочете додати залежності за допомогою власних залежностей, розширте образ Node-RED за допомогою відсутніх пакетів у запущених контейнерах або створіть нові образи, див. [docker-custom](https://nodered.org/docs/getting-started/docker- custom), який розширює [README.md](https://github.com/node-red/node-red-docker/tree/master/docker-custom) у проекті Node-RED Docker.

Перегляньте [проект Github README](https://github.com/node-red/node-red-docker/blob/master/README.md), щоб отримати детальну інформацію про зображення, теги та маніфести.

Наприклад: припустімо, що ви працюєте на Raspberry PI 3B, який має `arm32v7` як архітектуру. Потім просто виконайте наступну команду, щоб отримати зображення (з тегом `1.2.0-10-arm32v7`), і запустіть контейнер.

```
docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red:latest
```

Цю ж команду можна використовувати для запуску в системі amd64, оскільки Docker виявляє, що він працює на хості amd64, і отримує образ з відповідним тегом (`1.2.0-10-amd64`).

Це має ту перевагу, що вам не потрібно знати/вказувати, на якій архітектурі ви працюєте, і робить команди запуску докерів і файли створення докерів більш гнучкими та придатними для обміну між системами.

**Примітка**: наразі існує помилка у виявленні архітектури Docker, яка не вдається виконати для `arm32v6` - наприклад, Raspberry Pi Zero або 1. Для цих пристроїв наразі потрібно вказати повний тег образу, наприклад:

```
docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red:1.2.0-10-arm32v6
```

Починаючи з Node-RED v3.1.0, ми також надаємо образ на основі Debian для тих вузлів із рідними компонентами, які погано працюють на Alpine.

### Управління даними користувача

Після запуску Node-RED із Docker нам потрібно переконатися, що будь-які додані вузли чи потоки не будуть втрачені, якщо контейнер буде знищено. Ці дані користувача можна зберегти шляхом монтування каталогу даних до тому за межами контейнера. Це можна зробити за допомогою монтування прив’язки або іменованого тому даних.

Node-RED використовує каталог `/data` всередині контейнера для зберігання конфігураційних даних користувача.

#### Використання каталогу хоста (Host Directory) для збереження (прив’язане монтування)

Щоб зберегти каталог користувача Node-RED всередині контейнера в каталозі хоста за межами контейнера, ви можете скористатися наведеною нижче командою. Щоб дозволити доступ до цього каталогу хосту, користувач node-red (за замовчуванням uid=1000) усередині контейнера повинен мати той самий uid, що й власник каталогу хосту.

```
docker run -it -p 1880:1880 -v /home/pi/.node-red:/data --name mynodered nodered/node-red
```

У цьому прикладі каталог хоста `/home/pi/.node-red` прив'язаний до каталогу `/data` контейнера.

**Примітка**: користувачі, які переходять з версії 0.20 на 1.0, повинні переконатися, що будь-який існуючий каталог `/data` має правильне право власності. Починаючи з версії 1.0, це має бути «1000:1000». Це можна примусово виконати командою `sudo chown -R 1000:1000 path/to/your/node-red/data`

Перегляньте [вікі](https://github.com/node-red/node-red-docker/wiki/Permissions-and-Persistence), щоб отримати детальну інформацію про дозволи.

#### Використання іменованих томів даних (Named Data Volumes)

Docker також підтримує використання іменованих [томів даних](https://docs.docker.com/engine/tutorials/dockervolumes/) для зберігання постійних або спільних даних поза контейнером.

Щоб створити новий іменований том даних для збереження наших даних користувача та запустити новий контейнер, використовуючи цей том.

```
$ docker volume create --name node_red_data
$ docker volume ls
DRIVER              VOLUME NAME
local               node_red_data
$ docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red
```

Якщо вам потрібно створити резервну копію даних із підключеного тому, ви можете отримати доступ до нього, коли контейнер працює.

```
$ docker cp  mynodered:/data  /your/backup/directory
```

Використовуючи Node-RED для створення та розгортання деяких зразків потоків, тепер ми можемо знищити контейнер і запустити новий екземпляр без втрати даних користувача.

```
$ docker stop mynodered
$ docker rm mynodered
$ docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red
```

### Оновлення

Оскільки `/data` тепер зберігаються за межами контейнера, оновити базовий образ контейнера тепер так просто, як

```
$ docker pull nodered/node-red
$ docker stop mynodered
$ docker rm mynodered
$ docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red
```

### Docker Stack / Docker Compose

Нижче наведено приклад файлу Docker Compose, який можна запускати за допомогою `docker stack` або `docker-compose`. Для отримання додаткової інформації відвідайте офіційні сторінки Docker  [Docker stack](https://docs.docker.com/engine/reference/commandline/stack/) and [Docker compose](https://docs.docker.com/compose/).

```
################################################################################
# Node-RED Stack or Compose
################################################################################
# docker stack deploy node-red --compose-file docker-compose-node-red.yml
# docker-compose -f docker-compose-node-red.yml -p myNoderedProject up
################################################################################
version: "3.7"

services:
  node-red:
    image: nodered/node-red:latest
    environment:
      - TZ=Europe/Amsterdam
    ports:
      - "1880:1880"
    networks:
      - node-red-net
    volumes:
      - node-red-data:/data

volumes:
  node-red-data:

networks:
  node-red-net:
```

Наведений вище файл створення:

- створює службу node-red
- витягує останній образ node-red 
- встановлює часовий пояс на Європу/Амстердам
- Відображає контейнерний порт 1880 на хост-порт 1880
- створює мережу `node-red-net` і приєднує контейнер до цієї мережі
- зберігає каталог `/data` всередині контейнера в томі `node-red-data` в Docker

### Dockerfile, який копіюється в локальні ресурси

Іноді може бути корисним заповнити образ Node-RED Docker файлами з локального каталогу (наприклад, якщо ви хочете, щоб весь проект зберігався в репозиторії git). Для цього вам потрібно, щоб ваш локальний каталог виглядав так:

```
Dockerfile
README.md
package.json     # додайте будь-які додаткові вузли, які потрібні вашому потоку, у ваш власний файл package.json. 
flows.json       # звичайне місце Node-RED зберігає ваші потоки
flows_cred.json  # облікові дані, які можуть знадобитися вашим потокам
settings.js      # ваш файл налаштувань
```

**ПРИМІТКА**: цей метод НЕ підходить, якщо ви хочете підключити том `/data` ззовні. Якщо вам потрібно використовувати зовнішній том для збереження, скопіюйте налаштування та натомість передайте файли на цей том.

Наступний Dockerfile створено на основі базового образу Docker Node-RED, але додатково переміщує ваші файли на місце в цьому образі:

```
FROM nodered/node-red

# Copy package.json to the WORKDIR so npm builds all
# of your added nodes modules for Node-RED
WORKDIR /data
COPY package.json /data
RUN npm install --unsafe-perm --no-update-notifier --no-fund --only=production
WORKDIR /usr/src/node-red

# Copy _your_ Node-RED project files into place
# NOTE: This will only work if you DO NOT later mount /data as an external volume.
#       If you need to use an external volume for persistence then
#       copy your settings and flows files to that volume instead.
COPY settings.js /data/settings.js
COPY flows_cred.json /data/flows_cred.json
COPY flows.json /data/flows.json
```

**Примітка**: файл `package.json` повинен містити параметр запуску в розділі сценарію. Наприклад, типовий контейнер такий:

```
    "scripts": {
        "start": "node $NODE_OPTIONS node_modules/node-red/red.js $FLOWS",
        ...
```

#### Порядок файлів Docker і швидкість створення

Незважаючи на те, що це не обов’язково, було б гарною ідеєю виконати кроки `COPY package... npm install...` раніше, тому що, хоча `flows.json` часто змінюється під час роботи в Node-RED, ваш `package.json` зміниться лише тоді, коли ви зміните, які модулі є частиною вашого проекту. І оскільки крок `npm install`, який має відбуватися під час змін `package.json`, іноді може займати багато часу, краще виконати трудомісткі кроки, які зазвичай не змінюються, раніше у файлі Docker, щоб ці образи збірки можна було використовувати повторно, що робить наступні загальні збірки набагато швидшими.

#### Облікові дані, секрети та змінні середовища

Звичайно, ви ніколи не хочете жорстко кодувати облікові дані будь-де, тому, якщо вам потрібно використовувати облікові дані у вашому проекті Node-RED, наведений вище Dockerfile дозволить вам мати це у вашому `settings.js`…

```
module.exports = {
  credentialSecret: process.env.NODE_RED_CREDENTIAL_SECRET // add exactly this
}
```

…а потім, коли ви запускаєте Docker, ви додаєте змінну середовища до своєї команди `run`...

```
docker run -e "NODE_RED_CREDENTIAL_SECRET=your_secret_goes_here"
```

#### Building and running

Ви *build* цей Dockerfile зазвичай:

```
docker build -t your-image-name:your-tag .
```

Щоб *запустити* локально для розробки, де зміни записуються негайно і лише в локальний каталог, з яким ви працюєте, `cd` у каталог проекту, а потім запустіть:

```
docker run --rm -e "NODE_RED_CREDENTIAL_SECRET=your_secret_goes_here" -p 1880:1880 -v `pwd`:/data --name a-container-name your-image-name
```

### Запуск

Змінні середовища можна передати в контейнер, щоб налаштувати час виконання Node-RED.

Файл конфігурації потоків налаштовується за допомогою параметра середовища (**FLOWS**), який за замовчуванням має *‘flows.json’*. Це можна змінити під час виконання за допомогою наступного прапора командного рядка.

```
docker run -it -p 1880:1880 -v node_red_data:/data -e FLOWS=my_flows.json nodered/node-red
```

**Примітка**: якщо ви встановите `-e FLOWS=""`, то файл потоку можна встановити через властивість *flowFile* у файлі `settings.js`.

Інші корисні змінні середовища включають

- `-e NODE_RED_ENABLE_SAFE_MODE=false` # setting to true starts Node-RED in safe (not running) mode
- `-e NODE_RED_ENABLE_PROJECTS=false`  # setting to true starts Node-RED with the projects feature enabled

Аргументи середовища виконання Node.js можна передати в контейнер за допомогою параметра середовища (**NODE_OPTIONS**). Наприклад, щоб виправити розмір купи, який використовується збирачем сміття Node.js, ви повинні використати таку команду.

```
docker run -it -p 1880:1880 -v node_red_data:/data -e NODE_OPTIONS="--max_old_space_size=128" nodered/node-red
```

### Біг headless

Щоб працювати headless (тобто у фоновому режимі), просто замініть `-it` у більшості попередніх команд на `-d`, наприклад:

```
docker run -d -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red
```

### Container Shell

Коли він працює headless, ви можете використати наступну команду, щоб повернути доступ до контейнера.

```
$ docker exec -it mynodered /bin/bash
bash-4.4$
```

Надасть командний рядок всередині контейнера, де ви зможете запустити потрібну команду встановлення npm, наприклад

```
bash-4.4$ npm install node-red-dashboard
bash-4.4$ exit
$ docker stop mynodered
$ docker start mynodered
```

Оновлення сторінки веб-переглядача тепер має показати щойно додані вузли в палітрі.

### Multiple Instances

Running

```
docker run -d -p 1880 nodered/node-red
```

will create a locally running instance of a machine. Note: we did not specify a name.

This container will have an id number and be running on a random port… to find out which port, run `docker ps`

```
$ docker ps
CONTAINER ID  IMAGE             COMMAND                 CREATED         STATUS        PORTS                    NAMES
860258cab092  nodered/node-red  "npm start -- --user…"  10 seconds ago  Up 9 seconds  0.0.0.0:32768->1880/tcp  dazzling_euler
```

You can now point a browser to the host machine on the tcp port reported back, so in the example above browse to `http://{host ip}:32768`

### Linking Containers

You can link containers “internally” within the docker runtime by using Docker [user-defined bridges](https://docs.docker.com/network/bridge/).

Before using a bridge, it needs to be created.  The command below will create a new bridge called **iot**

```
docker network create iot
```

Then all containers that need to communicate need to be added to the same bridge using the **–network** command line option

```
docker run -itd --network iot --name mybroker eclipse-mosquitto mosquitto -c /mosquitto-no-auth.conf
```

(no need to expose the port 1883 globally unless you want to… as we do magic below)

Then run nodered docker, also added to the same bridge

```
docker run -itd -p 1880:1880 --network iot --name mynodered nodered/node-red
```

containers on the same user-defined bridge can take advantage of the  built in name resolution provided by the bridge and use the container  name (specified using the **–name** option) as the target hostname.

In the above example the broker can be reached from the Node-RED application using hostname *mybroker*.

Then a simple flow like below show the mqtt nodes connecting to the broker

```
    [{"id":"c51cbf73.d90738","type":"mqtt in","z":"3fa278ec.8cbaf","name":"","topic":"test","broker":"5673f1d5.dd5f1","x":290,"y":240,"wires":[["7781c73.639b8b8"]]},{"id":"7008d6ef.b6ee38","type":"mqtt out","z":"3fa278ec.8cbaf","name":"","topic":"test","qos":"","retain":"","broker":"5673f1d5.dd5f1","x":517,"y":131,"wires":[]},{"id":"ef5b970c.7c864","type":"inject","z":"3fa278ec.8cbaf","name":"","repeat":"","crontab":"","once":false,"topic":"","payload":"","payloadType":"date","x":290,"y":153,"wires":[["7008d6ef.b6ee38"]]},{"id":"7781c73.639b8b8","type":"debug","z":"3fa278ec.8cbaf","name":"","active":true,"tosidebar":true,"console":false,"tostatus":true,"complete":"payload","targetType":"msg","statusVal":"payload","statusType":"auto","x":505,"y":257,"wires":[]},{"id":"5673f1d5.dd5f1","type":"mqtt-broker","z":"","name":"","broker":"mybroker","port":"1883","clientid":"","usetls":false,"compatmode":false,"keepalive":"15","cleansession":true,"birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":"","closeTopic":"","closeRetain":"false","closePayload":"","willTopic":"","willQos":"0","willRetain":"false","willPayload":""}]
```

This way the internal broker is not exposed outside of the docker host - of course you may add `-p 1883:1883`  etc to the broker run command if you want other systems outside your computer to be able to use the broker.

### Raspberry PI - native GPIO support

| v1.0 - BREAKING: Native GPIO support for Raspberry PI has been dropped | | — | The replacement for native GPIO is [node-red-node-pi-gpiod](https://github.com/node-red/node-red-nodes/tree/master/hardware/pigpiod).

Disadvantages of the native GPIO support are:

- Your Docker container needs to be deployed on the same Docker node/host on which you want to control the gpio.
- Gain access to `/dev/mem` of your Docker node/host
- privileged=true is not supported for `docker stack` command

`node-red-node-pi-gpiod` fixes all these disadvantages. With `node-red-node-pi-gpiod` it is possible to interact with gpio of multiple Raspberry Pi’s from a  single Node-RED container, and for multiple containers to access  different gpio on the same Pi.

#### Quick Migration steps to `node-red-node-pi-gpiod`

1. Install `node-red-node-pi-gpiod` through the Node-RED palette.
2. Install and run `PiGPIOd daemon` on the host Pi. For detailed install instruction please refer to the `node-red-node-pi-gpiod` [README](https://github.com/node-red/node-red-nodes/tree/master/hardware/pigpiod#node-red-node-pi-gpiod).
3. Replace all native gpio nodes with `pi gpiod` nodes.
4. Configure `pi gpiod` nodes to connect to `PiGPIOd daemon`. Often the host machine will have an IP 172.17.0.1 port 8888 - but not always. You can use `docker exec -it mynodered ip route show default | awk '/default/ {print $3}'` to check.

**Note**: There is a contributed [gpiod project](https://github.com/corbosman/node-red-gpiod) that runs the gpiod in its own container rather than on the host if required.

### Serial Port - Dialout - Adding Groups

To access the host serial port you may need to add the container to the `dialout` group. This can be enabled by adding `--group-add dialout` to the start command. For example

```
docker run -it -p 1880:1880 -v node_red_data:/data --group-add dialout --name mynodered nodered/node-red
```

------

### Common Issues and Hints

Here is a list of common issues users have reported with possible solutions.

#### User Permission Errors

See [the wiki](https://github.com/node-red/node-red-docker/wiki/Permissions-and-Persistence) for detailed information on permissions.

If you are seeing *permission denied* errors opening files or accessing host devices, try running the container as the root user.

```
docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered -u node-red:dialout nodered/node-red
```

References:

https://github.com/node-red/node-red-docker/issues/15

https://github.com/node-red/node-red-docker/issues/8

#### Accessing Host Devices

If you want to access a device from the host inside the container,  e.g. serial port, use the following command-line flag to pass access  through.

```
docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered --device=/dev/ttyACM0 nodered/node-red
```

References: https://github.com/node-red/node-red/issues/15

#### Setting Timezone

If you want to modify the default timezone, use the TZ environment variable with the [relevant timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

```
docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered -e TZ=America/New_York nodered/node-red
```

or within a docker-compose file

```
  node-red:
    environment:
      - TZ=America/New_York
```

References: https://groups.google.com/forum/#!topic/node-red/ieo5IVFAo2o