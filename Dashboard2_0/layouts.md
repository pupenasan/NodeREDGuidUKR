| [На головну](../) | [Розділ](README.md) |
| ----------------- | ------------------- |
|                   |                     |

# Макетування (Layouts)

Кожна інформаційна панель (Dashboard) — це набір віджетів (наприклад, діаграм, кнопок, форм), які можна налаштувати та впорядкувати в нашому власному інтерфейсі користувача. Ієрархія інформаційної панелі така:

- `Base` – означує базову URL-адресу (наприклад, `/dashboard`) для вашої інформаційної панелі.
- Page – дана сторінка, на яку може перейти відвідувач, URL-адреса розширить базу, напр. `/dashboard/page1`. Кожна сторінка також може мати означену унікальну тему, яка керує стилем усіх груп/віджетів на сторінці.
- Group - колекція віджетів. Відображено на сторінці.
- Widget – один віджет (наприклад, діаграма, кнопка, форма), створений на інформаційній панелі.

Dashboard 2.0 додає до редактора Node-RED відповідну бічну панель «Dashboard 2.0». Ця бічна панель надає інтерфейс, за допомогою якого можна переглядати сторінки, теми, групи та віджети. Звідси ви можете додавати нові сторінки та групи, змінювати існуючі налаштування та змінювати порядок вмісту на свій смак.

![Screenshot showing the Dashboard 2.0 sidebar in the Node-RED Editor.](meida/getting-started-sidebar.BCmeVdD2.png)

рис. Знімок екрана, на якому показано бічну панель Dashboard 2.0 у редакторі Node-RED.

Параметри макета в інтерфейсі користувача Dashboard 2.0 керуються двома основними налаштуваннями:

- `Page Layout:` контролює, як `ui-groups` представлені на певній сторінці у вашій програмі.
- `Navigation Sidebar:` означує стиль навігації ліворуч, означений на рівні `ui-base`.

![Example of a "Grid" page layout, with a "Collapsing" sidebar navigation.](meida/getting-started-layout.CTFJcfOh.png)

Приклад "клітинного" макета сторінки (Grid) з навігацією бічної панелі типу "Collapsing".

### Сторінка за замовчуванням

Кожна сторінка в Dashboard 2.0 має унікальну URL-адресу. Якщо користувач переходить до нерозпізнаного шляху під шляхом `/dashboard/`, то для повернення використовується сторінка за замовчуванням.

Зараз у Dashboard 2.0 сторінка за замовчуванням вибирається як сторінка, яка стоїть першою в списку сторінок на бічній панелі навігації:

![Screenshot of the pages list in the Dashboard 2.0 side panel](meida/default-page-layout.BzpvPkIC.png)

Знімок екрана зі списком сторінок на бічній панелі Dashboard 2.0

У цьому прикладі сторінка "Віджети третьої сторони" є сторінкою за замовчуванням.

### Параметри макета (Layout)

Наразі ми маємо три різні варіанти макета сторінки:

- Grid: ([опис](https://dashboard.flowfuse.com/layouts/types/grid.html)) Макет сторінки за умовчанням. Він використовує структуру сітки з 12 стовпців для розміщення груп. Ширина кожної групи або віджета визначає кількість стовпців, у яких вони відтворюватимуться. Таким чином, «ширина» 6 дюймів відтворюватиме 50% екрана. Макети сітки повністю реагують і адаптуються до розміру екрана. .
- Fixed: ([опис](https://dashboard.flowfuse.com/layouts/types/fixed.html)) Кожен компонент відтворюватиметься з фіксованою шириною, незалежно від розміру екрана. Властивість «width» перетворюється на фіксоване значення пікселів (за замовчуванням кратне 48 пікселів).
- Notebook: ([опис](https://dashboard.flowfuse.com/layouts/types/notebook.html)) Цей макет розтягнеться до 100% ширини, до максимальної ширини 1024 пікселів, і буде вирівняти по центру. Це особливо корисно для розповіді історій (наприклад, статей/блогів) або користувальницьких інтерфейсів типу аналізу (наприклад, Jupyter Notebooks), де ви хочете, щоб користувач переглядав вміст у певному порядку за допомогою прокручування.

### Бічна панель навігації

У структуру інтерфейсу користувача вбудована бічна навігаційна панель разом із верхньою «панеллю додатків» на всій сторінці. Існують параметри конфігурації, за допомогою яких можна керувати поведінкою бічної навігації. Опції включають:

- Collapsing: коли бічна панель відкрита, вміст сторінки змінюватиметься відповідно до ширини бічної панелі.
- Fixed: повна бічна панель завжди буде видимою, а вміст сторінки підлаштовуватиметься відповідно до ширини бічної панелі.
- Collapse to Icons: у згорнутому режимі користувачі можуть переходити між сторінками, клацаючи піктограми, що представляють кожну сторінку, на бічній панелі.
- Appear over Content: коли бічна панель відкрита, сторінка накладається, а бічна панель розташовується зверху.
- Always Hide: бічна панель ніколи не відображатиметься, а навігація між сторінками може здійснюватися за допомогою [`ui-control`](https://dashboard.flowfuse.com/nodes/widgets/ui-control.html). ).

Детальніше про макетування читайте в [Макетування ](layouts.md)

https://dashboard.flowfuse.com/layouts/ 

Макети – це конфігурація, доступна на основі сторінки за сторінкою. Вони контролюють, як усі Групи віджетів розташовані на даній Сторінці:

![Screenshot of the layout options on a ui-page](meida/layouts-page-layout-option.BqMk3shr.png)

Зараз ми пропонуємо чотири різні варіанти компонування:

- [Grid](https://dashboard.flowfuse.com/layouts/types/grid.html)
- [Fixed](https://dashboard.flowfuse.com/layouts/types/fixed.html)
- [Notebook](https://dashboard.flowfuse.com/layouts/types/notebook.html)
- [Tabs](https://dashboard.flowfuse.com/layouts/types/tabs.html)

## Розмір груп і віджетів

Фундаментальним компонентом побудови макетів у Dashboard 2.0 (який дотримується принципу Dashboard 1.0) є можливість контролювати розмір кожної групи та віджета за допомогою віджета вибору розміру:

![Screenshot of the size selection widget for a ui-gauge](meida/layouts-sizing-options.DJ-4LIFd.png)

Конкретне значення цього розміру дещо відрізняється залежно від макета, який ви використовуєте, але загальний принцип полягає в тому, що розмір групи або віджета визначає, скільки місця вони займають у макеті.

Основні відмінності полягають у властивості «ширина» розміру:

- Для «Grid» та «Notebook» ширина обчислюється як частина 12 стовпців, тобто ширина «6» займе половину ширини макета.
- Для «Fixed» ширина обчислюється як кратне 90 пікселів, тобто ширина «3» займе 270 пікселів екрана.

## Точки переривання

У більшості макетів на інформаційній панелі використовується концепція «Columns», за якою ширина групи визначається як кількість стовпців, напр. 6, а потім сторінка також відображає певну кількість стовпців, наприклад. 12. Це означає, що група з шириною 6 займе половину ширини сторінки.

Точки переривання  [можна налаштувати](https://dashboard.flowfuse.com/nodes/config/ui-page.html#breakpoints) для кожної сторінки, контролюючи кількість стовпців, які відображаються на різних розмірах екрана. Це особливо корисно для адаптивного дизайну, що дозволяє контролювати кількість стовпців, які відображаються на мобільному пристрої, планшеті чи комп’ютері.

## Параметри теми

На додаток до основної структури макета, яка визначає, як упорядковано та розміщено групи, також можна керувати деякими інтервалами в макеті за допомогою сторінки  [Theme](https://dashboard.flowfuse.com/nodes/config/ui-theme.html).

### Конфігуровані параметри

![Screenshot of the theme options available to control sizings of the layout](meida/layouts-theme-options.BokV5az8.jpg)

Кожен колір тут відповідає відповідному розділу на наступному зображенні:

![Screenshot of the theme options available to control sizings of the layout](meida/layouts-theme-example.C6Zp6oG9.jpg)

Screenshot of the theme options available to control sizings of the layout, here showing a "Grid" layout

- Page Padding: The spacing that encapsulates the full page's content, depicted above as the orange space.
- Group Gap: The spacing between each group, depicted above as the green space.
- Widget Gap: The spacing between each widget, within a group, depicted above as the pink space.

Додаткова опція, доступна для кожної групи, полягає в тому, чи показувати назву групи, зображену вище жовтим пробілом. Якщо це приховано, заповнення групи (синє) відображатиметься з усіх чотирьох сторін групи.

### Not Configurable (Currently) 

Whilst we do offer reasonable levels of customization, there are some areas not currently configurable:

- Row Height: A single unit of height is currently fixed at 48px. This cannot be  changed at this time. This also affects the "Fixed" layout, where a  single unit of width is driven by this value.
- Group Padding: The spacing that encapsulates the full group's content, depicted above as the blue space.

# Config: UI Group `ui-group` 

Each group is rendered within a `ui-page` as part of a [Layout](https://dashboard.flowfuse.com/contributing/guides/layouts.html). Each layout will differ in how those groups are rendered, but  fundamentally, a group is a collection of widgets, and generally has a  label to categorise the contents of a single group.

## Properties 

| Prop          | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| Name          | Descriptive name for this group, will show in the Node-RED Editor and as a label in the Dashboard. |
| Page          | The Page (`ui-page`) that this group will render on.         |
| Type          | Керує, чи буде група відображатися як група за замовчуванням чи як діалогове вікно, яке потрібно запускати вручну за допомогою ui-control. Ви можете вибрати між типами «Default» і «Dialog». |
| Size          | The width and height of the group. Height will always be reinforced by this value, the height is generally a minimum height, and will extend to fit it's content. |
| Class         | Any custom CSS classes you wish to add to the Group.         |
| Default State | Visibility - Defines the default visibility of this group.Interactivity - Controls whether the group and it's contents are disabled/enabled when the page is loaded.Both of these can be overridden by the user at runtime using a `ui-control` node. |

## Type 

Визначає спосіб відображення групи. Або як звичайну (Default) групу, або як групу Dialog. Група «Default» відображається за замовчуванням, тоді як групу «Dialog» потрібно запускати вручну за допомогою вузла «ui-control» ([див. документацію](https://dashboard.flowfuse.com/nodes/widgets/ui-control.html#show-hide)). Ви можете вибрати між цими двома варіантами залежно від ваших потреб у макеті.

### Default Groups 

![Example of how the type 'Default' option looks](meida/ui-group-type-default.png)

Example of how the type 'Default' option looks

### Dialog Groups 

![Example of how the type 'Dialog' option looks](meida/ui-group-type-dialog.png)

Example of how the type 'Dialog' option looks







