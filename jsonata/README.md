[<- На головну](../)

# 11. Робота з JSONata 

[JSONata](http://docs.jsonata.org/overview) - це мова запитів і перетворень даних JSON. Іншими словами це мова яка вказує як з вхідного JSON зробити вихідний JSON. 

Для маніпулювання та об'єднання відібраних даних передбачено набір вбудованих операторів і функцій, а результати запитів можуть бути відформатовані в будь-яку вихідну структуру JSON, використовуючи звичний JSON-об'єкт і синтаксис масиву. У поєднанні з можливістю створення функцій, визначених користувачем, можна розробити додаткові вирази для вирішення будь-яких JSON-запитів і завдань трансформації.

З загальною документацією по JSONata можна ознайомитися на сайті http://docs.jsonata.org. У цьому розділі наведено деякі вирізки з цієї документації та напрацювання з інших джерел відносно використання в Node-RED. Перевірити загальні вирази JSONata можна на прикладі - http://try.jsonata.org/ 

## Доступ до об'єктів `Node-RED`

JSONata використовується в багатьох вузлах Node-RED. У якості вхідних даних для JSONata є змінна повідомлення `msg`, яка розглядається як вхідний документ JSON. Тому до властивостей об'єкта `msg` доступаються безпосередньо через імена, наприклад `msg.payload` доступний просто як `payload`. Наприклад, у наступному прикладі у вихідний `msg.payload` записується значення вхідного `msg.payload` збільшеного на 1. 

![](media/exmpl1.png)

JSONata проводить послідовні розрахунки відповідно до вказаного виразу. Після кожного розрахунку результат знаходиться в певній контекстній змінній (називатимо розрахунковий контекст), який можна використовувати в наступних розрахунках. Звернутися до контексту можна через знак  `$`. Перед початком розрахунків в контексті знаходиться вхідний документ, тобто `msg`, тому звертатись до нього можна через  `$`. Тобто, якщо потрібно отримати доступ до всього об'єкту `msg` на верхньому рівні виразу, можна використовувати змінну `$` . Наприклад `$._msgid` поверне унікальний ідентифікатор повідомлення. Якщо звертання йде всередині розрахунку, то розрахунковий контекст буде містити проміжні результати, тому при необхідності оцінювання вхідного документу до нього звертаються через подвійний "долар" `$$` 

З символу  `$` починаються також усі функції JSONata та змінні користувача. Останні використовуються тоді, коли є необхідність писати не просто вирази а підпрограми на мові JSONata. Див. [Програмні конструкції](program.md).    

У розрахунках можна також використовувати літеральні константи у форматі JavaScript, значення глобального контексту та контексту потоку, значення змінної середовища та комбінацію всього перерахованого. 

Аналогічно як Java Script через крапку можна доступатися до полів властивостей будь якого рівня вкладеності, а через `[]` до індексу масиву. Однак в JSONata квадратні дужки використовуються також для позначення умови пошуку (**предикату**). 

Якщо результат треба перетворити в інший вигляд, використовуються конструктори масивів (`[]`)  та об'єктів (`{}`). Так наступне повідомлення сформує обєкт з двома полями, в одне запише `payload` вхідного повідомлення, а в інше - `topic`.

```json
{"value" : payload , "name" : topic }
```

 А у цьому прикладі сформується масив:

```json
[payload , topic]
```

Доступ до контекстів потоку та глобального контексту можна робити через відповідні функції. Доступ до глобального контексту відбувається через вбудовану у Node-RED JSONata функцію `$globalContext()` в якій вказується назва змінної та за необхідності сховище (другим аргументом). Наприклад, наступний приклад доступається до змінної глобального контексту з іменем  'globalVariableName'.

![](media/getcontext_expml.png)

Аналогічно попередній, функція `$flowContext()` доступається до контексту потоку.

## Вирази (огляд)

Для рядків у JSONata можна використовувати оператор конкатенації  `&`. Наприклад у наступному прикладі якщо вхідний  `msg.payload=23` а `msg.topic='Temperature'` то вихідний `msg.payload` дорівнюватиме `Temperature = 23`.   

![](media/exmpl2.png)

Числові літетерали та вирази можуть бути використані в розрахунках результатів з використанням звичайних математичних операторів:

- `+` додавання
- `-` віднімання
- `*` множення
- `/` ділення
- `%` остача від ділення 
- `..` (Range) означення діпазону

На наступному прикладі на виході `msg.payload` формується масив елементів зі значеннями від 1 до 100.  

![](media/exmpl3.png)



Можна використовувати оператори порівняння двох значень, які повертають логічні значення `true` або `false`: 

- `=` дорівнює
- `!=` не дорівнює
- `<` менше ніж
- `<=` менше ніж чи дорівнює
- `>` більше ніж
- `>=` більше або дорівнює ніж
- `in` значення міститься в масиві

Для логічного об'єднання булевих результатів використовуються оператори `and` та `or`. Зверніть увагу, що булеве `not` підтримується як окрема функція ([$not](http://docs.jsonata.org/boolean-functions#not)), а не як оператор.

Ось ще кілька прикладів:

```json
[1..3, 7..9] => [1, 2, 3, 7, 8, 9] 
[1..$count(Items)].("Item " & $) => ["Item 1","Item 2","Item 3"]
[1..5].($*$) => [1, 4, 9, 16, 25]
```

## Оператори шляху

[Джерело](https://docs.jsonata.org/path-operators)

| Оператор                                                     | Пояснення                                                    | Приклад |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| [`.` (Map)](https://docs.jsonata.org/path-operators#-map)    | Вираз оцінюється для отримання масиву значень. Якщо це буде одне значення, воно трактується як еквівалент масиву, що містить це єдине значення. Якщо порожній масив, то результат вираження оператора - це nothing<br />For each value in the LHS array in turn: The value is known as the *context* and is used as the basis for any relative path expression on the RHS.  It is also accessible in the RHS expression using the `$` symbol. The RHS expression is evaluated to produce a value or array of  values (or nothing).  These values are appended to a combined array of  results for the operator as a whole.<br /><br />Для кожного значення в розрахованому масиві: Значення відоме як *контекст* і використовується як основа для будь-якого відносного вираження контуру на RHS. Він також доступний у виразі RHS, використовуючи символ `$`. Експресія RHS оцінюється для отримання значення або масиву значень (або нічого). Ці значення додаються до комбінованого масиву результатів для оператора в ціломуThe combined result of the operator is returned. |         |
| [`[` ... `]` (Filter)](https://docs.jsonata.org/path-operators#---filter) |                                                              |         |
| [`^(` ... `)` (Order-by)](https://docs.jsonata.org/path-operators#---order-by) |                                                              |         |
| [`{` ... `}` (Reduce)](https://docs.jsonata.org/path-operators#---reduce) |                                                              |         |
| [`*` (Wildcard)](https://docs.jsonata.org/path-operators#-wildcard) |                                                              |         |
| [`**` (Descendants)](https://docs.jsonata.org/path-operators#-descendants) |                                                              |         |
| [`%` (Parent)](https://docs.jsonata.org/path-operators#-parent) |                                                              |         |
| [`#` (Positional variable binding)](https://docs.jsonata.org/path-operators#-positional-variable-binding) |                                                              |         |
| [`@` (Context variable binding)](https://docs.jsonata.org/path-operators#-context-variable-binding) |                                                              |         |



## Перелік функцій

Опис функцій українською доступний в окремому [розділі](functions.md) тут наведений тільки перелік та короткий опис.

#### Додаткові функції Node-RED

- [`$env`]() - зчитує змінну середовища з вказаним іменем
- [`$flowContext`](recipes.md#доступ-до-глобального-контексту) - доступається до контексту потоку
- [`$globalContext`](recipes.md#доступ-до-контексту-потоку) - доступається до глобального контексту
- [`$clone`](recipes.md#відтворення-повідомлення-в-msg-payload) - клонує об'єкт  

#### String functions

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

#### Numeric functions

- [`$number()`](http://docs.jsonata.org/numeric-functions#number)
- [`$abs()`](http://docs.jsonata.org/numeric-functions#abs)
- [`$floor()`](http://docs.jsonata.org/numeric-functions#floor)
- [`$ceil()`](http://docs.jsonata.org/numeric-functions#ceil)
- [`$round()`](http://docs.jsonata.org/numeric-functions#round)
- [`$power()`](http://docs.jsonata.org/numeric-functions#power)
- [`$sqrt()`](http://docs.jsonata.org/numeric-functions#sqrt)
- [`$random()`](http://docs.jsonata.org/numeric-functions#random)
- [`$formatNumber()`](http://docs.jsonata.org/numeric-functions#formatnumber)
- [`$formatBase()`](http://docs.jsonata.org/numeric-functions#formatbase)
- [`$formatInteger()`](http://docs.jsonata.org/numeric-functions#formatinteger)
- [`$parseInteger()`](http://docs.jsonata.org/numeric-functions#parseinteger)

#### Numeric aggregation functions

- [`$sum()`](http://docs.jsonata.org/aggregation-functions#sum)
- [`$max()`](http://docs.jsonata.org/aggregation-functions#max)
- [`$min()`](http://docs.jsonata.org/aggregation-functions#min)
- [`$average()`](http://docs.jsonata.org/aggregation-functions#average)

#### Boolean functions

- [`$boolean()`](http://docs.jsonata.org/boolean-functions#boolean)
- [`$not()`](http://docs.jsonata.org/boolean-functions#not)
- [`$exists()`](http://docs.jsonata.org/boolean-functions#exists)

#### Array Functions

- [`$count()`](http://docs.jsonata.org/array-functions#count)
- [`$append()`](http://docs.jsonata.org/array-functions#append)
- [`$sort()`](http://docs.jsonata.org/array-functions#sort)
- [`$reverse()`](http://docs.jsonata.org/array-functions#reverse)
- [`$shuffle()`](http://docs.jsonata.org/array-functions#shuffle)
- [`$zip()`](http://docs.jsonata.org/array-functions#zip)
- [`$distinct`](https://docs.jsonata.org/array-functions#distinct)

#### Object functions

- [`$keys()`](http://docs.jsonata.org/object-functions#keys)
- [`$lookup()`](http://docs.jsonata.org/object-functions#lookup)
- [`$spread()`](http://docs.jsonata.org/object-functions#spread)
- [`$merge()`](http://docs.jsonata.org/object-functions#merge)
- [`$sift()`](http://docs.jsonata.org/object-functions#sift)
- [`$each()`](http://docs.jsonata.org/object-functions#each)
- [`$type()`](https://docs.jsonata.org/object-functions.html#type)
- [`$error()`](https://docs.jsonata.org/object-functions.html#error)

#### Date/Time functions

1. [`$now()`](http://docs.jsonata.org/date-time-functions#now)
2. [`$millis()`](http://docs.jsonata.org/date-time-functions#millis)
3. [`$fromMillis()`](http://docs.jsonata.org/date-time-functions#frommillis)
4. [`$toMillis()`](http://docs.jsonata.org/date-time-functions#tomillis)
5. [`$single`](https://docs.jsonata.org/higher-order-functions#single)

#### Higher order functions

- [`$map()`](http://docs.jsonata.org/higher-order-functions#map)
- [`$filter()`](http://docs.jsonata.org/higher-order-functions#filter)
- [`$reduce()`](http://docs.jsonata.org/higher-order-functions#reduce)
- [`$sift()`](http://docs.jsonata.org/higher-order-functions#sift)
- [`$single()`](https://docs.jsonata.org/higher-order-functions#single)

## Інші можливості

- [Приклад використання в застосунках Node-RED](examples.md)<span class="load"> </span>
- [Прості запити](simple.md)<span class="load"> </span>
- [Предикативні запити (Predicate Queries)](predicate.md) <span class="load"> </span>
- [Вирази](expression.md) <span class="load"> </span>
- [Структурування результату](structureresult.md) <span class="load"> </span>
- [Запити композиції (Query composition)](composition.md) <span class="load"> </span>
- [Сортування, групування і агрегація](sort.md)<span class="load"> </span> 
- [Програмні конструкції](program.md) 
- [Рецепти](recipes.md)

## 

