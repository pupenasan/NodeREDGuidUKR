## Рецепти JSONata

[Джерело](https://it.knightnet.org.uk/kb/nr-qa/jsonata/)

### Загальні

#### Доступ до глобального контексту

Доступ до глобального контексту відбувається через вбудовану у Node-RED JSONata функцію `$globalContext()` в якій вказується назва змінної та за необхідності сховище (другим аргументом). Наприклад, наступний приклад доступається до змінної глобального контексту з іменем  'globalVariableName'.

![](media/getcontext_expml.png)

#### Доступ до контексту потоку

Аналогічно попередній, функція `$flowContext()` доступається до контексту потоку.

На наступному прикладі вихідна змінна формується у JSON форматі з двох властивостей, в одній з яких вказується значення змінної глобального контексту, а в іншій - контексту потоку.     

```
{
  "aGlobalVariable": $globalContext('globalVariableName'),
  "aFlowVariable": $flowContext('flowVariableName')
}
```

#### Отримання значення елементу з контекстної змінної

Цей приклад показує, як витягти елемент із змінної контексту на основі `msg.topic` та припускаючи, що у назва змінної введена у властивості `topic`. Прикладом може бути глобальна змінна, введена на ідентифікатор датчика, яка містить місця датчиків, в якій треба додати місцеположення до даних датчика для передачі MQTT. 

```json
{
   "location": $globalContext('locations["' & topic & '"]'),
   "origPayload": payload
}
```

Тут використовуються дві властивості повідомлення `topic` для формування частини змінної - індексу масиву `locations` з глобального контексту та `payload`, яка вміщує значення. 

#### Доступ до об'єкту `msg`

До властивостей об'єкта доступаються безпосередньо через імена, наприклад `msg.payload` доступний просто як "payload". Якщо ви хочете отримати доступ до всього об'єкту `msg`, вам потрібно використовувати змінну `$` на верхньому рівні виразу. Наприклад: 

```json
$._msgid
```

поверне унікальний ідентифікатор повідомлення Якщо ви користуєтесь функціями або іншими дужками, ви можете використовувати `$$` для доступу до об'єкта верхнього рівня.

#### Складний приклад

Витягує ключі та значення з початкового `msg`, копіює оригінальний `msg.payload`, додає додаткові дані об’єкта та відмітку часу. Ілюструє використання функцій та змінних.

```json
(
    $lookupVals := function($i) { $lookup($$, $i) };
    $origMsgVals := $map($keys($$), $lookupVals);
    {
      "meta": { "a": 1, "thisIs":"more data" },
      "origPayload": payload,
      "origMsgKeys": $keys($$),
      "origMsgVals": $origMsgVals,
      "timestamp": $now()
    }
)
```

#### Посилання на індекс в масиві 

Ви можете [прив’язати змінну до послідовності, а потім використовувати послідовність всередині подальшої обробки](http://docs.jsonata.org/next/processing#jsonata-path-processing). Наприклад, щоб додати посилання зі списку до вихідного масиву:

```json
(
    /* Reference Array */
    $x := ["In","Out"];

    /* The old-fashioned way of doing things
     * using a map function
     */
    /*
    $map(payload, function($v, $i, $a) {
        {
            "data": $x[$i],
            "value":$v.value
        }
    });
    */

    /* The newer and MUCH simpler way
     * where the #$y binds the $y variable
     * to the input array.
     */
    payload#$y.[{
        "data": $x[$y],
        "value":$.value
    }]
)
```

дає результат

```json
[
    {
        "data": "In",
        "value": 139061084
    },
    {
        "data": "Out",
        "value": 12177618
    }
]
```

з вхідного повідомлення

```json
{
    "payload": [
        {
            "oid": "1.3.6.1.2.1.2.2.1.10.8",
            "type": 65,
            "value": 139061084,
            "tstr": "Counter"
        },
        {
            "oid": "1.3.6.1.2.1.2.2.1.16.8",
            "type": 65,
            "value": 12177618,
            "tstr": "Counter"
        }
    ]
}
```

### Рецепти для вузла Change 

#### Добавлення верхніх рівнів до теми повідомлення

Використовуйте `Set` для `msg.topic` разом з наступним виразом JSONata:

```json
"EXTRA/LEVELS/" & topic
```

#### Відтворення повідомлення в msg.payload

Попередні приклади застаріли станом на січень 2018 року із впровадженням Node-RED v0.18. Це побачило зміну до JSONata v1.5, що дає кілька інших можливостей.

```json
{
  "topic": topic,
  "payload": $,
  "_msgid": _msgid
}
```

Сказане буде працювати чудово. Однак якщо оригінальне повідомлення походить від вузла `http-in` або подібного, воно буде містити кругові посилання та багато даних і спричинять проблеми. Щоб цього уникнути, використовуйте нову функцію `$clone()`. Node-RED перевантажує це безпечною версією, яка дозволяє уникнути проблем принаймні з повідомленнями `http-in`.

```json
{
  "topic": topic,
  "payload": $clone($),
  "_msgid": _msgid
}
```

Для довідки, ось попередня пропозиція:

Іноді ви можете захотіти перенести вміст `msg` на `msg.payload`. Наприклад, якщо ви хотіли відправити `msg` як налагодження до MQTT. Ви не можете це зробити безпосередньо (встановивши `msg.payload` в `$`), оскільки система вважає, що це кругове посилання і блокує його. Тому вам доведеться відтворити `msg` вручну. Я включаю список ключів `msg`, щоб ви могли знати, чи щось ви пропустили.

```json
{
  "topic": topic,
  "payload": payload,
  "_msgid": _msgid,
  "msgKeys": $keys($),
}
```

Безсумнівно, є й інші способи зробити це більш автоматизованим способом.

Зробивши це трохи далі, ви також можете отримати ключі та значення початкового `msg` у масиві:

```json
(
    $spread($)
)
```

#### Розділення мульти-рядкових string в змінні ‘property=value’

Деякі вихідні дані командного рядка, які можуть бути повернуті з вузла `exec`, можуть містити складний рядок у такому форматі, як наприклад виконання команди `set` в Windows 10:

```json
ALLUSERSPROFILE=C:\ProgramData
CommonProgramFiles=C:\Program Files\Common Files
CommonProgramFiles(x86)=C:\Program Files (x86)\Common Files
CommonProgramW6432=C:\Program Files\Common Files
ComSpec=C:\WINDOWS\system32\cmd.exe
...
```

Якщо ви хочете розділити це на наступний формат:

```json
[
    {"ALLUSERSPROFILE":"C:\\ProgramData\r"},
    {"CommonProgramFiles":"C:\\Program Files\\Common Files\r"},
    {"CommonProgramFiles(x86)":"C:\\Program Files (x86)\\Common Files\r"},
    {"CommonProgramW6432":"C:\\Program Files\\Common Files\r"},
    {"ComSpec":"C:\\WINDOWS\\system32\\cmd.exe\r"},
    ...
]
```

Ви можете використовувати такі JSONata:

```json
(
    /* Split on newline */
    $x := $split(payload, "\n");

    /* Map function to split 'property=value' and return as object */
    $s := function($line) {
        (
            $ss := $split($line, "=");
            { $ss[0] : $ss[1] }
        )
    };

    /* Run the map to return the required array of objects */
    $map($x, $s)
)
```

### Створення payload що містить масив

Як обробити комбінацію масиву/об'єкта плюс обчислити true/false прапор з 2 властивостей масиву.

Наприклад вхідне повідомлення msg:

```json
{
    "payload": [
        {
            "Station ID": "3015432",
            "Station Name": "Sg.Klang di Tmn Sri Muda 1",
            "District": "Petaling",
            "River Basin": "Sg.Klang",
            "Last Update": "30/12/2017 01:30",
            "River Level (m)": "1.13",
            "Normal": "2.80",
            "Alert": "4.40",
            "Warning": "4.58",
            "Danger": "5.00"
        },
        {
            "Station ID": "3015490",
            "Station Name": "Sg.Damansara di TTDI Jaya",
            "District": "Petaling",
            "River Basin": "Sg.Klang",
            "Last Update": "30/12/2017 01:30",
            "River Level (m)": "13.35",
            "Normal": "3.50",
            "Alert": "7.30",
            "Warning": "7.80",
            "Danger": "8.30"
        }
    ]
}
```

Приклад JSONata для переформатування результатів

```json
payload.(
	{
		"station": $.'Station ID',
    	"name": $.'Station Name',
        "level": $.'River Level (m)',
        "alert": $number($.'River Level (m)') > $number($.Alert) ? true : false
    }
)
```

Виробляє:

```json
[
  {
    "station": "3015432",
    "name": "Sg.Klang di Tmn Sri Muda 1",
    "level": "1.13",
    "alert": false
  },
  {
    "station": "3015490",
    "name": "Sg.Damansara di TTDI Jaya",
    "level": "13.35",
    "alert": true
  }
]
```

Див https://groups.google.com/forum/#!topic/node-red/J0020rPetAY для детальнішої інформації.

### Перетворення масиву об'єктів в об'єкт з об'єктними полями 

Дано масив об'єктів, таких як:

```json
{
    "payload": [
        {
            "id": 5,
            "Name": "Bedroom 2",
            "CalculatedTemperature": 192,
            "CurrentSetPoint": 125
        },
         {
            "id": 6,
            "OverrideType": "Manual",
            "OverrideTimeoutUnixTime": 1534182107,
            "OverrideSetpoint": 125,
            "Name": "Master Bedroom",
            "Mode": "Auto",
            "CalculatedTemperature": 192,
            "CurrentSetPoint": 125
        }
    ]
}
```

Якщо ми хочемо перетворити це на вкладений об'єкт, використовуючи одне із внутрішніх властивостей об’єктів для назви кожного зовнішнього запису, ми можемо зробити наступне:

```json
payload{
    $.Name : {
        "id": $.id,
        "Name": $.Name,
        "CurrentTemperature": $.CalculatedTemperature/10,
        "DesiredTemperature": $.CurrentSetPoint/10,
        "Override": $.OverrideType?"Yes":"No",
        "OverrideTimeout": $.OverrideType?$split($split($fromMillis($.OverrideTimeoutUnixTime),"T")[1],".")[0]:"N/A"
    }
}
```

Що дає нам такий вихід:

```json
{
  "Bedroom 2": {
    "id": 5,
    "Name": "Bedroom 2",
    "CurrentTemperature": 19.2,
    "DesiredTemperature": 12.5,
    "Override": "No",
    "OverrideTimeout": "N/A"
  },
  "Master Bedroom": {
    "id": 6,
    "Name": "Master Bedroom",
    "CurrentTemperature": 19.2,
    "DesiredTemperature": 12.5,
    "Override": "Yes",
    "OverrideTimeout": "18:09:42"
  }
}
```

Зверніть увагу на відсутність `.` Між `payload`  і `{` в JSONata. Якщо ми додамо `.` між ними, ми отримаємо масив, що містить об'єкт, що містить об'єкт, що містить оригінальний об'єкт!

Ви можете бачити це в дії в потоках з цієї публікації про керування з [Drayton Wiser smart heating system](https://it.knightnet.org.uk/kb/nr-qa/drayton-wiser-heating-control/)

#### Більш простий приклад перетворення масиву в об’єкт 

З огляду на вхід:

```json
{
    "payload": [
        {
            "oid": "1.3.6.1.2.1.2.2.1.10.8",
            "type": 65,
            "value": 139061084,
            "tstr": "Counter"
        },
        {
            "oid": "1.3.6.1.2.1.2.2.1.16.8",
            "type": 65,
            "value": 12177618,
            "tstr": "Counter"
        }
    ]
}
```

Цей JSONata буде витягувати значення на об'єкт, що вводиться в контрольний масив:

```json
(
    $x := ["In","Out"];

    payload#$y{ $x[$y]: $.value }
)
```

Output object:

```json
{
    "In": 139061084,
    "Out": 12177618
}
```

Хитрість тут полягає в тому, що між вхідним масивом (`payload`) та фігурними дужками об'єкта немає крапки. Це також показує використання зв'язаної змінної індексу.

### Рецепти вузла Switch (Node-RED v0.18+)

#### Блокування/розблокування потоку

У наступному вузлі використовується глобальна змінна для блокування або розблокування потоку.

Встановіть "Властивість" вузла Switch на щось подібне:

```json
$globalContext('myBlockingVarName')
```

то використовуйте єдине правило "є істинним" або "неправдивим" за потребою.