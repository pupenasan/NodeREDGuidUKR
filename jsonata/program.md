## Програмні конструкції 

До цих пір ми ввели всі частини мови, які дозволяють нам витягувати дані з вхідного JSON-документа, об'єднувати дані за допомогою рядкових і числових операторів і форматувати структуру вихідного документа JSON. Тим не менше JSONata можна використовувати як повноцінну мову програмування Тьюрінга.

### Коментарі

​      У виразах JSONata можуть бути використані коментарі з використанням синтаксису стилю мови «C».

```json
/* Long-winded expressions might need some explanation */
(
  $pi := 3.1415926535897932384626;
  /* JSONata is not known for its graphics support! */
  $plot := function($x) {(
    $floor := $string ~> $substringBefore(?, '.') ~> $number;
    $index := $floor(($x + 1) * 20 + 0.5);
    $join([0..$index].('.')) & 'O' & $join([$index..40].('.'))
  )};
  
  /* Factorial is the product of the integers 1..n */
  $product := function($a, $b) { $a * $b };
  $factorial := function($n) { $n = 0 ? 1 : $reduce([1..$n], $product) };
  
  $sin := function($x){ /* define sine in terms of cosine */
    $cos($x - $pi/2)
  };
  $cos := function($x){ /* Derive cosine by expanding Taylor's series */
    $x > $pi ? $cos($x - 2 * $pi) : $x < -$pi ? $cos($x + 2 * $pi) :
      $sum([0..12].($power(-1, $) * $power($x, 2*$) / $factorial(2*$)))
  };

  [0..24].$sin($*$pi/12).$plot($)
)
```

рис.11.1. Приклад використання коментарів у виразах JSONata

Подивіться на цей приклад в дії http://try.jsonata.org/ryYn78Q0m  

### Побудова умов

​      Умовні конструкції «Якщо/тоді/інакше» будуються з використанням умовних операторів "? :"

```javascript
predicate ? expr1 : expr2
```

Оцінюється вираз `predicate`. Якщо вираз повертає `true` тоді оцінюється вираз `expr1` і повертається його значення, інакше обробляється вираз `expr2`.

Таблиця 11.15.

див. http://try.jsonata.org/

| **JSONata**            | **Result** |
| ---------------------- | ---------- |
| `35.6>20.1 ? 12 : 10 ` | `12`       |
| `35.6<20.1 ? 12 : 10`  | `10`       |

### Змінні

​      Будь які назви, що починаються з знаку '$' є змінними. **Змінна** – це поіменоване посилання на значення. Значення може бути одним із будь-яких типів серед [системних типів](http://docs.jsonata.org/processing#the-jsonata-type-system). Є також вбудовані в JSONata змінні:

- `$` - змінна без імені посилається на     значення контексту у будь якій точці вхідної ієрархії JSON.
- `$$` - корінь входу JSON. Тільки     потребується у випадках для виходу з теперішнього контексту для     тимчасового переходу вниз в інший шлях. Наприклад для перехресного посилання     або об’єднання даних.  
- Рідні (вбудовані) функції.  Див функції.

### Зв’язування змінних

​      Значення можуть бути зв’язані зі змінними наступним чином:

```json
$var_name := "value"
```

Збережене значення може бути позначено пізніше за допомогою виразу `$var_name`

Область видимості змінних обмежена ‘блоком’ в якому відбувалось зв’язування. Наприклад:

```json
Invoice.(
  $p := Product.Price;
  $q := Product.Quantity;
  $p * $q
)
```

Повертає значення Price помножений на Quantity в Product з Invoice.

### Функції 

 Функції є першокласним типом і можуть бути збережені в змінних подібно іншим типам. JSONata забезпечує глобальну бібліотеку вбудованих функцій, що назначені змінним в глобальній області видимості. Наприклад, $uppercase вміщує функцію, яка при виклику зі строковим аргументом str, буде повертати рядок з усіма символам в str, зміненими в верхній регістр.    
               Функції викликаються з вказівкою аргументів в дужках. Приклади:

- `$uppercase("Hello")` повертає рядок "HELLO".
- `$substring("hello world", 0, 5)` повертає     рядок "hello"
- `$sum([1,2,3])` повертає число 6

Анонімна (лямбда) функція може бути означена, використовуючи наступний синтаксис:

```js
function($l, $w, $h){ $l * $w * $h }
```

і може бути викликана з допомогою:

```js
function($l, $w, $h){ $l * $w * $h }(10, 10, 5)
```

що поверне результат 500
	Функція може бути назначена змінній для наступного використання (всередині блоку):

```json
$volume := function($l, $w, $h){ $l * $w * $h };
  $volume(10, 10, 5);
)
```

​	Функції можуть бути означені за допомогою додаткових підписів, яка означують типи параметрів функції. Якщо це передбачено, перш ніж функція буде викликана, будуть перевірятися аргументи. Якщо список аргументів не відповідає підпису, виникне динамічна помилка виникає.
​	Сигнатура функції це рядок в формі `<params:return>.params`  – це послідовність символів типу, кожен з яких представляє тип вхідних аргументів. `return` – це символ типу, що представляє тип вихідного значення функції. Нижче наведені типи:

Прості типи:

- `b` - Boolean
- `n` - number
- `s` - string
- `l` - `null`

Складені типи:

- `a` - array
- `o` - object
- `f` - function

Типи об’єднання:

- `(sao)` - string, array або object
- `(o)` – те саме що і `o`
- `u` - еквівалентно `(bnsl)` тобто Boolean, number, string або `null`
- `j` – будь-який тип JSON. Еквівалентно `(bnsloa)` тобто Boolean, number, string, `null`, object або array, але не function
- `x` - будь-який тип, Еквівалентно `(bnsloaf)`

Параметричні типи:

- `a` - масив рядків 
- `a` - масив значень будь-яких типів

Декілька прикладів сигнатур вбудованих функцій JSONata:

- `$count` має сигнатуру  ``;     приймає масив і повертає число.
- `$append` має сигнатуру ``; приймає два масиви і повертає масив.
- `$sum` має сигнатуру `:n>`; приймає масив чисел і повертає число.
- `$reduce` має сигнатуру `:j>`; приймає редукуючу функцію `f` і `a` (масив об’єктів JSON objects) і повертає об’єкт     JSON.

Кожен тип символу може також мати *options*.

- `+` - один або більше аргументів цього типу 

- - E.g. `$zip` has      signature ``; it accepts one array, or two arrays, or three      arrays, or...

- `?` – опійний аргумент 

- - E.g. `$join` has      signature `s?:s>`; it accepts an array of strings and an optional      joiner string which defaults to the empty string. It returns a string.

- `-` - якщо аргумент відстуній, використовується     значення контексту ("focus"). 

- - E.g. `$length`      has signature ``; it can be      called as `$length(OrderID)` (one argument) but equivalently as `OrderID.$length()`.

Функції, призначені для змінних, можуть викликати себе, використовуючи це посилання змінної. Це дозволяє визначити рекурсивні функції. Наприклад. 

```
(
  $factorial:= function($x){ $x <= 1 ? 1 : $x * $factorial($x-1) };
  $factorial(4)
)                   
```

поверне `24`

 Зауважимо, що фактично можна написати рекурсивну функцію, використовуючи суто анонімні функції (тобто нічого не присвоюється змінним). Це робиться за допомогою комбінатора Y, який може бути цікавим викликом для тих, хто цікавиться функціональним програмуванням.
               Більше про функції можна прочитати [за цим посиланням](http://docs.jsonata.org/programming#functions).

### Використання регулярних виразів

​      Про регулярні вирази можна прочитати [за цим посиланням](http://docs.jsonata.org/regex). 

### Робота з датою та часом

Є дві функції, які повертають відмітку часу: 

1. [`$now()`](http://docs.jsonata.org/date-time-functions#now) повертає відмітку часу в     форматі рядку ISO 8601.
2. [`$millis()`](http://docs.jsonata.org/date-time-functions#millis) повертає ту саму     відмітку часу як кількість мілісекунд починаючи з опівночі 1-го січня 1970     UTC (the [Unix epoch](https://en.wikipedia.org/wiki/Unix_time)).

Відмітка часу фіксується з початку оцінювання виразу, і та сама відмітка часу повертається для кожного входження `$now()` або `$millis()` в тому самому виразі протягом тривалості оцінювання. Наприклад:

Таблиця 11.17.

| JSONata | `{`  ` "invoiceTime": $now(),`  ` "total": $sum(Account.Order.Product.(Price * Quantity)),`  ` "closingTime": $now()`  `}` |
| ------- | ------------------------------------------------------------ |
| Result  | `{`   ` "invoiceTime":  "2018-12-10T13:49:51.141Z",`   ` "total": 336.36,`   ` "closingTime":  "2018-12-10T13:49:51.141Z"`   `}` |

ISO 8601 формат:

```json
{"myDateTime": "2018-12-10T13:45:00.000Z" }
```



Таблиця 11.18.

| JSONata | `$toMillis('10/12/2018', '[D]/[M]/[Y]') ~> $fromMillis('[M]/[D]/[Y]')` |
| ------- | ------------------------------------------------------------ |
| Result  | `"12/10/2018"`                                               |

Таблиця 11.19.

| JSONata | `$toMillis('10/12/2018', '[D]/[M]/[Y]') ~> $fromMillis('[FNn], [D1o] [MNn] [YI]')` |
| ------- | ------------------------------------------------------------ |
| Result  | `"Monday, 10th December MMXVIII"`                            |



### Оператори

#### Navigation Operators

- [`.` (Map)](http://docs.jsonata.org/control-operators#map)
- [`[...] (Filter)`](http://docs.jsonata.org/control-operators#filter)
- [`~>` (Chain)](http://docs.jsonata.org/control-operators#chain)
- [`^(`...`)`      (Order-by)](http://docs.jsonata.org/control-operators#order-by)
- [`... ~> | ... | ... |` (Transform)](http://docs.jsonata.org/control-operators#transform-)
- [`&` (Concatenation)](http://docs.jsonata.org/control-operators#concatenation)
- [`? :` (Conditional)](http://docs.jsonata.org/control-operators#conditional)
- [`:=` (Variable binding)](http://docs.jsonata.org/control-operators#variable-binding)

#### Numeric Operators

- [`+` (Addition)](http://docs.jsonata.org/numeric-operators#addition)
- [`-` (Substraction/Negation)](http://docs.jsonata.org/numeric-operators#substraction-negation)
- [`*` (Multiplication)](http://docs.jsonata.org/numeric-operators#multiplication)
- [`/` (Division)](http://docs.jsonata.org/numeric-operators#division)
- [`%` (Modulo)](http://docs.jsonata.org/numeric-operators#modulo)
- [`..` (Range)](http://docs.jsonata.org/numeric-operators#range)

#### Comparison Operators

- [`=` (Equals)](http://docs.jsonata.org/comparison-operators#equals)
- [`!=` (Not equals)](http://docs.jsonata.org/comparison-operators#not-equals)
- [`>` (Greater than)](http://docs.jsonata.org/comparison-operators#greater-than)
- [`<` (Less than)](http://docs.jsonata.org/comparison-operators#less-than)
- [`>=` (Greater than or equals)](http://docs.jsonata.org/comparison-operators#greater-than-or-equals)
- [`<=` (Less than or equals)](http://docs.jsonata.org/comparison-operators#less-than-or-equals)
- [`in` (Inclusion)](http://docs.jsonata.org/comparison-operators#in-inclusion)

#### Boolean Operators

- [`and` (Boolean AND)](http://docs.jsonata.org/boolean-operators#and-boolean-and)
- [`or` (Boolean OR)](http://docs.jsonata.org/boolean-operators#or-boolean-or)

### Бібліотека функцій 

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

#### Object functions

- [`$keys()`](http://docs.jsonata.org/object-functions#keys)
- [`$lookup()`](http://docs.jsonata.org/object-functions#lookup)
- [`$spread()`](http://docs.jsonata.org/object-functions#spread)
- [`$merge()`](http://docs.jsonata.org/object-functions#merge)
- [`$sift()`](http://docs.jsonata.org/object-functions#sift)
- [`$each()`](http://docs.jsonata.org/object-functions#each)

#### Date/Time functions

1. [`$now()`](http://docs.jsonata.org/date-time-functions#now)
2. [`$millis()`](http://docs.jsonata.org/date-time-functions#millis)
3. [`$fromMillis()`](http://docs.jsonata.org/date-time-functions#frommillis)
4. [`$toMillis()`](http://docs.jsonata.org/date-time-functions#tomillis)

#### Higher order functions

- [`$map()`](http://docs.jsonata.org/higher-order-functions#map)
- [`$filter()`](http://docs.jsonata.org/higher-order-functions#filter)
- [`$reduce()`](http://docs.jsonata.org/higher-order-functions#reduce)
- [`$sift()`](http://docs.jsonata.org/higher-order-functions#sift)