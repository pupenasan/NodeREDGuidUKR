| [На головну](../) | [ < Розділ > ](README.md) |
| ----------------- | ------------------------- |
|                   |                           |

## node-red-contrib-cpu ([link](https://flows.nodered.org/node/node-red-contrib-os))

Цей вузол моніторить використання CPU, і базується на [Node.js OS Library](https://nodejs.org/api/os.html).  

Приклад потоку:

![Flow](https://raw.githubusercontent.com/bartbutenaers/node-red-contrib-cpu/master/images/cpu_flow.png)

Коли тригерне повідомлення відправляється на вхід, перераховується використання CPU. Розраховане використання CPU базується на середньому значенні з попереднього розрахунку, тому обчислене значення стане більш точним, коли період між викликами і відповідно розрахунками буде  невеликим. Рекомендується щосекундний виклик.

У налаштуваннях вузла вказуються опції:

![](media/cpuprop.png)

### Єдине вихідне повідомлення про усереднене використання CPU (Single output message for overall cpu usage)

Якщо вибрано параметр "Single output message for overall cpu usage", буде створено одне вихідне повідомлення, яке містить загальне використання CPU (з топіком `загальний`). Загальне використання процесора обчислюється як усереднене значення використання усіх ядер:

![Formula](https://raw.githubusercontent.com/bartbutenaers/node-red-contrib-cpu/master/images/cpu_formula.png)

Саймон Хейлес порадив автору вузла додати цей варіант, оскільки графіки на ядро можуть стати занадто зашумленими. Наприклад, з наступного графу Ви можете зробити висновок (неправильний!), що для обробки відео (за допомогою бібліотеки OpenCv) добре використовуються всі 4 ядра Raspberry Pi:

![Formula](https://raw.githubusercontent.com/bartbutenaers/node-red-contrib-cpu/master/images/cpu_each_core.png)

Однак, дивлячись на загальне використання процесора, стає зрозуміло, що використовується лише 25% ресурсів процесора Raspberry Pi:

![Formula](https://raw.githubusercontent.com/bartbutenaers/node-red-contrib-cpu/master/images/cpu_overall.png)

Це означає, що бібліотека використовує всі 4 наявні ядра, але загалом лише 25% з 4 ядер ...

Буде єдине вихідне повідомлення, що містить загальні дані всіх ядер:

- `msg.payload` - усереднене значення у % (сумарне використання усіх дер поділена на їх кількість)
- `msg.speed` - частота процесору в MHz
- `msg.topic` - фіксоване текстове значення `overall`
- `msg.model` - модель CPU

### Розділені вихідні повідомлення для кожного ядра (Separate output message for each core)

Якщо вибрано цей параметр, буде створено вихідне повідомлення для кожного ядра окремо. Оскільки кожне ядро отримує власний `topic` (`core_xxx`), відображати всі ядра в одному графіку на інформаційній панелі стає дуже просто:

![Graph with multiple cores](https://raw.githubusercontent.com/bartbutenaers/node-red-contrib-cpu/master/images/cpu_legend.png)

Вихідне повідомлення для кожного ядра матиме вигляд:

- `msg.payload` - використання ядра у % 
- `msg.speed` - частота процесора в MHz
- `msg.topic` - назва логічного ядра CPU (`core_xxx`)
- `msg.model` - модель CPU 

Це приклад такого вихідного повідомлення:

![Debug message](https://raw.githubusercontent.com/bartbutenaers/node-red-contrib-cpu/master/images/cpu_debug.png)

### Єдине вихідне повідомлення з масивом використання ядер (Single output message with array of core usages)

Якщо вибрано цей параметр, буде створено одне вихідне повідомлення, яке містить масив усіх використань процесора (з topic `all_cores`).

- ```
  msg.payload
  ```

  це масив з інформацією про всі наявні ядра:

  - `msg.payload` - використання ядра у % 
  - `msg.speed` - частота процесора в MHz
  - `msg.topic` - назва логічного ядра CPU (`core_xxx`)
  - `msg.model` - модель CPU 

- `msg.topic` фіксований текст (`all_cores`)

### Єдине вихідне повідомлення з температурами ядер (Single output message with core temperature(s))

Якщо вибрано цей параметр, буде створено одне вихідне повідомлення, яке містить значення температури в ° C (з topic `temperature`).

![Temperature graph](https://raw.githubusercontent.com/bartbutenaers/node-red-contrib-cpu/master/images/cpu_temperature_graph.png)

Вихідне повідомлення матиме вигляд:

- `msg.payload` основна (усереднена) температура
- `msg.max` максимальна температура
- `msg.cores` масив температур по усім ядрам 
- `msg.topic` фіксований текст (`temperature`)

УВАГА: значення температури доступні не у всіх системах (наприклад, у Sun systems)! І в деяких системах масив `msg.cores` буде порожнім (наприклад, на Raspberry Pi 3), але замість цього може бути доступна основна температура.

## Означення поняття ядра (Core) 

Як було сказано раніше, дані будуть виводитися для кожного ядра. Однак що представляє собою ядро?

У випадку системи з N процесорами (і M ядрами в кожному процесорі) загальна кількість **фізичних** ядер на графіці буде NxM.

Однак іноді ми отримаємо набагато більше **віртуальних** ядер на виході (порівняно з кількістю фізичних ядер). Це може бути, наприклад, з процесорами, які підтримують [Hyper Threading](https://en.wikipedia.org/wiki/Hyper-threading).

## Боротьба з несправностями

Цей вузол можна легко використовувати для виявлення проблем з продуктивністю, не встановлюючи додаткових сторонніх інструментів.

В якості вихідної точки (для порівняння власного графіку використання CPU ) основний потік Node-Red використовує дуже мало основних ресурсів (крім періоду розгортання):

![Basic flow graph](https://raw.githubusercontent.com/bartbutenaers/node-red-contrib-cpu/master/images/cpu_graph.png)

## Alternative

The The [node-red-contrib-os](https://www.npmjs.com/package/node-red-contrib-os) node also contains a 'cpus' node, which can be used to get the same  kind of information.  However there are some differences between both  nodes:

Вузол [node-red-contrib-os](os.md) також містить вузол 'cpus', який можна використовувати для отримання такого ж типу інформації. Однак існують деякі відмінності між обома вузлами:

|                   |      node-red-contrib-os (cpus)       | node-red-contrib-cpu |
| ----------------- | :-----------------------------------: | :------------------: |
| Multiple cores    |             all in 1 msg              |  separate messages   |
| Measurement start |            system startup             | previous calculation |
| Output value      | multiple values (idle, user, sys ...) |  single percentage   |

Вузол node-red-contrib-cpu - це зручний вузол, який бере на себе всі обчислення у випадку, якщо ви хочете контролювати роботу процесора в реальному часі.

| [На головну](../) | [ < Розділ > ](README.md) |
| ----------------- | ------------------------- |
|                   |                           |