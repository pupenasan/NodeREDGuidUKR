[<- На головну](../)

## Створення власних вузлів ([Creating Nodes](https://nodered.org/docs/creating-nodes/))

The main way Node-RED can be extended is to add new nodes into its palette.

The following sections exist and are largely complete:

- [Створення першого вузлу](creatfirst.md)
- [JavaScript File](creatjs.md)
- [HTML File](creathtml.md)
- [Node context](creatcontext.md)
- [Node properties](creatprop.md)
- [Node appearance](createapp.md)
- [Node status](creatstat.md)
- [Configuration      nodes](creatconfig.md)
- [Help style      guide](creathelp.md)
- [Example flows](createxamp.md)
- [Packaging](creatpack.md)
- [Internationalisation](creatintern.md)

### Загальне керівництво

Існують деякі загальні принципи, які слід дотримуватися при створенні нових вузлів. Вони відображають підхід, який приймають основні вузли, і допомога, яка забезпечує послідовний досвід користувачів. Вузли повинні:

•     **бути чітко означеними у своїй меті**: вузол, який надає всі можливі варіанти API, є потенційно менш корисним, ніж група вузлів, кожен з яких виконує одну ціль.

•     **бути простим у використанні, незалежно від базової функціональності:** приховуйте складність і уникайте використання жаргону або знань, специфічних для певної галузі.

•     **бути простим у тому, які типи повідомлень приймаються:** властивості повідомлень можуть бути рядками, числами, булевими, буферами, об'єктами, масивами або nulls. Вузол повинен робити правильний вибір, коли стикається з будь-яким з них.

•     **бути послідовними в тому, що вони надсилають**: вузли повинні документувати ті властивості, які вони додають до повідомлень, і вони повинні бути послідовними та передбачуваними у своїй поведінці.

•     **розміщуватись на початку, в середині або в кінці потоку - не усюди відразу.**

•     **виловлювати помилки**: якщо вузол викидає помилку, що припиняється, Node-RED зупинить весь потік, оскільки стан системи більше не відомий. Там, де це можливо, вузли повинні ловити помилки або реєструвати обробники помилок для будь-яких асинхронних викликів.

### Створення першого вузлу 

Вузли створюються тоді, коли розгортається потік (flow is deployed). Після цього, поки потік запущений, вони можуть відправляти і отримувати деякі повідомлення. При розгортанні наступного потоку вони видаляються.

Зазвичай вузли складаються з пари файлів: 

•     файл JavaScript, який означує, що робить вузол, 

•     файл html, який означує властивості вузла, діалогове вікно редагування та текст довідки.

Файл `package.json` використовується для того, щоб упакувати все разом як модуль npm.      

#### Створення простого вузлу 

У цьому прикладі буде показано, як створити вузол, який перетворює корисні навантаження на всі символи нижнього регістру. Переконайтеся, що у вашій системі встановлено рекомендовану версію LTS для Node.js. На момент написання цієї статті це версія **LTS 8.x**, яка містить версію npm 5.x.

Створіть директорію, в якій ви будете розробляти свій код. У цій директорії створіть такі файли:

- `package.json`
- `lower-case.js`
- `lower-case.html`

##### package.json

Це стандартний файл, який використовується модулями Node.js для опису їхнього вмісту. Для створення стандартного файлу `package.json` можна використовувати команду `npm init`. Це згенерує ряд запитань, які допоможуть створити початковий вміст файлу, використовуючи розумні значення за замовчуванням. Коли буде запропоновано, вкажіть ім'я `node-red-contrib-example-lower-case`.

Після генерування потрібно додати секцію `node-red`:

```json
{
    "name" : "node-red-contrib-example-lower-case",
    ...
    "node-red" : {
        "nodes": {
            "lower-case": "lower-case.js"
        }
    }
}
```

Це вказує середовищу виконання, які файли вузлів містить модуль. Додаткову інформацію про те, як упакувати ваш вузол, включаючи вимоги до імен та інших властивостей, які слід встановити перед публікацією вашого вузла, див. [packaging guide](https://nodered.org/docs/creating-nodes/packaging).

Примітка. Будь ласка, ***не*** публікуйте цей приклад вузла до npm!

##### lower-case.js

```js
module.exports = function(RED) { //RED - змінна доступу до Node-RED API
    function LowerCaseNode(config) {
        RED.nodes.createNode(this,config);
        var node = this;
        node.on('input', function(msg) {
            msg.payload = msg.payload.toLowerCase();
            node.send(msg);
        });
    }
    RED.nodes.registerType("lower-case",LowerCaseNode);
}
```

Вузол обгортається як модуль Node.js. Модуль експортує функцію, яка викликається тоді, коли під час запуску середовище виконання завантажує вузол. Функція викликається з єдиним аргументом, `RED`, який надає модулю доступ до Node-RED runtime api.

Сам вузол означується функцією `LowerCaseNode`, яка викликається при створенні нового екземпляра вузла. Він передається об'єкту, що містить специфічні для вузла властивості, задані в редакторі потоків. Функція викликає функцію `RED.nodes.createNode` для ініціалізації функцій, спільних для всіх вузлів. Після цього виконується код, специфічний для вузла.

У цьому прикладі вузол реєструє слухача (listener) до події `input`, яка викликається, коли повідомлення надходить на вузол. У цьому слухачеві він змінює payload на нижній регістр, потім викликає функцію відправки, щоб передавати повідомлення по потоку. Нарешті, функція `LowerCaseNode` зареєстрована у середовищі виконання з використанням імені для вузла, `lower-case`. Якщо вузол має будь-які зовнішні модульні залежності, вони повинні бути включені в розділ залежностей файлу `package.json`.

Додаткову інформацію про частину вузла виконання можна знайти [тут](https://nodered.org/docs/creating-nodes/node-js).

##### lower-case.html

```html
<script type="text/javascript">
    RED.nodes.registerType('lower-case',{
        category: 'function',
        color: '#a6bbcf',
        defaults: {
            name: {value:""}
        },
        inputs:1,
        outputs:1,
        icon: "file.png",
        label: function() {
            return this.name||"lower-case";
        }
    });
</script>
<script type="text/x-red" data-template-name="lower-case">
    <div class="form-row">
        <label for="node-input-name"><i class="icon-tag"></i> Name</label>
        <input type="text" id="node-input-name" placeholder="Name">
    </div>
</script>
<script type="text/x-red" data-help-name="lower-case">
    <p>A simple node that converts the message payloads into all lower-case characters</p>
</script>
```

Файл HTML у вузлі містить наступні речі:

•     означення основного вузла, зареєстрованого редактором

•     шаблон редагування

•     текст довідки

У цьому прикладі вузол має єдину властивість для редагування, `name`. Хоча це і не потрібно, існує широко використовувана конвенція для цієї властивості, яка допомагає розрізняти декілька екземплярів вузла в одному потоці.

Докладнішу інформацію про редакторську частину вузла див. [Тут](https://nodered.org/docs/creating-nodes/node-html).

#### Testing your node in Node-RED

Once you have created a basic node module as described above, you can install it into your Node-RED runtime.

To test a node module locally using npm 5.x, the [`npm install `](https://docs.npmjs.com/cli/install) command can be used. This allows you to develop the node in a local directory and have it linked into a local node-red install during development.

In your node-red user directory, typically `~/.node-red`, run:

```bash
npm install <location of node module>
```

For example, on Mac OS or linux, if your node is located at `~/dev/node-red-contrib-example-lower-case` you would type the following:

```bash
cd ~/.node-red
npm install ~/dev/node-red-contrib-example-lower-case
```

This creates a symbolic link to your node module project directory in `~/.node-red/node_modules` so that Node-RED will discover the node when it starts. Any changes to the node’s file can be picked up by simply restarting Node-RED. On Windows, again, using npm 5.x or greater:

```bash
cd C:\Users\my_name\.node_red
npm install C:\Users\my_name\Documents\GitHub\node-red-contrib-example-lower-case
```

If you are using an older version of npm, you can create a symbolic link manually to your project. For example, on Mac or linux systems:

```bash
cd ~/.node-red/node_modules
ln -s ~/dev/node-red-contrib-example-lower-case  .
```

On Windows with older versions of npm, use `mklink` instead:

```bash
cd C:\Users\my_name\.node_red
mklink /D node_modules\node-red-contrib-example-lower-case C:\Users\my_name\Documents\GitHub\node-red-contrib-example-lower-case
```

*Note* : npm 5 will add your module as a dependency in the `package.json` file located in your user directory. If you want to prevent this, use the npm `--no-save` option. 

### Unit Testing

To support unit testing, an npm module called [`node-red-node-test-helper`](https://www.npmjs.com/package/node-red-node-test-helper) can be used. The test-helper is a framework built on the Node-RED runtime to make it easier to test nodes.

Using this framework, you can create test flows, and then assert that your node properties and output is working as expected. For example, to add a unit test to the lower-case node you can add a `test` folder to your node module package containing a file called `_spec.js`

#### test/_spec.js

```js
var should = require("should");
var helper = require("node-red-test-helper");
var lowerNode = require("../lower-case.js");
 
describe('lower-case Node', function () {
 
  afterEach(function () {
    helper.unload();
  });
 
  it('should be loaded', function (done) {
    var flow = [{ id: "n1", type: "lower-case", name: "test name" }];
    helper.load(lowerNode, flow, function () {
      var n1 = helper.getNode("n1");
      n1.should.have.property('name', 'test name');
      done();
    });
  });
 
  it('should make payload lower case', function (done) {
    var flow = [{ id: "n1", type: "lower-case", name: "test name",wires:[["n2"]] },
    { id: "n2", type: "helper" }];
    helper.load(lowerNode, flow, function () {
      var n2 = helper.getNode("n2");
      var n1 = helper.getNode("n1");
      n2.on("input", function (msg) {
        msg.should.have.property('payload', 'uppercase');
        done();
      });
      n1.receive({ payload: "UpperCase" });
    });
  });
});
```

These tests check to see that the node is loaded into the runtime correctly, and that it correctly changes the payload to lower case as expected.

Both tests load the node into the runtime using `helper.load` supplying the node under test and a test flow The first checks that the node in the runtime has the correct name property. The second test uses a helper node to check that the output from the node is, in fact, lower case.

The helper module contains other examples of tests taken from the Node-RED core nodes. For more information on the helper module, see the associated README.

[<- На головну](../)