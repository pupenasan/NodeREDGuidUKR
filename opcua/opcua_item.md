[<- На головну](../)  [Розділ](README.md)

## OpcUa-Item

![img](media/opcua_item.png)Означує OPC UA item, тип і значення у зручному вигляді. По суті даний елемент формує для OpcUA-Client повідомлення у зручному вигляді. 

Поле Item містить адресу NodeID вузла OPC UA. Поле Type вказує на необхідний тип. Наразі не всі типи можливі, але деякі з них можна вибрати. У поле Value вказується значення, воно потрібне, лише якщо на сервер OPC UA потрібно записувати значення елементу. 

![img](media/16_11.png)

рис.16.11. Налаштування OpcUa-Item

Можна добавити `Item` до клієнту а потім проводити групові операції, наприклад читання. Приклад потоку [за посиланням](https://github.com/mikakaraila/node-red-contrib-opcua/blob/master/examples/OPCUA_READMULTIPLE.json)

https://github.com/mikakaraila/node-red-contrib-opcua/blob/master/examples/OPCUA-TEST-NODES.json