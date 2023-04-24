# Devices

https://flowforge.com/docs/user/devices/

Платформу FlowForge можна використовувати для керування примірниками Node-RED, що працюють на віддалених пристроях. Пристрій запускає програмний агент, який підключається до платформи для отримання оновлень. У цьому посібнику пояснюється, як почати роботу з функцією пристроїв.

## Встановлення агента пристрою

Агент пристрою публікується в загальнодоступному репозиторії npm як [@flowforge/flowforge-device-agent](https://www.npmjs.com/package/@flowforge/flowforge-device-agent). Його можна встановити як глобальний модуль npm. Це гарантує, що команда агента знаходиться на шляху:

```bash
sudo npm install -g @flowforge/flowforge-device-agent
```

Або ви можете запустити контейнер Docker. Коли ви це зробите, вам потрібно буде змонтувати `device.yaml`, отриманий коли [Registering the device](https://flowforge.com/docs/user/devices/#register-the-device): 

```bash
docker run --mount /path/to/device.yml:/opt/flowforge/device.yml -p 1880:1880 flowforge/device-agent:latest
```

## Configuration

### Execution directory

За замовчуванням агент використовує `/opt/flowforge-device` як свій робочий каталог. Це можна змінити за допомогою опції `-d/--dir`. Каталог має існувати та бути доступним для користувача, який запускатиме агент.

```bash
sudo mkdir /opt/flowforge-device
sudo chown -R $USER /opt/flowforge-device
```

### Listen Port

За замовчуванням Node-RED слухатиме порт `1880`. Агент пристрою має прапорець, щоб змінити цю поведінку та прослуховувати інший порт за вибором: `-p/--port`. Це може бути корисно для спеціальних правил брандмауера або під час запуску кількох агентів пристроїв на одній машині.

```bash
flowforge-device-agent --port=1881
```

## Register the device

Щоб підключити пристрій до платформи, йому потрібен набір облікових даних.

Є два типи облікових даних на вибір:

- **Облікові дані пристрою (Device Credentials)**: для підключення одного пристрою до платформи
- **Надання облікових даних (Provisioning Credentials)**: для налаштування одного або кількох пристроїв для автоматичної реєстрації на платформі

### Generating "Device Credentials"

*для одного пристрою*

1. Перейдіть на сторінку **Devices** ваших команд.
2. Натисніть кнопку **Register Device**.
3. Вам буде запропоновано дати пристрою **name** та необов’язковий **type**. Поле типу можна використовувати для запису додаткової метаінформації про пристрій.
4. Натисніть **Register**

Після реєстрації пристрою ви побачите діалогове вікно **Device Credentials**. Це єдиний раз, коли платформа покаже вам цю інформацію без її скидання. Обов’язково зробіть копію або скористайтеся **Download**, щоб зберегти файл конфігурації локально. Повторіть ці дії для кожного пристрою, який потрібно підключити до платформи.

### Generating "Provisioning Credentials"

*для автоматичної реєстрації одного або кількох пристроїв*

1. Перейдіть на сторінку **Settings** ваших команд.
2. Відкрийте вкладку **Device**.
3. Натисніть вкладку **Create Provisioning Token**.
4. Вам буде запропоновано дати маркеру **name** та вибрати, якому **instance**, якщо такий є, слід призначити пристрій.
5. Натисніть **Create**

Після створення маркера надання вам буде показано діалогове вікно **Device Provisioning Credentials (Облікові дані пристрою)**. Це єдиний раз, коли платформа покаже вам цю інформацію. Обов’язково зробіть копію або скористайтеся **Download**, щоб зберегти файл конфігурації локально.

## Connect the device

### Using Device Credentials

Скопіюйте інформацію **Device Credentials** у файл під назвою `device.yml` у каталозі конфігурації пристрою (`/opt/flowforge-device` або будь-який інший, встановлений за допомогою параметра `-d`).

Потім агент можна запустити командою: [[1\]](https://flowforge.com/docs/user/devices/#fn1)

```баш
flowforge-device-agent
```

Ви побачите, як пристрій запускається та виконує «call-home», де він підключається до платформи, щоб перевірити, що він має запустити.

### Using Provisioning Credentials

Скопіюйте інформацію **Device Provisioning Credentials** у файл під назвою `device.yml` у каталозі конфігурації пристрою (`/opt/flowforge-device` або будь-який інший, встановлений за допомогою параметра `-d`).

Потім агент можна запустити командою: [[1:1\]](https://flowforge.com/docs/user/devices/#fn1)

```баш
flowforge-device-agent
```

Ви побачите, як пристрій запускається та виконує «call-home», де він підключається до платформи для автоматичної реєстрації на пристроях групи. У разі успіху справжні **Device Credentials** генеруються та завантажуються на пристрій. Оригінальні **Provisioning Credentials** буде перезаписано, що означає, що для наступних запусків не потрібно буде знову виконувати автоматичну реєстрацію.

## Призначте пристрій екземпляру Node-RED

Наступним кроком є призначення пристрою екземпляру Node-RED.

1. Перейдіть на сторінку **Devices** ваших команд.
2. Відкрийте спадне меню праворуч від пристрою, який потрібно призначити, і виберіть опцію **Add to Application Instance**.
3. Виберіть примірник у діалоговому вікні та натисніть **Add**, щоб продовжити.

## Розгортання примірника Node-RED на пристрої

Щоб розгорнути екземпляр Node-RED на пристрої:

1. [Create a snapshot](https://flowforge.com/docs/user/snapshots#create-a-snapshot) – резервна копія потоків і конфігурації Node-RED на певний момент часу.
2. [Mark that snapshot](https://flowforge.com/docs/user/snapshots#setting-a-device-target-snapshot) як знімок **Device Target**.

Ця модель дозволяє вам розвивати свої потоки у FlowForge і надсилати їх на зареєстровані пристрої лише тоді, коли ви задоволені тим, що створили.

## Remove a device from a Node-RED instance

To remove the device from a Node-RED instance:

1. Go to your teams's **Devices** page.
2. Open the dropdown menu to the right of the device you want to remove and select the **Remove from application instance** option.
3. Confirm the action by clicking the **Remove** option.

The device will stop running the current Node-RED flows. It will then wait until it is assigned to another instance.

## Regenerating credentials

To regenerate device credentials:

1. Go to your team's or instance's **Devices** page.
2. Open the dropdown menu to the right of the device and select the **Regenerate credentials** option.
3. You will need to confirm this action as the existing credentials will be immediately revoked. If the device tries to use the old credentials it will fail to connect and will delete its local copy of the snapshot it was running. Click **Regenerate credentials** to continue.

You will then be shown the **Device Credentials** dialog again with a new set of credentials to copy or download.

## Deleting a device

To delete a device:

1. Go to your team's or instance's **Devices** page.
2. Open the dropdown menu to the right of the device and select the **Delete device** option.
3. Confirm the action by clicking the **Delete** option.

The next time the device attempts to connect to the platform it will find it is no longer authorised and will stop and delete its local copy of the flows it was running.

## Running with no access to npmjs.org

By default the Device Agent will try and download the correct version of Node-RED and any nodes required to run the Snapshot that is assigned to run on the device.

If the device is being run on an offline network or security policies prevent the Device Agent from connecting to npmjs.org then it can be configured to use a pre-cached set of modules.

You can enable this mode by adding `-m` to the command line adding `moduleCache: true` to the `device.yml` file. This will cause the Device Agent to load the modules from the `module_cache` directory in the Device Agents Configuration directory as described above. By default this will be `/opt/flowforge-device/module_cache`.

### Creating a module cache

To create a suitable module cache, you will need to install the modules on a local device with access to npmjs.org, ensuring you use the same OS and Architecture as your target device, and then copy the modules on to your device.

1. From the Snapshot page, select the snapshot you want to deploy and select the option to download its `package.json` file.
2. Place this file in an empty directory on your local device.
3. Run `npm install` to install the modules. This will create a `node_modules` directory.
4. On your target device, create a directory called `module_cache` inside the Device Agent Configuration directory.
5. Copy the `node_modules` directory from your local device to the target device so that it is under the `module_cache` directory.