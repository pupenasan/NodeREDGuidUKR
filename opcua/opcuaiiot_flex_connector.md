## OPC UA IIoT Flex Connector

Вузол Flex Connector має налаштувати прослуховувач подій з параметрами, щоб змінити налаштування зв’язаного з’єднувача та перезапустити з’єднання. Він запускається за допомогою Inject Node-RED або IIoT OPC UA Inject. Він також може отримати тригер з вхідними подіями з інших вузлів.

### Input

Вузол приймає параметри з об’єкта msg або з параметрів вузла за замовчуванням. Це означає, що порожній об’єкт msg просто скине з’єднання і схожий на команду, щоб просто перезапустити конектор з параметрами вузла.

msg with connector parameters

- endpoint (string with opc.tcp://) 
- keepSessionAlive (boolean) 
- securityPolicy (string) 
- securityMode (string) 
- name (string) 
- showErrors (boolean) 
- publicCertificateFile (path string) 
- privateKeyFile (path string) 
- defaultSecureTokenLifetime (number) 
- endpointMustExist (boolean) 
- autoSelectRightEndpoint (boolean) 
- strategyMaxRetry (number) 
- strategyInitialDelay (number) 
- strategyMaxDelay (number) 
- strategyRandomisationFactor (float from 0 .. 1) 
- requestedSessionTimeout (number) 
- connectionStartDelay (number) 
- reconnectDelay (number) 

[Output](http://127.0.0.1:1880/)

A msg object with connector parameters and a result if the restart with new settings was done.

Name 

Name in the flow of Node-RED.

 