# Node-RED Dashboard Template Examples (AngularJS)

[Посилання на оригінал](https://it.knightnet.org.uk/kb/nr-qa/dashboard-template-examples/#a-couple-of-ways-to-send-a-msg-back-to-node-red)

> Деякі приклади використання AngularJS з Node-RED Dashboard. Не всі функції Angular доступні за допомогою Dashboard

## Доступ до msg object

To access the `msg` object from within a client Angular script. Put this into a Dashboard Template node:

При використанні Dashboard сервер Node-RED (back end) надсилає дані через Socket.IO до клієнтського браузера (front end). Це відбувається у вигляді об'єкта `msg`. у подібній формі до повідомлення, яке протікає через решту Node-RED.

Щоб отримати доступ до об’єкта `msg` з клієнтського сценарію Angular помістіть це у вузол Dashboard Template:

```html
<div ng-bind-html="msg.payload"></div>
<script>
    //console.dir(scope) // це також працює
    //console.dir(scope.msg) // це ні, бо scope.msg ще не існує

    // Lambda function для доступу до Angular Scope
    ;(function(scope) {
        //console.log('--- SCOPE ---')
        //console.dir(scope) // це працює, але Ви можете отримати його тільки один раз (при запуску)
        //console.dir(scope.msg) // не працює бо scope.msg ще не існує
        //Щоб отримати нові вхідні повідомлення, потрібно використовувати $watch
        scope.$watch('msg.payload', function(newVal, oldVal) {
            console.log('- Scope.msg -')
            console.dir(scope.msg)
        })
    })(scope)
</script>
```

## Кілька способів надіслати повідомлення назад до Node-RED

Це показує, як налаштувати деякі кнопки та віджет повзунка, які надсилають дані назад до Node-RED. Як завжди, додайте цей код до вузла Dashboard Template.

```html
<div>{{msg.payload}}</div>

<md-button ng-click="send({payload: 'Hello World'})">
    Натисни мене для відправки hello world
</md-button>

<md-slider ng-model="msg.payload" ng-change="send(msg)"></md-slider>

<div flex layout="row" layout-align="space-around center">
    <md-button ng-repeat="b in buttons" class="md-icon-button" ng-click="click(b)">
        <ng-md-icon icon="{{msg.payload[b.payload]?b.icon2:b.icon}}"
                    ng-style="{color: msg.payload[b.payload]?b.color2:b.color}"></ng-md-icon>
    </md-button>
</div>

<script>
    scope.buttons = [{
        icon: 'pause', color: 'black',
        icon2: 'play_arrow', color2: 'red',
        payload: 'play',
    }, {
        icon: 'alarm', color: 'black',
        icon2: 'alarm', color2: 'red',
        payload: 'alarm',
    }];

    scope.click = function(b) {
        if (!this.msg) this.msg = {};
        if (!this.msg.payload) this.msg.payload = {};
        this.msg.payload[b.payload] = !this.msg.payload[b.payload];
        this.send(this.msg);
    }.bind(scope);
</script>
```

## Шляхи оновлення UI

За допомогою Angular та Dashboard Template ми можемо оновити інтерфейс користувача безпосередньо з вхідного повідомлення, зробивши розрахунок після отримання повідомлення або викликаючи функцію.

```html
<h1>Msg Topic: {{msg.topic}}</h1>
<h2>msg.payload.a</h2>
<div ng-bind-html="msg.payload.a"></div>
<h2>Розраховується після отримання msg</h2>
<div>{{myCalc}}</div>
<h2>Викликати функцію по кліку</h2>
<div ng-click="click(b)">Клікни мен для зміни числа</div>
<div>{{myNum}}</div>

<script>
    // Lambda function для доступу до Angular Scope
    ;(function(scope) {
        //Щоб отримати нові вхідні повідомлення, потрібно використовувати $watch 
        scope.$watch('msg.payload', function(newVal, oldVal) {
            console.log('- Scope.msg -')
            console.dir(scope.msg)
            scope.myCalc = scope.msg.payload.b * 2
        })

        // Функція спрацьовує по кліку на div
        scope.click = function(b) {
            if ( ! scope.myNum ) scope.myNum = 0
            scope.myNum++
        }
    })(scope)
</script>
```

## Приклад Date Picker 

```javascript
<div>
   <md-datepicker ng-model="myDate" md-placeholder="Enter date" ng-change="send({payload: myDate})"></md-datepicker>
</div>
```

## Динамічне вприскування HTML

Використовуйте цей код у Dashboard Template для візуалізації повідомлення msg.payload, що містить HTML.

```javascript
<div ng-bind-html="msg.payload"></div>
```

## Для створення списку використовуйте вхідний масив або об’єкт 

Angular має властивість `ng-repeat`, що дозволяє нам проходити через масив (або об’єкт) для динамічного створення списку, таблиці тощо.

```html
<div ng-repeat="(key, value) in myObj"> ... </div>
```

Якщо можливо, використовуйте IіD для відстеження, оскільки це допомагає Angular знати, коли щось потребує оновлення:

```html
<div ng-repeat="(key, value) in myObj track by myObj.id"> ... </div>
```

Ви також можете використовувати елементи `ng-repeat-start` і ` ng-repeat-end` для обертання вмісту.

Докладніше див. у [Angular v1 docs for ngRepeat](https://docs.angularjs.org/api/ng/directive/ngRepeat) .

Робочий приклад, використовуйте це у вузлі Dashboard Template:

```html
<table>
    <tr ng-repeat="(key, value) in msg.payload">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
</table>
```

## Зміна розділювачів Angular

Якщо ви хочете надіслати дані через вузол Node-RED Template, перш ніж надсилати його на вузол Dashboard Template, ви побачите це, оскільки обидва використовують однакові роздільники (подвійні фігурні дужки). Тож вам потрібно змінити роздільники у Dashboard Template.

```javascript
<!DOCTYPE html>
<html ng-app="ngApp">
<head></head>
<body ng-controller="ngCtrl">
    <h1>Topic: {[{topic}]}</h1>
    <pre>
{[{payload | json }]}
    </pre>
    <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.4.12/angular.min.js"></script>
    <script>
        var ngApp = angular.module('ngApp', []);
        ngApp.config(function($interpolateProvider) {
            $interpolateProvider.startSymbol('{[{');
            $interpolateProvider.endSymbol('}]}');
        });
        ngApp.controller('ngCtrl', ['$scope', function($scope) {
            // Need to wrap with TRY in case not valid JSON
            $scope.payload = JSON.parse(decodeEntities('{{payload}}'));
            $scope.topic = '{{topic}}';
        }]);
        function decodeEntities(encodedString) {
            var textArea = document.createElement('textarea');
            textArea.innerHTML = encodedString;
            return textArea.value;
        }
    </script>
</body>
</html>
```