[<- На головну](../)

# 16. Бібліотека OPC UA 

Бібліотека на [Git](https://github.com/mikakaraila/node-red-contrib-opcua)

https://flows.nodered.org/node/node-red-contrib-opcua

Опис специфікацій OPC UA доступні на офіційному сайті [OPC Foundation](https://opcfoundation.org/). 

Короткий опис українською наведений у [Вступ до OPC UA](https://drive.google.com/file/d/1nZCjvvyf9STbZ5WIol7bWEhZQidGT3GE/view?fbclid=IwAR0XYTzV2EVrOw_T7S4vagL8kbPw7lbwyZC5gXTzs22c8BjgVvw3Um-5uGk)

Короткий огляд OPC UA англійською наведений в [OPC UA Fundamentals](https://documentation.unified-automation.com/uasdkcpp/1.5.6/html/L1OpcUaFundamentals.html?fbclid=IwAR06ZJqbeDdcgcerx8HizRK8uhGP6f5MMwhcLYDgYD8tfhbDl85mvQzlcm0)

Для перевірки роботи OPC UA рекомендуємо завантажити безкоштовні утиліти:

- [UaExpert](https://www.unified-automation.com/downloads/opc-ua-clients.html) - це повнофункціональний клієнт     OPC UA, який може працювати з декількома профілями та функціями OPC UA.
- [OPC UA C++ Demo Server](https://www.unified-automation.com/downloads/opc-ua-servers/file/download/details/opc-ua-c-demo-server-v163-windows.html) – тестовий     OPC Unified Architecture Server для операційних систем     Windows (XP, Vista, 7, 8, 10), в якому імітуються дані та інформаційна     модель (Standard, DI та PLCopen).

Також в Інтернеті доступні онлайн клієнти та сервери, зокрема:

- https://www.uaclient.com/ - [OPC UA Web Client](https://www.uaclient.com/about.html) by [One-Way Automation](http://www.onewayautomation.com) 
- opc.tcp://opcuaserver.com:48010
- [інші сервери в Інтернеті](https://github.com/node-opcua/node-opcua/wiki/publicly-available-OPCUA-servers)

Для роботи принаймні OpcUA-Server’а Node-RED необхідно запускати з робочої папки користувача!

У довіднику навдений опис вузлів [node-red-contrib-opcua](https://flows.nodered.org/node/node-red-contrib-opcua):

- [OpcUa-Endpoint](opcua_endpoint.md)<span class="load"> </span>
- [OpcUa-Client](opcua_client.md)<span class="load"> </span>
- [OpcUa-Item](opcua_item.md)<span class="load"> </span>
- [OpcUa-Event](opcua_event.md)<span class="load"> </span>
- [OpcUa-Server](opcua_server.md)<span class="load"> </span>

Також є вузли для [OPC DA](https://flows.nodered.org/node/node-red-contrib-opc-da)