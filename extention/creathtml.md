# Створення власних вузлів

## [HTML File](https://nodered.org/docs/creating-nodes/node-html)

Файл `.html`вузла означує спосіб появи вузла в редакторі. Він містить три чіткі частини, кожна з яких загорнута у власний тег `<script>`:

1. головне означення вузла, що реєструється у редакторі. Це означує такі речі, як категорія палітри, властивості для редагування (`defaults`) та який значок використовувати. Він знаходиться в межах звичайного тегу сценарію javascript
2. шаблон редагування, який означує вміст діалогу редагування для вузла. Він означений у сценарії типу `text/html` із набору ` data-template-name`, встановленим у типі вузла.
3. текст довідки, який відображається на вкладці бічної панелі інформації. Він означений у сценарії типу `text/html` із набору`data-help-name`, встановленим у типі вузла.

### Означення вузлу

Вузол повинен бути зареєстрований у редакторі за допомогою функції `RED.nodes.registerType`.

Ця функція бере два аргументи: тип вузлу та його означення:

```html
<script type="text/javascript">
    RED.nodes.registerType('node-type',{
        // означення вузлу
    });
</script>
```

#### Node type (тип вузлу)

Тип вузлу використовується у всьому редакторі для ідентифікації вузла. Він повинен відповідати значенню, використовуваному викликом до `RED.nodes.registerType` у відповідному файлі` .js`.

Тип також використовується як мітка для вузла в палітрі. Якщо тип закінчується на `in` або `out`, це знімається з мітки. Наприклад, вузли `mqtt in` та `mqtt out` обоє позначені як «mqtt», при цьому відображення вхідних та вихідних портів забезпечують контекст `in` або `out`.

#### Означення вузлу

Означення вузлу містить всю інформацію про вузол, необхідний редактору. Це об'єкт із наступними властивостями: 

- `category`: (string) категорія палітри, в якій з'являється вузол 
- `defaults`: (object)  [налаштовувані властивості](creatprop.md) для вузлу.
- `credentials`: (object) [credential properties](creatcredent.md) для вузлу.
- `inputs`: (number) скільки входів має вузол, `0` або `1`.
- `outputs`: (number) скільки виходів має вузол. Більше або рівне `0`.
- `color`: (string)  [колір фону](createapp.md#color) для використання.
- `paletteLabel`: (string|function) [мітка](createapp.md#label) на палітрі.
- `label`: (string|function) [мітка](createapp.md#label) в робочому просторі.
- `labelStyle`: (string|function) [стиль](createapp.md#label-style) застосовний для мітки.
- `inputLabels`: (string|function) опціональна [мітка](createapp.md#port-labels) для вхідного порту.
- `outputLabels`: (string|function) опціональна [мітка](createapp.md#port-labels) для вихідних портів.
- `icon`: (string) [іконка](createapp.md#icon) для використання.
- `align`: (string) [вирівнювання](createapp.md#alignment) іконки та мітки.
- `button`: (object) добавляє [кнопку](createapp.md#buttons) на край вузлу.
- `oneditprepare`: (function) викликається коли буде побудований діалог редагування. Див [поведінка редактору налаштування](creatprop.md#custom-edit-behaviour).
- `oneditsave`: (function) викликається, коли в діалозі буде натиснута кнопка `Ok`. Див [поведінка редактору налаштування](creatprop.md#custom-edit-behaviour).
- `oneditcancel`: (function) викликається, коли в діалозі буде натиснута кнопка `Cancel`. Див [поведінка редактору налаштування](creatprop.md#custom-edit-behaviour).
- `oneditdelete`: (function) викликається, коли в діалозі буде натиснута кнопка `Delete`. Див [поведінка редактору налаштування](creatprop.md#custom-edit-behaviour).
- `oneditresize`: (function) викликається, коли розмір діалогу редагування буде змінений. Див [поведінка редактору налаштування](creatprop.md#custom-edit-behaviour).
- `onpaletteadd`: (function) викликається, коли тип вузлу добавляється на палітру.
- `onpaletteremove`: (function) викликається, коли тип вузлу видаляється з палітри.

### Діалог редагування

Шаблон редагування для вузла описує вміст його діалогового вікна редагування.

```html
<script type="text/html" data-template-name="node-type">
    <div class="form-row">
        <label for="node-input-name"><i class="fa fa-tag"></i> Name</label>
        <input type="text" id="node-input-name" placeholder="Name">
    </div>
    <div class="form-tips"><b>Tip:</b> Місце для тексту допомоги.</div>
</script>
```

Дотримуйтесь декількох простих умов: 

- для компонування кожного рядка діалогового вікна слід використовувати `<div>` з класом `form-row` .
- типовий рядок матиме `<label>`, що містить піктограму та ім'я властивості, за яким слідує `<input>`. Значок створюється за допомогою елемента `<i>` з класом, узятим із доступних у [Font Awesome 4.7](https://fontawesome.com/v4.7.0/icons/).
- якщо потрібно більше інтерактивності, для приєднання будь-яких обробників подій до елементів діалогу можна використовувати  `oneditprepare` .

Більше інформації про те, як використовується шаблон редагування, доступна [тут](creatprop.md#property-edit-dialog).

### Текст допомоги

Коли вибирається вузол, його довідковий текст відображається на інформаційній вкладці. Це повинно дати змістовний опис того, що робить вузол. Він повинен означити, які властивості він встановлює для вихідних повідомлень та які властивості можна встановити для вхідних повідомлень.

Вміст першого тегу `<p>` використовується як підказка під час наведення курсору на вузли в палітрі.

```html
<script type="text/html" data-help-name="node-type">
   <p>Some useful help text to introduce the node.</p>
   <h3>Outputs</h3>
       <dl class="message-properties">
       <dt>payload
           <span class="property-type">string | buffer</span>
       </dt>
   <h3>Details</h3>
   <p>Some more information about the node.</p>
</script>
```

Повний посібник зі стилю для допомоги у вузлах [доступний тут](creathelp.md).