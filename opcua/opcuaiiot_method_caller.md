# OPCUA-IIoT-Method-Caller

## OPC UA IIoT Method Caller

The Node is to call a basic or complex method on the OPC UA server.

### [Input ](http://127.0.0.1:1880/)

If the settings of the node are filled, then a simple inject will work, otherwise the incoming has to receive a complex message with all parameters. 

You need to add your XML definition of types and attributes to the server.

**Simple event message payload could be a simple inject if the node parameters are filled or you have to send the parameters via msg object like:** 

```
msg.payload.
```

- objectId     (Object-Id) 

- methodId     (Method-Id) 

- inputArguments     (Array) 

- - name      (just to name the method parameter - has no effect to later use for now) 
  - dataType      (all node-opcua DataTypes) 
  - value      (value or Variant as expected from node-opcua) 

- methodType     (basic, complex) 

The settings in that node will override incoming data if the msg property is empty or undefined.

**Complex event message:**

- objectId     (Object-Id) 

- methodId     (Method-Id) 

- inputArguments     (Array) 

- - dataType      
  - value      

- methodType     

- nodetype     

### [Output](http://127.0.0.1:1880/)

**Event message:**

- payload     (Array) 

- - statusCode      
  - inputArgumentResults      (Array) 
  - inputArgumentDiagnosticInfos      (Array) 
  - outputArguments      (Array) 

- definitionResults     

- - methodId      
  - methodDefinition      

- nodetype     (method) 

- methodType     

**Name** 

Name in the flow of Node-RED.

Set showErrors to get errors from node-opcua on browse.

 