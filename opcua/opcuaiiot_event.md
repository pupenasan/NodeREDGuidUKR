**OPCUA-IIoT-Event**

**OPC UA IIoT Event**

The Event node is to set up an event listener with parameters. It is to trigger by an Inject of Node-RED or by the OPC UA IIoT Inject. It could also trigger with incoming events from other nodes. 

**[Input](http://127.0.0.1:1880/)**

msg with addressSpaceItems

**[Output](http://127.0.0.1:1880/)**

**Event message:** 

- payload (number/Object) 

- - eventType (ObjectTypeId) 

  - eventFilter (Array of conditions or events) 

  - - selectClause (Array) 
    - whereClause (Object) 

  - eventFields (Array) 

  - queueSize (counter) 

  - interval (number msec.) 

  - - topic 
    - nodetype (events) 

**Name** 

Name in the flow of Node-RED.

 