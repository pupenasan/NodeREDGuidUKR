**Олександр ПУПЕНА**

# Довідник з Node-RED

# Вступ

Довідник створений з метою спрощення вивчення Node-RED студентам та спеціалістам з автоматизації та комп’ютерно-інтегрованих технологій. Зокрема даний довідник призначений для використання в лабораторних роботах в курсі «Технології індустрії 4.0». 

![pic](media/node-red-icon.png)

Нова версія на сайті Github [за посиалнням](https://pupenasan.github.io/NodeREDGuidUKR/)

Стара версія посібника доступна [за посиланням](https://drive.google.com/file/d/1tbhv1j-tiUGpIlAO4kWlInCRXJh0ZIqf/view?fbclid=IwAR2yP3egoT_Eie6nvtTQbZZDSVUyID3o-nmGTGHfgICvN8QZ4BDITM9X97U).

Якщо Ви хочете пришвидшити вивчення Node-RED а також багатьох інших технологій Інтернету речей та Індустрії 4.0, ви можете записатися на онлайн-курс [«Технології індустрії 4.0»](https://sites.google.com/view/i4uinua/%D0%BA%D1%83%D1%80%D1%81%D0%B8-i4u/%D1%82%D0%B5%D1%85%D0%BD%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D0%B8-%D0%B8%D0%BD%D0%B4%D1%83%D1%81%D1%82%D1%80%D0%B8%D0%B8-4-0) 

1. [Загальні основи користування Node-RED та основні компоненти](base/README.md) <span class="load"> </span>

2. [Розширення](extention/README.md) <span class="load"> </span>

3. [Dashboard (node-red-dashboard)](Dashboard/README.md) <span class="load"> </span>

4. [Вбудовані вузли для роботи з файлами](files/README.md) <span class="load"> </span>

5. [Базові операції з файлами: бібліотека fs-ops](fs_ops/README.md) <span class="load"> </span>

6. [Бібліотека MODBUS](modbus/README.md)<span class="load"> </span>

7. [Бібліотека MQTT](mqtt/README.md) <span class="load"> </span>

8. [Бібліотека HTTP](http/README.md) <span class="load"> </span>

9. [Бібліотека WebSocket](websocket/README.md) <span class="load"> </span>

10. [Бібліотека PARSING](parsing/README.md) <span class="load"> </span>

11. [Робота з JSONata](jsonata/README.md) <span class="load"> </span>

12. [Бібліотека Storage Cloudant](storage_cloudant/README.md) <span class="load"> </span>

13. [Бібліотека Storage COS (node-red-contrib-cos)](storage_cos/README.md) <span class="load"> </span>

14. [Робота з Watson IoT Device/Gateway (node-red-contrib-ibm-watson-iot)](watson_iot_device_gateway/README.md) <span class="load"> </span>

15. [Бібліотека IBM IoT APP (node-red-contrib-scx-ibmiotapp)](ibm_iot_app/README.md) <span class="load"> </span>

16. [Бібліотека OPC UA (node-red-contrib-opcua)](opcua/README.md) <span class="load"> </span>

17. [Робота з Базами даних](dbase/README.md) <span class="load"> </span>

18. [Робота з ОС](systems/README.md) <span class="load"> </span>

19. [Взаємодія з сервісами Google](google/README.md) <span class="load"> </span>

20. [Боти](bots/README.md) <span class="load"> </span>

    

# Перелік вузлів

## Стандартна комплектація

### Загальні (common)

|          Вузол          | Призначення                                                  | Примітка |
| :---------------------: | ------------------------------------------------------------ | -------- |
|  ![](media/inject.png)  | [Inject](base/1_4_1.md#inject-ініціювання-повідомлення) для ініціювання потоку (відправки повідомлення) користувачем, автоматично при запуску, періодично або за розкладом. | 07.2020  |
|  ![](media/debug.png)   | [Debug](base/1_4_1.md#debug-вивести-на-відлагодження) використовуватися для відображення повідомлень на бічній панелі Debug у редакторі. | 07.2020  |
| ![](media/complete.png) | [Complete](base/1_4_1.md#complete) запускає потік, коли інший вузол завершує оброблення повідомлення. | 07.2020  |
|  ![](media/catch.png)   | [Catch](base/1_4_1.md#catch-обробник-помилок) ловить помилки виконання інших вузлів у тому самому потоці (вкладці) і формує повідомлення з інформацією про них. | 07.2020  |
|  ![](media/status.png)  | [Status](base/1_4_1.md#status-стан-вузлу) показує стан (status message) вказаних або усіх вузлів в потоці. | 07.2020  |
| ![](media/link-in.png)  | [Link in](base/1_4_1.md#link-in-та-link-out-посилання) вхідне з'єднання з іншого потоку | 07.2020  |
| ![](media/link-out.png) | [Link out](base/1_4_1.md#link-in-та-link-out-посилання) вихідне з'єднання до іншого потоку | 07.2020  |
| ![](media/comment.png)  | [Comment](base/1_4_1.md#comment) для добавлення коментарів в потік. | 07.2020  |
| ![](media/unknown.png)  | [Unknown](base/1_4_1.md#unknown-невідомий) вузол невідомого типу для встановленого Node-RED | 07.2020  |

### Функціональні (function)

| Вузол                   | Призначення                                                  | Примітка |
| ----------------------- | ------------------------------------------------------------ | -------- |
| ![](media/function.png) | [Function](base/1_5.md) дозволяє виконувати код JavaScript для обробки повідомлень, що передаються через нього. | 07.2020  |
| ![](media/switch.png)   | [Switch](base/1_4_1.md#switch-перемикач-повідомлення) дозволяє передавати повідомлення до різних гілок потоку, оцінюючи набір правил для кожного повідомлення | 07.2020  |
| ![](media/change.png)   | [Change](base/1_4_1.md#change-зміна-повідомлення-в-потоці) для зміни властивостей повідомлення та контекстів (потоку і глобального) без необхідності вдаватися до вузла Function | 07.2020  |
| ![](media/range.png)    | [Range](base/1_4_1.md#range-масштабування) масштабує числові значення відповідно до вказаних вхідних та вихідних діапазонів | 07.2020  |
| ![](media/template.png) | [Template](base/1_4_1.md#template-шаблон) використовується для створення тексту з властивостей повідомлення з використанням означеного шаблону Mustache | 07.2020  |
| ![](media/delay.png)    | [Delay](base/1_4_1.md#delay-затримка) робить затримку для кожного повідомлення, що проходить через вузол, або обмежує швидкість, з якою вони можуть пройти. | 07.2020  |
| ![](media/trigger.png)  | [Trigger](base/1_4_1.md#trigger) відправляє повідомлення з вказаним інтервалом | 07.2020  |
| ![](media/exec.png)     | [Exec](base/1_4_1.md#exec-запуск-команди) запускає системну команду. | 07.2020  |
| ![](media/rbe.png)      | [Rbe](base/1_4_1.md#rbe-гістерезис-нечутливість) пропускає повідомлення лише у випадку зміни корисного навантаження | 07.2020  |

### Мережні (network)

| Вузол                             | Призначення                                                  | Примітка |
| --------------------------------- | ------------------------------------------------------------ | -------- |
| ![](media/mqtt-in.png)            | [Mqtt in](mqtt/mqttin.md) - підключається до брокера MQTT та підписується на повідомлення з зазначеної теми | 2019     |
| ![](media/mqtt-out.png)           | [Mqtt out](mqtt/mqttout.md) підключається до брокера MQTT та публікує повідомлення | 2019     |
| ![](media/mqtt-broker.png)        | [Mqtt-broker](mqtt/mqttbroker.md) конфігураційний вузол для Mqtt-broker | 2019     |
| ![](media/http-in.png)            | [Http-in](http/httpin.md) HTTP-сервер - обробка вхідного повідомлення | 2019     |
| ![](media/http-response.png)      | [Http response](http/httpresponse.md) HTTP-сервер - формування вихідного повідомлення | 2019     |
| ![](media/http-request.png)       | [Http request](http/httprequests.md) робота з клієнтськими запитами до HTTP-серверів | 2019     |
| ![](media/http-proxy.png)         | [Http proxy]()                                               |          |
| ![](media/tls-config.png)         | [Tls-config]()                                               |          |
| ![](media/websocket-in.png)       | [Websocket in](websocket/websocketin.md) вхідний вузол WebSocket | 2019     |
| ![](media/websocket-out.png)      | [Websocket out ](websocket/websocketout.md) вихідний вузол WebSocket | 2019     |
| ![](media/websocket-listener.png) | [Websocket-listener]()                                       |          |
| ![](media/websocket-client.png)   | [Websocket-client]()                                         |          |
| ![](media/tcp-in.png)             | [TCP in]()                                                   |          |
| ![](media/tcp-out.png)            | [TCP out]()                                                  |          |
| ![](media/tcp-request.png)        | [TCP request]()                                              |          |
| ![](media/udp-in.png)             | [UDP in]()                                                   |          |
| ![](media/udp-out.png)            | [UPD out]()                                                  |          |

### Послідовності (sequence)

| Вузол                | Призначення                                                  | Примітка |
| -------------------- | ------------------------------------------------------------ | -------- |
| ![](media/split.png) | [Split](base/1_6.md#split) розділює одне повідомлення в послідовність повідомлень. | 07.2020  |
| ![](media/join.png)  | [Join](base/1_6.md#join) об'єднує послідовність повідомлень у єдине повідомлення | 07.2020  |
| ![](media/sort.png)  | [Sort](base/1_6.md#sort) сортує масив або послідовність повідомлень на основі значення властивості або результату вираження JSONata | 07.2020  |
| ![](media/batch.png) | [Batch](base/1_6.md#batch) створює нові послідовності згрупованих повідомлень з отриманих. | 07.2020  |

### Парсери (parser) 

| Вузол               | Призначення                                                  | Примітка |
| ------------------- | ------------------------------------------------------------ | -------- |
| ![](media/csv.png)  | [CSV](parsing/csv.md) перетворює рядки, відформатовані CSV в об’єкти JavaScript та навпаки | 07.2020  |
| ![](media/html.png) | [HTML](parsing/html.md) витягує елементи з HTML-документа, що міститься у вказаній властивості `msg`  за допомогою селекторів CSS | 07.2020  |
| ![](media/json.png) | [JSON](parsing/json.md) перетворює рядки JSON в об’єкти JavaScript та в зворотному напрямку | 07.2020  |
| ![](media/xml.png)  | [XML](parsing/xml.md) перетворює рядок XML в об’єкт JavaScript та в зворотному напрямку напрямку. | 07.2020  |
| ![](media/yaml.png) | [YAML](parsing/yaml.md) перетворює рядок, відформатований в форматі YAML у об'єкт JavaScript та в зворотному напрямку | 07.2020  |

### Сховища (storage) 

| Вузол                  | Призначення                                                  | Примітка |
| ---------------------- | ------------------------------------------------------------ | -------- |
| ![](media/file.png)    | [File](files/fileout.md) записує дані у файл, додавши його до кінця або замінюючи існуючий вміст | 07.2020  |
| ![](media/file-in.png) | [File in](files/filein.md) читає вміст файлу у вигляді рядку або бінарного буферу | 07.2020  |
| ![](media/watch.png)   | [Watch](files/watch.md) відслідковує зміни в каталозі або у файлі. | 07.2020  |
| ![](media/tail.png)    | [Tail](files/tail.md) стежить за тим, що було додано у вказаний файл | 07.2020  |

## Dashboard

| Вузол                          | Призначення                                                  | Примітка |
| ------------------------------ | ------------------------------------------------------------ | -------- |
| ![](media/ui_button.png)       | [Button](Dashboard/Button.md) додає до інтерфейсу користувача кнопку | 2019     |
| ![](media/ui_dropdown.png)     | [Dropdown](Dashboard/Dropdown.md) додає до інтерфейсу користувача спадне меню вибору | 2019     |
| ![](media/ui_switch.png)       | [Switch](Dashboard/Switch.md) додає до інтерфейсу користувача перемикач. | 2019     |
| ![](media/ui_slider.png)       | [Slider](Dashboard/Slider.md) додає до інтерфейсу користувача віджет повзунка. | 2019     |
| ![](media/ui_numeric.png)      | [Numeric](Dashboard/Numeric.md) додає до інтерфейсу користувача віджет зміни числового значення кнопками «більше» та «менше». | 2019     |
| ![](media/ui_text_input.png)   | [Text input](Dashboard/Text_input.md) додає до інтерфейсу користувача поле введення тексту, електронної пошти або вибору кольорів. | 2019     |
| ![](media/ui_date_picker.png)  | [Date picker](Dashboard/Date_picker.md) додає до інтерфейсу користувача віджет вибору дати. | 2019     |
| ![](media/ui_color_picker.png) | [Color picker](Dashboard/Colour_picker.md) додає до інтерфейсу користувача панель вибору кольору. | 2019     |
| ![](media/ui_form.png)         | [Form](Dashboard/Form.md) додає до інтерфейсу користувача форму (кілька полів введення). | 2019     |
| ![](media/ui_text.png)         | [Text](Dashboard/Text.md) додає до інтерфейсу користувача поле для виведення тексту. | 2019     |
| ![](media/ui_gauge.png)        | [Gauge](Dashboard/Gauge.md) додає до інтерфейсу користувача віджет приладового показчика | 2019     |
| ![](media/ui_chart.png)        | [Chart](Dashboard/Chart.md) додає до інтерфейсу користувача діаграму з відображенням значень, що надходять на вхід у вигляді різного типу діаграм | 2019     |
| ![](media/ui_audio.png)        | [Audio](Dashboard/Audio_out.md) відтворює аудіо або текст в мову (text to speech TTS). | 2019     |
| ![](media/ui_toast.png)        | [Notification](Dashboard/Show_notification.md) показує `msg.payload` як спливаюче сповіщення або діалогове повідомлення з кнопками OK/Cancel | 2019     |
| ![](media/ui_ui_control.png)   | [Ui control](Dashboard/Ui_control.md) дозволяє динамічно керувати Dashboard. | 2019     |
| ![](media/ui_template.png)     | [Template](Dashboard/Template.md) шаблонний віджет (template widget) може містити будь-які дійсні директиви html та Angular/Angular-Material. | 2019     |
| ![](media/ui_link.png)         | [Link](Dashboard/config.md#link-посилання)                   | to do    |
| ![](media/ui_spacer.png)       | [Spacer](Dashboard/config.md#spacer-пустий-простір)          | to do    |
| ![](media/ui_tab.png)          | [Tab](Dashboard/config.md#tab-закладка)                      | to do    |
| ![](media/ui_base.png)         | [Base](Dashboard/config.md#base-база-UI)                     | to do    |
| ![](media/ui_group.png)        | [Group](Dashboard/config.md#group-група)                     | to do    |

