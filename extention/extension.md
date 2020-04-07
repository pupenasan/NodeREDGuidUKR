[<- На головну](../)

##  Розширення інших застосунків

Можна вставляти Node-RED у більший застосунок на `node.js`. Типовим сценарієм буде те, що ви використовуєте Node-RED для створення потоків даних, які ви хочете відображати на веб-панелі, - все з тієї ж програми.

Нижче наводиться мінімальний приклад вбудованого середовища виконання у ширшу програму Express.

```javascript
var http = require('http');
var express = require("express");
var RED = require("node-red");
 
// Create an Express app
var app = express();
 
// Add a simple route for static content served from 'public'
app.use("/",express.static("public"));
 
// Create a server
var server = http.createServer(app);
 
// Create the settings object - see default settings.js file for other options
var settings = {
    httpAdminRoot:"/red",
    httpNodeRoot: "/api",
    userDir:"/home/nol/.nodered/",
    functionGlobalContext: { }    // enables global context
};
 
// Initialise the runtime with a server and settings
RED.init(server,settings);
 
// Serve the editor UI from /red
app.use(settings.httpAdminRoot,RED.httpAdmin);
 
// Serve the http nodes UI from /api
app.use(settings.httpNodeRoot,RED.httpNode);
 
server.listen(8000);
 
// Start the runtime
RED.start();
```

Коли використовується такий підхід, тоді файл `settings.js` включений в Node-RED не використовується. Замість цього налаштування передаються викликом `RED.init` як показано вище. Крім того, ігноруються наступні параметри, оскільки вони залишаються для налаштування екземпляра Express:

- `uiHost`
- `uiPort`
- `httpAdminAuth`
- `httpNodeAuth`
- `httpStatic`
- `httpStaticAuth`
- `https`