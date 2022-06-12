**OPCUA-IIoT-Crawler**

**OPC UA IIoT Crawler**

Use the Crawler to browse OPC UA address spaces. It normally starts with a root folder or object by using an OPC UA Node-Id like i=85 (root->Objects), but that is not a good practice. Set up folders without crawling the server object and its types in depth. 

**[Configuration](http://127.0.0.1:1880/)**

The filter tab inside the configuration section is used to filter crawling by properties. You can set your own or use some of the listed properties. 

**[Examples](http://127.0.0.1:1880/)**

[GitHub Crawler example flow](https://github.com/biancode/node-red-contrib-iiot-opcua/blob/master/examples/)

You'll find the examples under Node-RED menu > Import > Examples > iiot opcua

**[Input](http://127.0.0.1:1880/)**

The input has to receive an addressSpaceItems (Array of objects) to browse for. A datatype or name is not required here - it just requires the nodeId in the addressSpaceItems objects here. 

Filter: 

- name => property name to search inside result per     item 
- value => regex string to match content 

**[Output](http://127.0.0.1:1880/)**

The output returns either a structured JSON object with the requested data or the error messages from node-opcua.

**Name** 

Name in the flow of Node-RED.

Set showErrors to get errors from node-opcua on browse. 

 