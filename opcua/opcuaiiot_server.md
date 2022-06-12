# OPCUA-IIoT-Server

## OPC UA IIoT Server

The Server node is an OPC UA server with a simple optional information model (ASO Demo). The address space is to expand with the ASO nodes and commands are to send by the Command nodes. 

Default enpoint: opc.tcp://localhost:55388

Named enpoint: opc.tcp://localhost:55388/UA/NodeREDIIoTServer 

Default discovery: opc.tcp://localhost:4840/UADiscovery

all discovery: opc.tcp://localhost:4840/

### [Options](http://127.0.0.1:1880/)

If you need more information about all options read the node-opcua API, please!

The 'Delay On Close' is to close the server node with delay to all other nodes.

### [Certificates](http://127.0.0.1:1880/)

The server provides simple NodeOPCUA demo certificates and private keys.

You could set up your own certificate and private key files. This is optional.

### [User](http://127.0.0.1:1880/)

The user list is to set up users to the server. It is stored with Node-RED credentials best practice.

### [XML NodeSets](http://127.0.0.1:1880/)

That is static for now to add ISA95, DI, and Auto-ID to a server via XML NodeSet.

### [Discovery ](http://127.0.0.1:1880/)

That gives you access to the servers discovery node-opcua parameters.

Set showErrors to get errors from node-opcua on browse.

 