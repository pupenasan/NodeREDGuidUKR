| [На головну](../)                             | [Розділ](README.md) |
| --------------------------------------------- | ------------------- |
| [<- Ui control (Керування UI)](Ui_control.md) |                     |

## 3.20. Template (Шаблон)

![img](media/template.png)Шаблонний віджет (template widget) може містити будь-які дійсні директиви html та Angular / Angular-Material. Цей вузол може бути використаний для створення динамічного елементу інтерфейсу користувача, який змінює свій вигляд на основі вхідного повідомлення і може посилати повідомлення назад до Node-RED. 

Наведений нижче код буде змінювати текст в залежності від парності числа, отриманого `msg.payload`. Він також змінить колір тексту на зелений, якщо число парне, або на червоний, якщо непарне.

```html
<div layout="row" layout-align="space-between">
  <p>The number is</p>
  <p ng-style="{color: (msg.payload || 0) % 2 === 0 ? 'green' : 'red'}">
    {{(msg.payload || 0) % 2 === 0 ? 'even' : 'odd'}}
  </p>
</div>
```

У наступному прикладі показано, як встановити унікальний ідентифікатор для вашого шаблону, підібрати колір теми за замовчуванням і переглянути будь-яке вхідне повідомлення.

```html
<div id="{{'my_'+$id}}" style="{{'color:'+theme.base_color}}">Some text</div>
<script>
(function(scope) {
  scope.$watch('msg', function(msg) {
    if (msg) {
      // Do something when msg arrives
      $("#my_"+scope.$id).html(msg.payload);
    }
  });
})(scope);
</script>
```

Шаблони, зроблені таким чином, можуть бути скопійовані і залишатися незалежними один від одного. 

Наступний код приведе до того, що з'явиться кнопка, яка при натисканні надішле повідомлення з payload `'Hello world'`.

```html
<script>
var value = "hello world";
// or overwrite value in your callback function ...
this.scope.action = function() { return value; }
</script>
<md-button ng-click="send({payload:action()})">
    Click me to send a hello world
</md-button>
```

Ви також можете визначити вміст шаблону за допомогою `msg.template`. При цьому, наприклад, можна використовувати зовнішні файли. Шаблон буде перезавантажено на вхід, якщо він був змінений.

Якщо в у полі Template ` msg.template` присутній код, його буде проігноровано. Також доступні наступні шрифтові значки: [Material Design icons](https://design.google.com/icons/), [Font Awesome icons](https://fontawesome.com/v4.7.0/icons/), [Weather icons](https://github.com/Paul-Reed/weather-icons-lite/blob/master/css/weather-icons-lite.css).

У Template можна використовувати директиви AngularJS, які дозволяють розробнику модифікувати поведінку деяких елементів, чи описати власні елементи. 

**ng-app**

Оголошує елемент кореневим елементом застосунку, дозволяючи змінювати поведінку за допомогою спеціальних тегів.

**ng-bind**

Змінює текст елемента на значення виразу.

```html
<span ng-bind="name"></span> 
```

відобразить значення змінної `name` всередині тегу `span`. Будь-які зміни змінної будуть миттєво відображені в DOM, де б змінна не використовувалась.

**ng-init**

Ініціалізує/визначає дані/змінні вашого додатку. 

**ng-model**

Подібна до `ng-bind`, але дозволяє двостороннє зв'язування даних (зміни в DOM будуть змінювати змінну).

**ng-class**

Дозволяє динамічно додавати та забирати класи елемента.: 

```html
<div class="{'active': activeDiv}"></div>
```

**ng-controller**

Вказує клас JavaScript контролера.

**ng-repeat**

Створює кілька екземплярів елемента, для кожного об'єкта колекції.

**ng-show & ng-hide**

Показують чи ховають елемент залежно від значення булевого виразу. Це досягається за допомогою задання в CSS атрибуту `display`.

**ng-disabled** 

Встановлює атрибут `disabled`` `для елемента (кнопка, поле вводу, тощо), якщо вираз в середині ng-disabled вірний. Код нижче встановить атрибут disabled для поля вводу при введенні рядка більше 15 символів:

```html
<input ng-model='name' ng-disabled='name.length > 15'> 
```

**ng-click/ngDblclick** 

Виконує описаний вираз при кліку/подвійному кліку на елемент. Код нижче виконує функцію submitForm при кліку на кнопку

```html
<button ng-click='submitForm()'></button> 
```

**ng-mousedown/ng-mouseup** 

Подібні до ng-click, спрацьовують при натисканні/відпусканні лівої кнопки миші на елементі. 

**ng-if** 

Видаляє чи створює елемент в DOM дереві. 

```html
<div ng-if='showBlock'>...</div> 
```

Директива дуже подібна до директиви ng-show. Для того щоб запобігти втрат у швидкодії, рекомендується застосовувати директиву ng-show для приховування великої кількості елементів у зв'язку повільної роботи DOM дерева. 

Про AngularJS можна також почитати за наступними посиланнями 

- [Tutorial](https://docs.angularjs.org/tutorial) 
- [AngularJS Hello world example. Основы AngularJS: модуль, контроллер, выражения](http://javastudy.ru/angularjs/angularjs-hello-world-example/) 
- [Использование фильтров AngularJS filters. Angular ng-repeat filter и собственный фильтр](http://javastudy.ru/angularjs/angularjs-filters/)
- [Основы AngularJS ](https://metanit.com/web/angular/2.4.php)
- [All About the Built-In AngularJS Filters](https://scotch.io/tutorials/all-about-the-built-in-angularjs-filters)

[<- На головну](../)  [Розділ](README.md)

