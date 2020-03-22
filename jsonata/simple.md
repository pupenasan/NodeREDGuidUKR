## Прості запити 

Для підтримки вилучення значень зі структури JSON означений **синтаксис шляху розташування**. Це дозволяє вибрати всі можливі значення в документі, які відповідають вказаному **шляху розташування** (location path). В JSON  є дві структурні конструкції - це об'єкти і масиви. Нижче показаний синтаксис роботи з ними в JSONata.

### Прості приклади навігації об'єктами JSON

У таблиці 11.1 показні прості приклади задавання пошуку в ``JSONata``. Можна перевірити ці приклади, перейшовши на сайт `http://try.jsonata.org/ (виберіть приклад Address).

При вказівки простих запитів шляху слід дотримуватися наступних правил. При пошуку полів з пробілами вони вказуються в спеціальних лапках ` `` `. Якщо індекс в шуканому масиві не є цілим, він округляється до цілого. Негативне значення індексу в масиві шукає значення відраховане з кінця, наприклад `arr[-1]` бере останній елемент, а `arr[-2] ` - бере передостанній. Якщо індекс не вказується – береться весь масив. Якщо при цьому масив містить об'єкти, а шлях розташування вибирає поля в цих об'єктах, то для кожного об'єкта в масиві буде запрошено вибір.

Приклад:

```json
{
  "FirstName": "Fred",
  "Surname": "Smith",
  "Age": 28,
  "Address": {
    "Street": "Hursley Park",
    "City": "Winchester",
    "Postcode": "SO21 2JN"
  },
  "Phone": [
    {
      "type": "home",
      "number": "0203 544 1234"
    },
    {
      "type": "office",
      "number": "01962 001234"
    },
    {
      "type": "office",
      "number": "01962 001235"
    },
    {
      "type": "mobile",
      "number": "077 7700 1234"
    }
  ],
  "Email": [
    {
      "type": "work",
      "address": ["fred.smith@my-work.com", "fsmith@my-work.com"]
    },
    {
      "type": "home",
      "address": ["freddy@my-social.com", "frederic.smith@very-serious.com"]
    }
  ],
  "Other": {
    "Over 18 ?": true,
    "Misc": null,
    "Alternative.Address": {
      "Street": "Brick Lane",
      "City": "London",
      "Postcode": "E1 6RF"
    }
  }
}
```

Таблиця 11.1.

| **JSONata**              | **Result**                                                   |
| ------------------------ | ------------------------------------------------------------ |
| `Surname`                | `"Smith"`                                                    |
| `Age`                    | `28`                                                         |
| `Address.City`           | `"Winchester"`                                               |
| `Other.Misc`             | `null`                                                       |
| `Other.Nothing`          | *undefined*                                                  |
| `Other.`Over 18 ?``  ` ` | `true`                                                       |
| `Phone[0]`               | `{ "type": "home", "number": "0203 544 1234" }`              |
| `Phone[-1]`              | `{ "type": "mobile", "number": "077 7700 1234" }`            |
| `Phone[-2]`              | `{ "type": "office", "number": "01962 001235" }`             |
| `Phone[8]`               | *undefined*                                                  |
| `Phone[0].number`        | `"0203 544 1234"`                                            |
| `Phone.number`           | `[ "0203 544 1234", "01962 001234", "01962 001235", "077 7700 1234" ]` |
| `Phone.number[0]`        | `[ "0203 544 1234", "01962 001234", "01962 001235", "077 7700 1234" ]` |
| `(Phone.number)[0]`      | `"0203 544 1234"`                                            |
| `Phone[[0..1]]`          | `[   { "type": "home", "number": "0203 544 1234" },   { "type": "office", "number": "01962 001234" }  ]` |

### Пусті послідовності та послідовності з одним елементом

Візьмемо приклад:

```json
[
 { "ref": [ 1,2 ] },
 { "ref": [ 3,4 ] }
]
```

На верхньому рівні ми маємо масив, а не об'єкт. Якщо ми хочемо вибрати перший (0-й) об'єкт у цьому масиві, то необхідно вказати назву об’єкту верхнього рівня, до якого треба додати [0]. Ми не можемо використовувати [0] самостійно, тому що стикаємося з синтаксисом конструктора масиву. Однак, ми можемо використовувати посилання контексту *$* (*context*) для посилання на початок документа наступним чином:

Приклад:

```json
[
  { "ref": [ 1,2 ] },
  { "ref": [ 3,4 ] }
]
```

Таблиця 11.2.

| **JSONata**     | **Result**           | **Коментар**                                                 |
| --------------- | -------------------- | ------------------------------------------------------------ |
| `$[0]`          | `{ "ref": [ 1,2 ] }` | `$` на початку виразу відноситься до всього вхідного документа |
| `$[0].ref`  ` ` | `[ 1,2 ] `  ` `      | `.ref` тут повертає  весь внутрішній масив                   |
| `$[0].ref[0]`   | `1`                  | повертає елемент на  першу позицію внутрішнього масиву       |
| `$.ref`         | `[ 1, 2, 3, 4 ]`     | Незважаючи на  структуру вкладеного масиву, результуючий вибір сплющується в один плоский  масив. Початкова вкладена структура вхідних масивів втрачається. |