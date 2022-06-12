## node-red-contrib-iiot-opcua

<https://github.com/BiancoRoyal/node-red-contrib-iiot-opcua>

The IoT/IIoT OPC UA toolbox package for Node-RED based on [node-opcua](https://github.com/node-opcua/node-opcua).

| Вузол                                                        | Призначення                                                  | Примітка |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- |
| ![image-20220610235755971](media1/image-20220610235755971.png) | [opcuaiiot_connector](opcuaiiot_connector.md) - конфігураційний вузол підключення до сервера OPC UA | 2022     |
| ![image-20220610235814261](media1/image-20220610235814261.png) | [opcuaiiot_browser](opcuaiiot_browser.md)                    |          |
| ![image-20220610235826749](media1/image-20220610235826749.png) | [opcuaiiot_inject](opcuaiiot_inject.md) - фомування msg для інших вузлів бібліотеки |          |
| ![image-20220610235837651](media1/image-20220610235837651.png) | [opcuaiiot_discovery](opcuaiiot_discovery.md)                |          |
| ![image-20220610235857187](media1/image-20220610235857187.png) | [opcuaiiot_event](opcuaiiot_event.md)                        |          |
| ![image-20220610235907143](media1/image-20220610235907143.png) | [opcuaiiot_listener](opcuaiiot_listener.md) - налаштування моніторингу адресного простору або Alarm&Events |          |
| ![image-20220610235919546](media1/image-20220610235919546.png) | [opcuaiiot_read](opcuaiiot_read.md)                          |          |
| ![image-20220610235928879](media1/image-20220610235928879.png) | [opcuaiiot_write](opcuaiiot_write.md)                        |          |
| ![image-20220610235938885](media1/image-20220610235938885.png) | [opcuaiiot_response](opcuaiiot_response.md)                  |          |
| ![image-20220610235948830](media1/image-20220610235948830.png) | [opcuaiiot_crawler](opcuaiiot_crawler.md)                    |          |
| ![image-20220611000001500](media1/image-20220611000001500.png) | [opcuaiiot_flex_connector](opcuaiiot_flex_connector.md)      |          |
| ![image-20220611000011916](media1/image-20220611000011916.png) | [opcuaiiot_flex_server](opcuaiiot_flex_server.md)            |          |
| ![image-20220611000021811](media1/image-20220611000021811.png) | [opcuaiiot_method_caller](opcuaiiot_method_caller.md)        |          |
| ![image-20220611000036131](media1/image-20220611000036131.png) | [opcuaiiot_server](opcuaiiot_server.md)                      |          |
| ![image-20220611000047854](media1/image-20220611000047854.png) | [opcuaiiot_node](opcuaiiot_node.md) - налаштування параметрів Node для інших вузлів OPC |          |
| ![image-20220611000058212](media1/image-20220611000058212.png) | [opcuaiiot_server_aso](opcuaiiot_server_aso.md)              |          |
| ![image-20220611000107882](media1/image-20220611000107882.png) | [opcuaiiot_server_command](opcuaiiot_server_command.md)      |          |
| ![image-20220611000118629](media1/image-20220611000118629.png) | [opcuaiiot_result_filter](opcuaiiot_result_filter.md)        |          |

### Basic Flow

![Flow Example](media1/browser-listener-flow3-active.png)

### Ваша власна модель адресного простору!

За допомогою flex-сервера ви можете створити власну інформаційну модель з адресним простором OPC UA.

![Flex server Example](media1/flexServerAddressSapceExamplev3.png)

### Вчіться на прикладах!

Вузол сервера містить демонстраційні об’єкти та змінні, щоб почати гру з операціями виклику методу OPC UA, читання та запису.

див Node-RED menu (right upper corner) -> Import -> Examples -> iiot opcua



![Flow Example](media1/method-call3-active.png)

**... безпечне зчитування з серверів OPC UA з вашими власними парами ключів ...**

![Read Example](media1/read-history3-active.png)

**... і безпечне записування та переміщення даних між серверами OPC UA...**

![Write Example](media1/write-flow3-active.png)

![Read Write Example](media1/write-read-flow3.png)

**... створювати власні змінні та об’єкти з подій ...**

| Node-RED                                    | UAExpert / Client                                    |
| ------------------------------------------- | ---------------------------------------------------- |
| ![ASO Example](media1/server-aso-flow3.png) | ![ASO UAExpert](media1/ASOTestVariablesUAExpert.png) |

### Повторне підключення через події за допомогою Flex Connector! 

![Flow Flex Connector](media1/flex-connector-flow31.png)

## 