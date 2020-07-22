[<- На головну](../)

# 11. Робота з JSONata 

[JSONata](http://docs.jsonata.org/overview) - це мова запитів і перетворень для даних JSON. Для маніпулювання та об'єднання відібраних даних передбачено набір вбудованих операторів і функцій, а результати запитів можуть бути відформатовані в будь-яку вихідну структуру JSON, використовуючи звичний JSON-об'єкт і синтаксис масиву. У поєднанні з можливістю створення функцій, визначених користувачем, можна розробити додаткові вирази для вирішення будь-яких JSON-запитів і завдань трансформації.

Документація - http://docs.jsonata.org 

Перевірка на прикладі - http://try.jsonata.org/ 

- [Приклад використання в застосунках Node-RED](examples.md)<span class="load"> </span>
- [Прості запити](simple.md)<span class="load"> </span>
- [Предикативні запити (Predicate Queries)](predicate.md) <span class="load"> </span>
- [Функції та вирази](function.md) <span class="load"> </span>
- [Структурування результату](structureresult.md) <span class="load"> </span>
- [Запити композиції (Query composition)](composition.md) <span class="load"> </span>
- [Сортування, групування і агрегація](sort.md)<span class="load"> </span> 
- [Програмні конструкції](program.md) 
- [Рецепти](recipes.md)

## Перелік функцій

#### Функції Node-RED

- [$env]() - доступається до змінної середовища
- [$flowContext](recipes.md#доступ-до-глобального-контексту) - доступається до контексту потоку
- [$globalContext](recipes.md#доступ-до-контексту-потоку) - доступається до глобального контексту
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