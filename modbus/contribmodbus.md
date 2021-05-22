### The all in one Modbus TCP and Serial contribution package for Node-RED (node-red-contrib-modbus).

[Сайт](https://flows.nodered.org/node/node-red-contrib-modbus)

#### modbus-client

![](media/mbclient.png)



#### modbus-response 

Вузол для відображення відповіді або тривалості відгуку з другого виходу вузлів Read/Write/Getter у статусі. Show-Max-Register - це межа, звідки вузол лише показує, скільки даних знаходиться у масиві відповідей. Цей вузол призначений лише для отримання деякої інформації, і не потрібен для роботи з вузлами Modbus Read/Write/Getter. Якщо Modbus Read/Write/Getter надсилає дані дуже швидко, будь ласка, не використовуйте цей вузол.

#### modbus-read

**Якщо у вас більше 10 вузлів в одній конфігурації зв'язку, використовуйте Modbus-Flex-Getter або подумайте про кілька підключень до вашого пристрою Modbus, будь ласка! Ви також можете проводити опитування за допомогою Modbus-Getter та Modbus-Flex-Getter, використовуючи вузол inject з вказаним інтервалом.**

Вузол зчитування Modbus TCP/Serial. Підключається до протоколу Modbus TCP або послідовного зчитування значень регістрів/котушок із заданою швидкістю опитування. Коди функцій, які зараз підтримуються, включають:

- FC 1: Read Coil Status 
- FC 2: Read Input Status  
- FC 3: Read Holding Registers 
- FC 4: Read Input Registers    

У спадному меню виберіть код функції (FC), оберіть початкову адресу  coil/input/register (0: 65535) та їх кількість, які слід прочитати з початкової адреси.

 Unit-Id (0..255 tcp |1..247 serial) - залиште порожнім, інакше він перевизначає типовий Unit-ID клієнтської конфігурації. 

Output 1: масив даних (PDU), буфер відповіді modbus, вхідне повідомлення

Output 2: буфер відповіді modbus, масив даних (PDU), вхідне повідомлення

#### modbus-getter

**Якщо у вас є більше 10 вузлів в одній конфігурації зв'язку, використовуйте Modbus-Flex-Getter або подумайте про кілька підключень до свого пристрою Modbus! **

Modbus TCP/Serial вузол із функцією зчитування за ініціювання входу. Підключається до Modbus TCP або serial для зчитування  coils/inputs/registers зі швидкістю вхідного повідомлення. На даний момент підтримуються коди функцій: 

- FC 1: Read Coil Status 
- FC 2: Read Input Status  
- FC 3: Read Holding Registers 
- FC 4: Read Input Registers    

Виберіть зі спадного меню код функції (FC), виберіть адресу (0: 65535) та кількість coil/input/register, які слід прочитати зі стартової адреси. Виберіть або відредагуйте конфігурацію з'єднання Modbus. Unit-Id (0..255 tcp | 1..247 serial) - залиште порожнім, інакше він перекриває типовий ідентифікатор Unit-налаштування клієнтського конфігурації. 

Встановіть частоту опитування (більшу за нуль) та одиницю часу. Виберіть або відредагуйте конфігурацію підключення Modbus.

Вихід 1: масив даних (PDU), буфер відповіді модуля, вхідне повідомлення 

вихід 2: modbus Буфер відповідей, масив даних (PDU), вхідне повідомлення

#### modbus-flex-getter

Вузол зчитування Modbus TCP, ініційований зчитуванням, із вхідними параметрами підключення. Підключається до Modbus TCP або serial для read coils/inputs/registers зі швидкістю вхідних повідомлень. Коди функцій (1: 4), які зараз підтримуються, включають:

- FC 1: Read Coil Status 
- FC 2: Read Input Status 
- FC 3: Read Holding Registers 
- FC 4: Read Input Registers     

**Вхідні параметри для підключення Modbus**   

- unitid (0..255 tcp | 1..247 serial) - overrides default Unit-ID 
- fc (1..4) 
- start address (0:65535) 
- quantity (1:65535) of coils/inputs/registers to be read from the start address    

Output 1: data Array (PDU), modbus response Buffer, input message  

Output 2: modbus response Buffer, data Array (PDU), input message 

Приклад коду вузла функції для одиночного читання:

```js
msg.payload = { value: msg.payload, 'fc': 1, 'unitid': 1, 'address': 0 , 'quantity': 1 } return msg
```

Приклад коду вузла функції для множинного читання:

```js
msg.payload = { value: msg.payload, 'fc': 3, 'unitid': 1, 'address': 0 , 'quantity': 10 } return msg
```

#### modbus-write

**Якщо у вас більше 10 вузлів на одній конфігурації зв'язку, використовуйте Modbus-Flex-Writer або подумайте про кілька підключень до вашого пристрою Modbus, будь ласка!**

Modbus TCP/Serial вузол спрацьовує при поданні на нього **msg.payload** для запису.

Підключається до Modbus TCP або serial для запису coils/registers на кожну вхідну msg.

Коди функцій, які зараз підтримуються, включають:

- FC 5: Force Single Coil 
- FC 6: Preset Single Register 
- FC 15: Force Multiple Coils 
- FC 16: Preset Multiple Registers    

У спадному меню виберіть код функції (FC), оберіть початкову адресу coil/register (0: 65535) та кількість, яку потрібно записати. Виберіть або відредагуйте конфігурацію Modbus TCP/serial сервер, щоб вказати сервер для підключення.

Unit-Id (0..255 tcp | 1..247 serial) -  залиште порожнім, інакше він замінює типовий Unit-ID клієнтської конфігурації

For FC 5, **msg.payload** must be a value of 1 or 0 or true or false. 

For FC 15,  **msg.payload** must be an array[] of comma separated values true or false each. 

For FC 6, **msg.payload** must be a single value between 0:65535. 

For FC 16, **msg.payload** must be an array[] of comma separated values between 0:65535 each.  

Output 1: all given data, modbus response Buffer, input message  

Output 2: modbus response Buffer, all given data, input message 

#### modbus-flex-write

Вузол запису, що запускається за допомогою гнучкого введення Modbus TCP, із вхідними параметрами з'єднання.

Підключається до Modbus TCP або serial для запису coils/registers на кожну вхідну msg.

Коди функцій, які зараз підтримуються, включають:

- FC 5: Force Single Coil 
- FC 6: Preset Single Register 
- FC 15: Force Multiple Coils 
- FC 16: Preset Multiple Registers     

**Вхідні параметри для підключення Modbus**   

- unitid (0..255 tcp | 1..247 serial) - overrides default Unit-ID 
- fc (5|6|15|16) 
- start address (0:65535) 
- quantity (1:65535) of coils/inputs/registers to be written from the start address    

For FC 5, **msg.payload** must be a value of 1 or 0 or true or false. 

For FC 6, **msg.payload** must be a single value between 0:65535. 

For FC 16, **msg.payload** must be an array[] of comma separated values between 0:65535 each.   

Output 1: all given data, modbus response Buffer, input message  

Output 2: modbus response Buffer, all given data, input message 

Function node code example for single write: 

```js
msg.payload = { value: msg.payload, 'fc': 5, 'unitid': 1, 'address': 0 , 'quantity': 1 }
return msg
```

Function node code example for multiple write:

```js
msg.payload = {value: msg.payload, 'fc': 15, 'unitid': 1, 'address': 0 , 'quantity': 10 } 
return msg
```

#### modbus-server

Вузол для надання сервера тестування Modbus TCP на основі node-modbus (jsmodbus) для тестування.

Після ін'єкції сервер надсилає буфери на окремі виходи

Ви можете використовувати вузли запису Modbus (FC) для запису даних у буфери сервера.

Ви можете використовувати вузли читання Modbus (FC) для зчитування даних із буферів сервера.

Output 1: holding Buffer, type, msg 

Output 2: coils Buffer, type, msg 

Output 3: input Buffer, type, msg  

Output 4: discrete Buffer, type, msg 

Input: 

При введенні спеціального корисного навантаження ви можете писати безпосередньо в будь-який register. Це слід використовувати, лише якщо ви хочете імітувати клієнт Modbus.

```js
msg.payload = { 'value': msg.payload, 'register': 'holding', 'address': 1 , 'disableMsgOutput' : 0 }; 
return msg;
```

The value could also be a list of UInt8 numbers and they will be written to the buffer. 

 Valid registers are:  

- holding 
- coils 
- input 
- discrete  

Set disableMsgOutput if you want to disable the Server outputs when injecting. 

#### modbus-flex-server

Вузол для забезпечення гнучкого сервера протоколу Modbus TCP на основі modbus-serial для тестування.

Пакет modbus-serial дозволяє налаштовувати/вводити код для обробки запитів modbus. Завдяки цьому ви можете створити свій персональний сервер Modbus. Кадр функцій виправлений - лише сукупність функцій є гнучкою.

Після ін’єкції сервер надсилає буфери на окремі виходи. Ви можете використовувати вузли запису Modbus (FC) для запису даних у буфери сервера.

You can use the Modbus read nodes (FC) to read data from the server buffers. 

Output 1: holding Buffer, type, msg 

Output 2: coils Buffer, type, msg 

Output 3: input Buffer, type, msg  

Output 4: discrete inputs Buffer, type, msg 

Input: On injecting a special payload, you can write directly to any  register. This should only be used if you want to simulate a Modbus  client.  

```js
msg.payload = { 'value': msg.payload, 'register': 'holding', 'address': 1 , 'disableMsgOutput' : 0 }; return msg;
```

The value could also be a list of UInt8 numbers and they will be written to the buffer.  

Valid registers are:  

- holding 
- coils 
- input 
- discrete  

Set disableMsgOutput if you want to disable the Flex Server outputs when injecting. 

#### modbus-queue-info

**Черга встановлюється на unit - встановіть unit-id, щоб отримати потрібну інформацію.**

Вузол інформації про чергу TCP/Serial черги.

Unit-Id (0..255 tcp | 1..247 serial) 

Use inject of 

`msg.resetQueue = true` 

to reset the queue. 

Reset on high level to connect with the catch node 

```json
[{"id":"430f76bf.9de2d8","type":"function","z":"b245d3e4.b52de","name":"reset on High",
"func":"if(\"high level reached\" === msg.state) {\n    msg.payload.resetQueue = true;\n    return msg;\n}\n","outputs":1,"noerr":0,"x":410,"y":140,"wires":[["64cca59a.dc295c"]]}]
```

 Reset on high high level to connect with the catch node  

```json
[{"id":"fc74491.2ddc9b8","type":"function","z":"b245d3e4.b52de","name":"reset on HighHigh","func":"if(\"high high level reached\" === msg.state) {\n    msg.payload.resetQueue = true;\n return  msg;\n}\n","outputs":1,"noerr":0,"x":430,"y":180,"wires":[["64cca59a.dc295c"]]}] 
```

An update of all unit queues can be watched by checking the option. Use just a single queue info per client if you activate that option.  

"Error on high level" with that option the node sends an error if high level is reached and on high high level. 

With reaching the high level there comes a warning and with the high high an error for work with the catch node 

Output: all queue information - use complete msg with debug 

#### modbus-flex-connector

Modbus Flex Connector є вузлом для гнучких вхідних тригерів для повторного підключення до нових параметрів з'єднання.

`msg.payload.connectorType = 'TCP' || 'SERIAL'`  

**TCP options**

- msg.payload.tcpHost || node.tcpHost 
- msg.payload.tcpPort || node.tcpPort  
- msg.payload.tcpType || node.tcpType 
- msg.payload.unitId || node.unit_id  
- msg.payload.commandDelay || node.commandDelay 
- msg.payload.clientTimeout || node.clientTimeout  
- msg.payload.reconnectTimeout| || node.reconnectTimeout    

**SERIAL options**   

- msg.payload.serialPort || node.serialPort 
- msg.payload.serialBaudrate || node.serialBaudrate  
- msg.payload.serialDatabits || node.serialDatabits 
- msg.payload.serialStopbits || node.serialStopbits 
- msg.payload.serialParity || node.serialParity 
- msg.payload.serialType || node.serialType  
- msg.payload.serialConnectionDelay || node.serialConnectionDelay 
- msg.payload.unitId || node.unit_id  
- msg.payload.commandDelay || node.commandDelay 
- msg.payload.clientTimeout || node.clientTimeout  
- msg.payload.reconnectTimeout || node.reconnectTimeout    

Function node code examples for TCP: 

```js
msg.payload = { 'connectorType': 'TCP', 'tcpHost': '127.0.0.1', 'unitId': 2 } 
return msg 
```

```js
msg.payload = { 'connectorType': 'TCP', 'tcpHost': '127.0.0.1', 'tcpPort': '10502' 'unitId': 2 } 
return msg
```

Function node code example for SERIAL:

```js
msg.payload = { 'connectorType': 'SERIAL', 'serialPort': '/dev/USB02', 'serialBaudrate': '9600' 'unitId': 2 } return msg
```

#### modbus-response-filter

Фільтр відповідей призначений для роботи з файлом IO для фільтрації значень з IO-Payload  за іменем.

Спочатку розгорніть, щоб скористатися кнопкою пошуку! Вам потрібен робочий IO-File-Config для пошуку.