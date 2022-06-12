**OPCUA-IIoT-Flex-Server**

**OPC UA IIoT Flex Server**

The Flex Server node is an OPC UA server with a flexible address space to build your own information model. The address space is to expand with JS based on node-opcua API. The Flex Server did not work with ASO requests, but it works also with the Command node. 

Default enpoint: opc.tcp://localhost:55380/

Named enpoint: opc.tcp://localhost:55380/UA/NodeREDFlexIIoTServer

Default discovery: opc.tcp://localhost:4840/UAFlexDiscovery

all discovery: opc.tcp://localhost:4840/

**[Options](http://127.0.0.1:1880/)**

If you need more information about all options read the node-opcua API, please!

The 'Delay On Close' is to close the server node with delay to all other nodes.

**[Certificates](http://127.0.0.1:1880/)**

The server provides simple NodeOPCUA demo certificates and private keys.

You could set up your own certificate and private key files. This is optional.

**[User](http://127.0.0.1:1880/)**

The user list is to set up users to the server. It is stored with Node-RED credentials best practice.

**[XML NodeSets](http://127.0.0.1:1880/)**

That is static for now to add ISA95, DI, and Auto-ID to a server via XML NodeSet.

**[AddressSpace](http://127.0.0.1:1880/)**

A function like programming editor to construct your own flexible address space in the server.

**[Discovery](http://127.0.0.1:1880/)**

That gives you access to the servers discovery node-opcua parameters.

Set showErrors to get errors from node-opcua on browse.

 