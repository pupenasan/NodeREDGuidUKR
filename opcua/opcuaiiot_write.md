# OPCUA-IIoT-Write

## OPC UA IIoT Write

The Write node is for sending data to the OPC UA server. It handles a single data request and multiple data requests. All write requests will produce an array of StatusCodes for writing in amount as applied for and responded. 

It needs a 

```
msg.valuesToWrite
```

to write values and datatypeName in the addressSpaceItems objects is required.

Every entry in the addressSpaceItems corresponding to each array place in msg.valuesToWrite. That means addressSpaceItem[0] will write the data from msg.valuesToWrite[0]! 

It is important to have the injectType write in the msg object! That is to protect your flow in event based flows.

### [Input](http://127.0.0.1:1880/)

- payload     (value to write one or all)
- topic
- addressSpaceItems     or nodesToWrite (Array of Node-Ids) 
- nodetype     (inject)
- injectType     (write) 
- valuesToWrite     (Array of values or objects to write individual)

### [Output](http://127.0.0.1:1880/)

Results in message:

- payload

- - statusCodes      (Array of Status Codes) 
  - nodesToWrite      (Array of Node-Id)

- topic 

- nodetype     (write)

- resultsConverted     (Array) 

Set showErrors to get errors from node-opcua on browse.