[<- На головну](../)  [Розділ](README.md)

# Функції JSONata 

## Додаткові функції Node-RED

- [`$env`]() - зчитує змінну середовища з вказаним іменем
- [`$flowContext`](recipes.md#доступ-до-глобального-контексту) - доступається до контексту потоку
- [`$globalContext`](recipes.md#доступ-до-контексту-потоку) - доступається до глобального контексту
- [`$clone`](recipes.md#відтворення-повідомлення-в-msg-payload) - клонує об'єкт  

## String functions

- [`$string()`](http://docs.jsonata.org/string-functions#string)

- [`$length()`](http://docs.jsonata.org/string-functions#length)

- [`$substring()`](http://docs.jsonata.org/string-functions#substring)

- [`$substringBefore()`](http://docs.jsonata.org/string-functions#substringbefore)

- [`$substringAfter()`](http://docs.jsonata.org/string-functions#substringafter)

- [`$uppercase()`](http://docs.jsonata.org/string-functions#uppercase)

- [`$lowercase()`](http://docs.jsonata.org/string-functions#lowercase)

- [`$trim()`](http://docs.jsonata.org/string-functions#trim)

- [`$pad()`](http://docs.jsonata.org/string-functions#pad)

- [`$contains()`](http://docs.jsonata.org/string-functions#contains)

- [`$split()`](http://docs.jsonata.org/string-functions#split)

- [`$join()`](http://docs.jsonata.org/string-functions#join)

- [`$match()`](http://docs.jsonata.org/string-functions#match)

- [`$replace()`](http://docs.jsonata.org/string-functions#replace)

- [`$eval()`](http://docs.jsonata.org/string-functions#eval)

- [`$base64encode()`](http://docs.jsonata.org/string-functions#base64encode)

- [`$base64decode()`](http://docs.jsonata.org/string-functions#base64decode)

- [`$decodeURL`](https://docs.jsonata.org/string-functions#decodeurl)

- [`$decodeURLComponent`](https://docs.jsonata.org/string-functions#decodeurlcomponent)

- [`$encodeURL`](https://docs.jsonata.org/string-functions#encodeurl)

- [`$encodeURLComponent`](https://docs.jsonata.org/string-functions#encodeurlcomponent)

## Numeric functions

- [`$number()`](http://docs.jsonata.org/numeric-functions#number)
- [`$abs()`](http://docs.jsonata.org/numeric-functions#abs)
- [`$floor()`](http://docs.jsonata.org/numeric-functions#floor)
- [`$ceil()`](http://docs.jsonata.org/numeric-functions#ceil)

### round

[`$round()`](http://docs.jsonata.org/numeric-functions#round)

Повертає значення параметра `number`, округлене до кількості десяткових знаків, указаної необов’язковим параметром `precision`. Параметр `precision` (який має бути цілим числом) означує кількість знаків після коми в округленому числі. Якщо `precision` не вказано, за замовчуванням використовується значення 0, а число округлюється до найближчого цілого числа. Якщо «точність» є від’ємною, тоді її значення вказує, до якого стовпця округляти ліворуч від десяткового знака. Ця функція використовує [Round_half_to_even](https://en.wikipedia.org/wiki/Rounding#Round_half_to_even) . Ця стратегія зазвичай використовується у фінансових розрахунках і є стандартним режимом округлення в IEEE 754.

**Приклади**

`$round(123.456)` => `123` 

`$round(123.456, 2)` => `123.46`

`$round(123.456, -1)` => `120` 

`$round(123.456, -2)` => `100`

`$round(11.5)` => `12`

`$round(12.5)` => `12` 

`$round(125, -1)` => `120`



- [`$power()`](http://docs.jsonata.org/numeric-functions#power)
- [`$sqrt()`](http://docs.jsonata.org/numeric-functions#sqrt)
- [`$random()`](http://docs.jsonata.org/numeric-functions#random)
- [`$formatNumber()`](http://docs.jsonata.org/numeric-functions#formatnumber)
- [`$formatBase()`](http://docs.jsonata.org/numeric-functions#formatbase)
- [`$formatInteger()`](http://docs.jsonata.org/numeric-functions#formatinteger)
- [`$parseInteger()`](http://docs.jsonata.org/numeric-functions#parseinteger)

## Numeric aggregation functions

- [`$sum()`](http://docs.jsonata.org/aggregation-functions#sum)
- [`$max()`](http://docs.jsonata.org/aggregation-functions#max)
- [`$min()`](http://docs.jsonata.org/aggregation-functions#min)
- [`$average()`](http://docs.jsonata.org/aggregation-functions#average)

## Boolean functions

- [`$boolean()`](http://docs.jsonata.org/boolean-functions#boolean)
- [`$not()`](http://docs.jsonata.org/boolean-functions#not)
- [`$exists()`](http://docs.jsonata.org/boolean-functions#exists)

## Array Functions

- [`$count()`](http://docs.jsonata.org/array-functions#count)
- [`$append()`](http://docs.jsonata.org/array-functions#append)
- [`$sort()`](http://docs.jsonata.org/array-functions#sort)
- [`$reverse()`](http://docs.jsonata.org/array-functions#reverse)
- [`$shuffle()`](http://docs.jsonata.org/array-functions#shuffle)
- [`$zip()`](http://docs.jsonata.org/array-functions#zip)
- [`$distinct`](https://docs.jsonata.org/array-functions#distinct)

## Object functions

- [`$keys()`](http://docs.jsonata.org/object-functions#keys)
- [`$lookup()`](http://docs.jsonata.org/object-functions#lookup)
- [`$spread()`](http://docs.jsonata.org/object-functions#spread)
- [`$merge()`](http://docs.jsonata.org/object-functions#merge)
- [`$sift()`](http://docs.jsonata.org/object-functions#sift)
- [`$each()`](http://docs.jsonata.org/object-functions#each)
- [`$type()`](https://docs.jsonata.org/object-functions.html#type)
- [`$error()`](https://docs.jsonata.org/object-functions.html#error)

## Date/Time functions

Функції забезпечують отримання плинних дати та часу та їх перетворення. 

У більшості з функцій фігурує аргумент `picture`, який задає формат текстового представлення дати/часу. Якщо він не вказаний, то вважається, що формат мітки часу – ISO 8601 на кшталт `"2017-11-07T15:12:37.121Z"` . Якщо він вказаний то має задаватися в форматі аналогічному XPath/XQuery функції [fn:format-dateTime](https://www.w3.org/TR/xpath-functions-31/#func-format-dateTime), що означена в специфікації XPath F&O 3.1. Параметр `picture` складається з послідовності маркерів змінних і літеральних підрядків. Підрядок, укладений у квадратні дужки, інтерпретується як маркер змінної; підрядки, не взяті в квадратні дужки, сприймаються як підрядки літералів. Літеральні підрядки є необов’язковими і, якщо вони присутні, відтворюються без змін, включаючи будь-які пробіли. Якщо відкриваюча або закриваюча квадратна дужка потрібна в літеральному підрядку, її потрібно подвоїти. Маркери змінних замінюються в результаті на рядки, що представляють аспекти дати та/або часу, які потрібно відформатувати. Вони детально описані нижче.               

Маркер змінної складається зі специфікатора компонента, за яким необов’язково слідує один або два модифікатори представлення та/або необов’язково модифікатор ширини. Пробіли в маркері змінної ігноруються.

Маркер змінної можна розділити на компоненти, застосовуючи такі правила:    

1. Специфікатор компонента завжди присутній і завжди складається з однієї літери.
2. Модифікатор ширини можна розпізнати за наявністю коми.
3. Підрядок між специфікатором компонента та комою (якщо є) або кінцем рядка (якщо коми немає) містить перший і другий модифікатори представлення, обидва з яких є необов’язковими. Якщо цей підрядок містить один символ, це інтерпретується як перший модифікатор представлення. Якщо він містить більше одного символу, перевіряється останній символ: якщо він дійсний як другий модифікатор представлення, тоді він розглядається як такий, і попередня частина підрядка становить перший модифікатор представлення. В іншому випадку другий модифікатор представлення вважається відсутнім, а весь підрядок інтерпретується як перший модифікатор представлення.

*Специфікатор компонента* вказує на потрібний компонент дати або часу та приймає такі значення:

| Специ-фіктаор | Значення                                                     | модифікатор представлення за замовченням |
| :------------ | :----------------------------------------------------------- | :--------------------------------------- |
| Y             | year (absolute value)                                        | 1                                        |
| M             | month in year                                                | 1                                        |
| D             | day in month                                                 | 1                                        |
| d             | day in year                                                  | 1                                        |
| F             | day of week                                                  | n                                        |
| W             | week in year                                                 | 1                                        |
| w             | week in month                                                | 1                                        |
| H             | hour in day (24 hours)                                       | 1                                        |
| h             | hour in half-day (12 hours)                                  | 1                                        |
| P             | am/pm marker                                                 | n                                        |
| m             | minute in hour                                               | 01                                       |
| s             | second in minute                                             | 01                                       |
| f             | fractional seconds                                           | 1                                        |
| Z             | timezone                                                     | 01:01                                    |
| z             | timezone (same as Z, but modified where appropriate to include a prefix    as a time offset using GMT, for example GMT+1 or GMT-05:00. For this component there    is a fixed    prefix of `GMT`, or a localized    variation thereof for the chosen language, and the remainder of the value is formatted    as for specifier `Z`. | 01:01                                    |
| C             | calendar: the name or abbreviation of a calendar name        | n                                        |
| E             | era: the name of a baseline for the numbering of years, for example    the reign of a monarch | n                                        |

Перший *модифікатор представлення* вказує на стиль, у якому має бути представлено значення компонента. Його значення може бути:

- будь-який маркер формату, дозволений як основний маркер формату в другому аргументі функції [`fn:format-integer`](https://www.w3.org/TR/xpath-functions-31/#func-format-integer ), який вказує, що значення компонента має бути виведено в числовому вигляді, використовуючи вказаний числовий формат, наприклад:
  -  `1` - одна цифа
  - `01` - дві цифри
  - `i` - римські числа літерами нижнього регістру
  - `I` - римські числа літерами верхнього регістру
  - `w` - символьне позначення числа у нижньому регістрі,
  - `W` -  символьне позначення числа у верхньому регістрі
  - ` Ww` -  символьне позначення числа у нижньому регістрі які починаються з великої літери
- маркер формату `n`, `N` або `Nn`, що вказує, що значення компонента має бути виведено за назвою, у нижньому, верхньому регістрі або в заголовку відповідно. Компоненти, які можна виводити за назвою, включають (але не обмежуються ними) місяці, дні тижня, часові пояси та ери. Якщо процесор не може вивести ці компоненти за іменами для вибраного календаря та мови, тоді він має використовувати [·implementation-defined·](https://www.w3.org/TR/xpath-functions-31/#implementation-defined ) резервне представлення.

Якщо кома має використовуватися як роздільник групування в маркері формату, тоді має бути специфікатор ширини. Точніше: якщо маркер змінної містить одну або більше ком, остання кома розглядається як введення модифікатора ширини, а всі інші розглядаються як розділювачі груп. Отже, `[Y9,999,*]` виведе рік як `2,008`.  Неможливо використовувати закриваючу квадратну дужку як роздільник групування в маркері формату. Якщо реалізація не підтримує використання потрібного маркера формату, вона повинна використовувати модифікатор представлення за замовчуванням для цього компонента. 



### now

[`$now()`](http://docs.jsonata.org/date-time-functions#now)

```js
$now([picture [, timezone]])
```

Створює відмітку часу UTC у форматі, сумісному зі стандартом ISO 8601, і повертає її як рядок. Усі виклики `$now()` у межах оцінки виразу повертатимуть однакове значення позначки часу. Якщо вказано додаткові параметри `picture` та `timezone`,  поточна позначка часу форматується відповідно до вказаних параметрів.

Приклад

```js
$now() => "2017-05-15T15:12:59.152Z"
```

### millis

[`$millis()`](http://docs.jsonata.org/date-time-functions#millis)

Повертає кількість мілісекунд після *епохи* Unix (1 січня 1970 UTC) у вигляді числа. Усі виклики `$millis()` під час обчислення виразу повертатимуть однакове значення.

**Приклад** 

`$millis()` => `1502700297574`

### fromMillis

[`$fromMillis()`](http://docs.jsonata.org/date-time-functions#frommillis)

`$fromMillis(number [, picture [, timezone]])` 

Перетворює `number`, яке представляє мілісекунди з *Епохи* Unix (1 січня 1970 року за UTC), у відформатований рядок подання мітки часу, як зазначено в рядку `picture `. Якщо необов’язковий параметр `picture` опущено, мітка часу буде відформатована у форматі [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html). 

**Приклади** 

`$fromMillis(1510067557121)` => `"2017-11-07T15:12:37.121Z"` 

`$fromMillis(1510067557121, '[M01]/[D01]/[Y0001] [h#1]:[m01][P]')` => `"11/07/2017 3:12pm"` 

`$fromMillis(1510067557121, '[H01]:[m01]:[s01] [z]', '-0500')` => `"10:12:37 GMT-05:00"`

### toMillis

[`$toMillis()`](http://docs.jsonata.org/date-time-functions#tomillis)



## Higher order functions

- [`$map()`](http://docs.jsonata.org/higher-order-functions#map)
- [`$filter()`](http://docs.jsonata.org/higher-order-functions#filter)
- [`$reduce()`](http://docs.jsonata.org/higher-order-functions#reduce)
- [`$sift()`](http://docs.jsonata.org/higher-order-functions#sift)
- [`$single()`](https://docs.jsonata.org/higher-order-functions#single)