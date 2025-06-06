[Статті та новини](README.md)

# Візуальний редактор макета – тепер доступний на інформаційній панелі Dashboard

Ориганльна стаття [доступна за поисланням](https://flowfuse.com/blog/2024/11/dashboard-new-group-type-app-icon-and-charts)

З останнім оновленням ми випустили новий редактор макета для інформаційної панелі, а також нові віджети та широкі покращення.

![](https://flowfuse.com/img/dashboard-1-19-0-tile-Em6FTUUp6r-560.avif)

Це була одна з найбільш затребуваних функцій для FlowFuse Dashboard, і тепер доступна в її першій ітерації. Тепер можна змінювати розмір і переміщувати групи на самій інформаційній панелі Dashboard за допомогою нової функції "Edit Layout". Але це ще не все, ми додали новий віджет "Spacer", щоб допомогти з макетами, покращили відтворення діаграм і багато іншого.

## Редактор макетів - короткий посібник

Для тих, хто переходить з оригінальної Node-RED Dashboard 1.0, ви помітите певну різницю в тому, як тепер можна редагувати макет вашої інформаційної панелі. Тепер редагування здійснюється безпосередньо на панелі інструментів, а не в редакторі Node-RED.

Щоб відкрити інформаційну панель у «Edit Mode», натисніть кнопку «Edit Layout» для відповідної сторінки на бічній панелі інформаційної панелі:

![Screenshot showing the Edit Layout button in the Dashboard sidebar](https://flowfuse.com/img/edit-layout-button-XmkdmksdcR-1228.jpeg)

This will open the relevant page in "Edit Mode": Це відкриє відповідну сторінку в "Edit Mode":



![Short recording to show resizing and reordering in the visual layout editor](https://flowfuse.com/img/wysiwyg-demo-arCxQc55qK-800.webp)

*Короткий запис, щоб показати зміну розміру та порядок у редакторі візуального макета*

Три елементи керування у верхній частині сторінки:

- **Save Changes:** розгорнути будь-які зміни в основному потоці Node-RED.
- **Discard Changes:** очистити всі зміни в браузері, які ще не були збережені.
- **Exit Edit Mode:** зупинити «Режим редагування» та взаємодіяти з інформаційною панеллю як стандартний кінцевий користувач.

Потім ви можете використовувати маркери кожної групи, щоб змінити їх розмір, або клацнути та перетягнути, щоб змінити розташування груп на сторінці. Спосіб виконання цього перепозиціонування контролюється властивістю "Layout" сторінки. Візуальний редактор наразі доступний лише для макетів "Grid" та "Fixed". Коли ви задоволені своїми змінами, натисніть кнопку «Зберегти зміни», щоб розгорнути їх у базовому потоці Node-RED. Зауважте, що коли ви повернетеся до редактора Node-RED, тоді панель інструментів сповістить вас про те, що *"ваші потоки оновлено"*, .

Зауважте, що ви можете ввійти в «Режим редагування» лише через редактор Node-RED, щоб забезпечити безпеку та стабільність вашої інформаційної панелі, у випадках, коли у вас можуть бути користувачі вашої інформаційної панелі, які не повинні мати доступу до зміни макета вашої інформаційної панелі.

## Редактор макетів - наступні кроки

Ми добре розуміємо, що це лише перша ітерація редактора макета, і ми маємо багато планів щодо його подальшого вдосконалення. Ось деякі функції, які ми розглядаємо для майбутніх випусків:

- Додавання функції зміни розміру та порядку віджетів у редакторі макета
- Перегляд параметрів розміру для груп і віджетів [#835](https://github.com/FlowFuse/node-red-dashboard/issues/835)

Якщо є якісь інші ключові функції редактора, які ви хотіли б побачити, зв’яжіться з нами, розкрийте issues GitHub і допоможіть нам сформувати майбутнє FlowFuse Dashboard.

## Новий віджет: UI Spacer

На бічній панелі інформаційної панелі тепер у вас є можливість додати «Spacer», це лише порожній віджет, який можна використовувати для зміни положення інших віджетів. Це може бути корисним для створення складніших макетів або для додавання простору між віджетами. Наприклад, якщо ви хочете мати деякі елементи керування з кнопками вгору/вниз/ліворуч/праворуч, ви можете використати прокладку, щоб розділити та вирівняти їх:

![(left) A d-pad controller layout using spacers, (right) the spacer's highlighted to demonstrate their positioning](https://flowfuse.com/img/spacer-example-AU_VauCu1g-1688.jpeg)

*(ліворуч) Розташування контролера d-pad із використанням spacers , (праворуч) spacer's виділена, щоб продемонструвати їхнє розташування*

Spacers можуть бути будь-якої ширини та висоти, і вони завжди відображатимуть порожній простір. Щоб додати нову spacer, ви можете натиснути кнопку «+» на бічній панелі інформаційної панелі біля будь-якої групи. Потім ви також можете змінити порядок віджетів там (змінити порядок віджетів у редакторі візуального макета буде незабаром).