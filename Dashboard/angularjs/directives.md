# Директиви AngularJS

## ng-app

https://docs.angularjs.org/api/ng/directive/ngApp

Використовуйте цю директиву для **автоматичного завантаження (auto-bootstrap)** програми AngularJS. Директива `ngApp` позначає **кореневий елемент** програми і зазвичай розміщується біля кореневого елемента сторінки - наприклад. на тегах `<body>` або `<html>`.

Під час використання `ngApp` слід пам’ятати про кілька речей:

- лише один додаток AngularJS може автоматично завантажуватися для кожного документа HTML. Перший `ngApp`, знайдений у документі, буде використано для визначення кореневого елемента для автоматичного завантаження як програми. Щоб запустити кілька програм у документі HTML, потрібно замість цього завантажити їх вручну за допомогою [`angular.bootstrap`](https://docs.angularjs.org/api/ng/function/angular.bootstrap).
- Додатки AngularJS не можна вкладати один в одного.
- Не використовуйте директиву, яка використовує [transclusion](https://docs.angularjs.org/api/ng/service/$compile#transclusion) для того самого елемента, що і `ngApp`. Сюди входять такі директиви, як [`ngIf`](https://docs.angularjs.org/api/ng/directive/ngIf), [` ngInclude`](https://docs.angularjs.org/api/ng/ directive/ngInclude) та [`ngView`](https://docs.angularjs.org/api/ngRoute/directive/ngView). Це не позначає додаток [`$rootElement`](https://docs.angularjs.org/api/ng/service/$rootElement) та [injector](https://docs.angularjs.org/api/ auto/service/$injector) програми, внаслідок чого анімація перестає працювати, а інжектор стає недоступним за межами програми.

Ви можете вказати **модуль AngularJS**, який буде використовуватися як кореневий модуль для програми. Цей модуль буде завантажено до [`$njector`](https://docs.angularjs.org/api/auto/service/$injector) при завантаженні програми. Він повинен містити необхідний код програми або мати залежності від інших модулів, які будуть містити код. Див. [`Angular.module`](https://docs.angularjs.org/api/ng/function/angular.module) для отримання додаткової інформації.

In the example below if the `ngApp` directive were not placed on the `html` element then the document would not be compiled, the `AppController` would not be instantiated and the `{{ a+b }}` would not be resolved to `3`.

У наведеному нижче прикладі, якби директива `ngApp` не була розміщена на елементі ` html`, тоді документ не був би скомпільований, `AppController` не був би створений екземпляром, а ` {{a+b}}` не був би вирішений як `3 '.

Ця директива виконується на рівні пріоритету 0.

Використання:

- як елемент:      

  ```html
  <ng-app
    ng-app="angular.Module"
    [ng-strict-di="boolean"]>
  ...
  </ng-app>
  ```

- як атрибут:        

  ```html
  <ANY
    ng-app="angular.Module"
    [ng-strict-di="boolean"]>
  ...
  </ANY>
  ```

| Param                                  | Type                                          | Details                                                      |
| -------------------------------------- | --------------------------------------------- | ------------------------------------------------------------ |
| ngApp                                  | [angular.Module](https://docs.angularjs.org/) | an optional application  [module](https://docs.angularjs.org/api/ng/function/angular.module) name to load. |
| ngStrictDi                *(optional)* | [boolean](https://docs.angularjs.org/)        | if this attribute is present on the app element, the injector will be  created in "strict-di" mode. This means that the application will fail to invoke functions which  do not use explicit function annotation (and are thus unsuitable for minification), as described  in [the Dependency Injection guide](https://docs.angularjs.org/guide/di), and useful debugging info will assist in  tracking down the root of these bugs. |

```html
<div ng-controller="ngAppDemoController">
  I can add: {{a}} + {{b}} =  {{ a+b }}
</div>
```

## ngController

https://docs.angularjs.org/api/ng/directive/ngController

Директива `ngController` приєднує controller class до view. Це ключовий аспект того, як angular підтримує принципи, що лежать в основі шаблону дизайну Model-View-Controller.

Компоненти MVC в angular:

- Model - Моделі - це властивості scope; scope прикріплені до DOM, де доступ до властивостей області здійснюється за допомогою прив'язок.
- View - Шаблон (HTML із прив'язками даних), який відображається у View.
- Controller - Директива `ngController` визначає клас Controller; клас містить бізнес-логіку, що стоїть за додатком, щоб прикрасити область функціями та значеннями

![img](https://docs.angularjs.org/img/tutorial/tutorial_02.png)

Зауважте, що ви також можете приєднати контролери до DOM, оголосивши його у визначенні маршруту за допомогою служби [$route](https://docs.angularjs.org/api/ngRoute/service/$route) . Поширеною помилкою є повторне оголошення контролера за допомогою `ng-controller` у самому шаблоні. Це призведе до підключення і виконання контролера двічі.

- Ця директива створює нову scope.
- Ця директива виконується на рівні пріоритету 500.

Використання:

- як елементу:      

  ```html
  <ng-controller
    ng-controller="expression">
  ...
  </ng-controller>
  ```

- як атрибуту:        

  ```html
  <ANY
    ng-controller="expression">
  ...
  </ANY>
  ```

| Param        | Type                                      | Details                                                      |
| ------------ | ----------------------------------------- | ------------------------------------------------------------ |
| ngController | [expression](https://docs.angularjs.org/) | Назва функції конструктора, зареєстрованої у поточному [$controllerProvider](https://docs.angularjs.org/api/ng/provider/$controllerProvider)  або  [expression](https://docs.angularjs.org/guide/expression) , який у поточній scope оцінює функцію конструктора. Екземпляр контролера можна опублікувати у властивості видимості, вказавши `ng-controller ="as propertyName"`. |

**Приклад**

Ось проста форма для редагування контактної інформації користувача. Додавання, видалення, очищення та привітання - це методи, оголошені на контролері (див. Вкладку «Джерело»). Ці методи можна легко викликати з розмітки AngularJS. Будь -які зміни даних автоматично відображаються у View без необхідності оновлення вручну.

Нижче наведено два різних стилі декларування:

- один прив'язує методи та властивості безпосередньо до контролера за допомогою `this`: `ng-controller="SettingsController1 as settings"`
- вводиться `$scope` в контролер:` ng-controller="SettingsController2" `

Другий варіант є більш поширеним у спільноті AngularJS і зазвичай використовується у шаблонах та в цьому посібнику. Однак існують переваги у прив’язуванні властивостей безпосередньо до контролера та уникнення scope.

- Використання `controller as` дає зрозуміти, до якого контролера ви звертаєтесь у шаблоні, коли до елемента застосовується кілька контролерів.
- Якщо ви пишете свої контролери як класи, у вас буде легший доступ до властивостей і методів, які відображатимуться в області видимості, всередині коду контролера.
- Оскільки у прив'язках завжди є `.`, вам не потрібно турбуватися про прототипові маски, що маскують primitives.

У цьому прикладі демонструється синтаксис  `controller as` .

```html
<div id="ctrl-as-exmpl" ng-controller="SettingsController1 as settings">
  <label>Name: <input type="text" ng-model="settings.name"/></label>
  <button ng-click="settings.greet()">greet</button><br/>
  Contact:
  <ul>
    <li ng-repeat="contact in settings.contacts">
      <select ng-model="contact.type" aria-label="Contact method" id="select_{{$index}}">
         <option>phone</option>
         <option>email</option>
      </select>
      <input type="text" ng-model="contact.value" aria-labelledby="select_{{$index}}" />
      <button ng-click="settings.clearContact(contact)">clear</button>
      <button ng-click="settings.removeContact(contact)" aria-label="Remove">X</button>
    </li>
    <li><button ng-click="settings.addContact()">add</button></li>
 </ul>
</div>
```

```js
angular.module('controllerAsExample', [])
  .controller('SettingsController1', SettingsController1);

function SettingsController1() {
  this.name = 'John Smith';
  this.contacts = [
    {type: 'phone', value: '408 555 1212'},
    {type: 'email', value: 'john.smith@example.org'}
  ];
}

SettingsController1.prototype.greet = function() {
  alert(this.name);
};

SettingsController1.prototype.addContact = function() {
  this.contacts.push({type: 'email', value: 'yourname@example.org'});
};

SettingsController1.prototype.removeContact = function(contactToRemove) {
 var index = this.contacts.indexOf(contactToRemove);
  this.contacts.splice(index, 1);
};

SettingsController1.prototype.clearContact = function(contact) {
  contact.type = 'phone';
  contact.value = '';
};
```

This example demonstrates the "attach to `$scope`" style of controller.

```html
<div id="ctrl-exmpl" ng-controller="SettingsController2">
  <label>Name: <input type="text" ng-model="name"/></label>
  <button ng-click="greet()">greet</button><br/>
  Contact:
  <ul>
    <li ng-repeat="contact in contacts">
      <select ng-model="contact.type" id="select_{{$index}}">
         <option>phone</option>
         <option>email</option>
      </select>
      <input type="text" ng-model="contact.value" aria-labelledby="select_{{$index}}" />
      <button ng-click="clearContact(contact)">clear</button>
      <button ng-click="removeContact(contact)">X</button>
    </li>
    <li>[ <button ng-click="addContact()">add</button> ]</li>
 </ul>
</div>
```

```js
angular.module('controllerExample', [])
  .controller('SettingsController2', ['$scope', SettingsController2]);

function SettingsController2($scope) {
  $scope.name = 'John Smith';
  $scope.contacts = [
    {type:'phone', value:'408 555 1212'},
    {type:'email', value:'john.smith@example.org'}
  ];

  $scope.greet = function() {
    alert($scope.name);
  };

  $scope.addContact = function() {
    $scope.contacts.push({type:'email', value:'yourname@example.org'});
  };

  $scope.removeContact = function(contactToRemove) {
    var index = $scope.contacts.indexOf(contactToRemove);
    $scope.contacts.splice(index, 1);
  };

  $scope.clearContact = function(contact) {
    contact.type = 'phone';
    contact.value = '';
  };
}
```

## ngModel

https://docs.angularjs.org/api/ng/directive/ngModel

Директива `ngModel` пов'язує ` input`, `select`, ` textarea` (або спеціальний елемент керування формою) зі властивістю в scope  за допомогою  [NgModelController](https://docs.angularjs.org/api/ng/type/ngModel.NgModelController), який створюється та відкривається цією директивою.

`ngModel` несе відповідальність за:

- Прив’язка представлення до моделі, що вимагається іншими директивами, такими як `input`, ` textarea` або `select`.

- Надання перевірки поведінки (тобто обов'язковий, номер, електронна адреса, url).
- Збереження стану контролю (valid/invalid, dirty/pristine, touched/untouched, validation errors).
- Встановлення відповідних класів css для елемента  (`ng-valid`, `ng-invalid`, `ng-dirty`, `ng-pristine`, `ng-touched`, `ng-untouched`, `ng-empty`, `ng-not-empty`) , включаючи анімації.
- Реєстрація елемента керування в його батьківській  [form](https://docs.angularjs.org/api/ng/directive/form).

Примітка: `ngModel` спробує зв’язатись із властивістю, заданою, оцінивши вираз у поточній області видимості. Якщо властивість ще не існує в цій області, вона буде створена неявно і додана до області видимості.

For best practices on using `ngModel`, see:

- [Understanding Scopes](https://github.com/angular/angular.js/wiki/Understanding-Scopes)

For basic examples, how to use `ngModel`, see:

- input
  - [text](https://docs.angularjs.org/api/ng/input/input[text])
  - [checkbox](https://docs.angularjs.org/api/ng/input/input[checkbox])
  - [radio](https://docs.angularjs.org/api/ng/input/input[radio])
  - [number](https://docs.angularjs.org/api/ng/input/input[number])
  - [email](https://docs.angularjs.org/api/ng/input/input[email])
  - [url](https://docs.angularjs.org/api/ng/input/input[url])
  - [date](https://docs.angularjs.org/api/ng/input/input[date])
  - [datetime-local](https://docs.angularjs.org/api/ng/input/input[datetime-local])
  - [time](https://docs.angularjs.org/api/ng/input/input[time])
  - [month](https://docs.angularjs.org/api/ng/input/input[month])
  - [week](https://docs.angularjs.org/api/ng/input/input[week])
- [select](https://docs.angularjs.org/api/ng/directive/select)
- [textarea](https://docs.angularjs.org/api/ng/directive/textarea)

**Складні моделі (objects or collections)**

За замовчуванням `ngModel` переглядає модель за посиланням, а не за значенням. Це важливо знати при прив'язці вхідних даних до моделей, які є об'єктами (наприклад, `Date`) або колекціями (наприклад, масивами). Якщо змінюються лише властивості об'єкта або колекції, `ngModel` не буде повідомлено, а тому вхідні дані не будуть відтворені повторно.

Моделю потрібно призначити абсолютно новий об’єкт або колекцію, перш ніж відбудеться повторне відтворення.

Деякі директиви мають варіанти, які змусять їх використовувати власний `$watchCollection` у виразі моделі

- наприклад, `ngOptions` зробить це, якщо в вираз розуміння включено пропозицію` track by`, або якщо вибору надано атрибут `multiple`.

Метод `$watchCollection()` робить лише поверхневе порівняння, що означає, що зміна властивостей глибше, ніж на першому рівні об'єкта (або лише зміна властивостей елемента в колекції, якщо це масив) все одно не спричинить повторне візуалізація моделі.

**CSS classes**

Наступні класи CSS додаються та видаляються у відповідному елементі input/select/textarea залежно від дійсності моделі.

- `ng-valid`: the model is valid
- `ng-invalid`: the model is invalid
- `ng-valid-[key]`: for each valid key added by `$setValidity`
- `ng-invalid-[key]`: for each invalid key added by `$setValidity`
- `ng-pristine`: the control hasn't been interacted with yet
- `ng-dirty`: the control has been interacted with
- `ng-touched`: the control has been blurred
- `ng-untouched`: the control hasn't been blurred
- `ng-pending`: any `$asyncValidators` are unfulfilled
- `ng-empty`: the view does not contain a value or the value is deemed "empty", as defined by the [`ngModel.NgModelController`](https://docs.angularjs.org/api/ng/type/ngModel.NgModelController#$isEmpty) method
- `ng-not-empty`: the view contains a non-empty value

Keep in mind that ngAnimate can detect each of these classes when added and removed.

**Directive Info**

- This directive executes at priority level 1.

**Usage**

- as attribute:        

  ```
  <ANY
    ng-model="expression">
  ...
  </ANY>
  ```

**Arguments**

| Param   | Type                                      | Details                                                      |
| ------- | ----------------------------------------- | ------------------------------------------------------------ |
| ngModel | [expression](https://docs.angularjs.org/) | assignable [Expression](https://docs.angularjs.org/guide/expression) to bind to. |

**Animations**

Анімації всередині моделей запускаються, коли будь -який з асоційованих класів CSS додається та видаляється на вхідному елементі, що приєднаний до моделі. До цих класів належать: `.ng-pristine`,` .ng-dirty`, `.ng-invalid` та` .ng-valid`, а також будь-які інші перевірки, які виконуються на самій моделі. Анімації, які запускаються в ngModel, подібні до того, як вони працюють у ngClass, і анімації можна підключити за допомогою переходів CSS, ключових кадрів, а також анімацій JS.

У наведеному нижче прикладі показано простий спосіб використання CSS -переходів для стилізації елемента введення, який після його перевірки став недійсним:

```css
//be sure to include ngAnimate as a module to hook into more
//advanced animations
.my-input {
  transition:0.5s linear all;
  background: white;
}
.my-input.ng-invalid {
  background: red;
  color:white;
}
```

[Click here](https://docs.angularjs.org/api/ngAnimate/service/$animate) to learn more about the steps involved in the animation.     

**Examples**

```html
<script>
 angular.module('inputExample', [])
   .controller('ExampleController', ['$scope', function($scope) {
     $scope.val = '1';
   }]);
</script>
<style>
  .my-input {
    transition:all linear 0.5s;
    background: transparent;
  }
  .my-input.ng-invalid {
    color:white;
    background: red;
  }
</style>
<p id="inputDescription">
 Update input to see transitions when valid/invalid.
 Integer is a valid value.
</p>
<form name="testForm" ng-controller="ExampleController">
  <input ng-model="val" ng-pattern="/^\d+$/" name="anim" class="my-input"
         aria-describedby="inputDescription" />
</form>
```

**Binding to a getter/setter**

Іноді корисно прив'язати `ngModel` до функції  getter/setter.  getter/setter - це функція, яка повертає представлення моделі при виклику з нульовими аргументами, і встановлює внутрішній стан моделі при виклику з аргументом. Іноді корисно використовувати це для моделей, які мають внутрішнє представлення, яке відрізняється від того, що модель виставляє подання.

**Найкраща практика:** Найкраще тримати геттерів, оскільки AngularJS, швидше за все, буде викликати їх частіше, ніж інші частини вашого коду.

You use this behavior by adding `ng-model-options="{ getterSetter: true }"` to an element that has `ng-model` attached to it. You can also add `ng-model-options="{ getterSetter: true }"` to a `<form>`, which will enable this behavior for all `<input>`s within it. See [`ngModelOptions`](https://docs.angularjs.org/api/ng/directive/ngModelOptions) for more.

У наведеному нижче прикладі показано, як використовувати `ngModel` з геттером/сеттером:

```html
<div ng-controller="ExampleController">
  <form name="userForm">
    <label>Name:
      <input type="text" name="userName"
             ng-model="user.name"
             ng-model-options="{ getterSetter: true }" />
    </label>
  </form>
  <pre>user.name = <span ng-bind="user.name()"></span></pre>
</div>
```

```js
angular.module('getterSetterExample', [])
.controller('ExampleController', ['$scope', function($scope) {
  var _name = 'Brian';
  $scope.user = {
    name: function(newName) {
     // Note that newName can be undefined for two reasons:
     // 1. Because it is called as a getter and thus called with no arguments
     // 2. Because the property should actually be set to undefined. This happens e.g. if the
     //    input is invalid
     return arguments.length ? (_name = newName) : _name;
    }
  };
}]);
```



[Button (Кнопка) ->](Button.md)