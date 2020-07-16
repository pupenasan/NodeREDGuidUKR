**Олександр ПУПЕНА**

# Довідник з Node-RED

# Вступ

Довідник створений з метою спрощення вивчення Node-RED студентам та спеціалістам з автоматизації та комп’ютерно-інтегрованих технологій. Зокрема даний довідник призначений для використання в лабораторних роботах в курсі «Технології індустрії 4.0». 

![pic](media/node-red-icon.png)

Нова версія на сайті Github [за посиалнням](https://pupenasan.github.io/NodeREDGuidUKR/)

Стара версія посібника доступна [за посиланням](https://drive.google.com/file/d/1tbhv1j-tiUGpIlAO4kWlInCRXJh0ZIqf/view?fbclid=IwAR2yP3egoT_Eie6nvtTQbZZDSVUyID3o-nmGTGHfgICvN8QZ4BDITM9X97U).

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

| Вузол                   | Призначення                                                  | Примітка |
| ----------------------- | ------------------------------------------------------------ | -------- |
| ![](media/inject.png)   | [Inject](base/1_4_1.md#inject-ініціювання-повідомлення) для ініціювання потоку (відправки повідомлення) користувачем, автоматично при запуску, або періодично. | +-       |
| ![](media/debug.png)    | [Debug](base/1_4_1.md#debug-вивести-на-відлагодження) використовуватися для відображення повідомлень на бічній панелі Debug у редакторі. | +-       |
| ![](media/complete.png) | [Complete]()                                                 |          |
| ![](media/catch.png)    | [Catch]()                                                    |          |
| ![](media/status.png)   | [Status](base/1_4_1.md#status-стан-вузлу)                    | +-       |
| ![](media/link-in.png)  | [Link in](base/1_4_1.md#link-in-та-link-out-посилання)       | +-       |
| ![](media/link-out.png) | [Link out](base/1_4_1.md#link-in-та-link-out-посилання)      | +-       |
| ![](media/comment.png)  | [Comment]()                                                  |          |
| ![](media/unknown.png)  | [Unknown]()                                                  |          |

### Функціональні (function)

| Вузол                   | Призначення                                                | Примітка |
| ----------------------- | ---------------------------------------------------------- | -------- |
| ![](media/function.png) | [Function](base/1_5.md)                                    | +-       |
| ![](media/switch.png)   | [Switch](base/1_4_1.md#switch-перемикач-повідомлення)      | +-       |
| ![](media/change.png)   | [Change](base/1_4_1.md#change-зміна-повідомлення-в-потоці) | +-       |
| ![](media/range.png)    | [Range](base/1_4_1.md#template-шаблон)                     | +-       |
| ![](media/template.png) | [Template]()                                               |          |
| ![](media/delay.png)    | [Delay](base/1_4_1.md#delay-затримка)                      | +-       |
| ![](media/trigger.png)  | [Trigger](base/1_4_1.md#trigger)                           | +-       |
| ![](media/exec.png)     | [Exec](base/1_4_1.md#exec-запуск-команди)                  | +-       |
| ![](media/rbe.png)      | [Rbe](base/1_4_1.md#rbe-гістерезис-нечутливість)           | +-       |

### Мережні (network)

| Вузол                             | Призначення            | Примітка |
| --------------------------------- | ---------------------- | -------- |
| ![](media/mqtt-in.png)            | [Mqtt in]()            |          |
| ![](media/mqtt-out.png)           | [Mqtt out]()           |          |
| ![](media/mqtt-broker.png)        | [Mqtt-broker]()        |          |
| ![](media/http-in.png)            | [Http-in]()            |          |
| ![](media/http-response.png)      | [Http response]()      |          |
| ![](media/http-request.png)       | [Http request]()       |          |
| ![](media/http-proxy.png)         | [Http proxy]()         |          |
| ![](media/tls-config.png)         | [Tls-config]()         |          |
| ![](media/websocket-in.png)       | [Websocket in]()       |          |
| ![](media/websocket-out.png)      | [Websocket out]()      |          |
| ![](media/websocket-listener.png) | [Websocket-listener]() |          |
| ![](media/websocket-client.png)   | [Websocket-client]()   |          |
| ![](media/tcp-in.png)             | [TCP in]()             |          |
| ![](media/tcp-out.png)            | [TCP out]()            |          |
| ![](media/tcp-request.png)        | [TCP request]()        |          |
| ![](media/udp-in.png)             | [UDP in]()             |          |
| ![](media/udp-out.png)            | [UPD out]()            |          |

### Послідовності (sequence)

| Вузол                | Призначення | Примітка |
| -------------------- | ----------- | -------- |
| ![](media/split.png) | [Split]()   |          |
| ![](media/join.png)  | [Join]()    |          |
| ![](media/sort.png)  | [Sort]()    |          |
| ![](media/batch.png) | [Batch]()   |          |

### Парсери (parser) 

| Вузол               | Призначення | Примітка |
| ------------------- | ----------- | -------- |
| ![](media/csv.png)  | [CSV]()     |          |
| ![](media/html.png) | [HTML]()    |          |
| ![](media/json.png) | [JSON]()    |          |
| ![](media/xml.png)  | [XML]()     |          |
| ![](media/yaml.png) | [YAML]()    |          |

### Сховища (storage) 

| Вузол                  | Призначення | Примітка |
| ---------------------- | ----------- | -------- |
| ![](media/file.png)    | [File]()    |          |
| ![](media/file-in.png) | [File in]() |          |
| ![](media/watch.png)   | [Watch]()   |          |
| ![](media/tail.png)    | [Tail]()    |          |

