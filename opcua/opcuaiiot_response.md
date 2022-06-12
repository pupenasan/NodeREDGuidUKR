## OPC UA IIoT Response

There is a compress option to get compressed data with less optional data in msg objects.

The Response node shows you the response data from your request in categories of Good, Bad, and Other.

Існує опція стиснення, щоб отримати стислі дані з меншою кількістю необов’язкових даних в об’єктах msg.

Вузол «Відповідь» показує дані відповіді з вашого запиту в категоріях  Good, Bad та Other.

### [Input ](http://127.0.0.1:1880/)

Output message from client nodes like Read, Write, Listener, and Browser

### [Output](http://127.0.0.1:1880/)

The output is the input message including the entry status Array ( msg.entryStatus [Good, Bad, Other]).

Set showErrors to get errors from node-opcua on browse.

 