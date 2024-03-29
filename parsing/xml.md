[<- На головну](../)  [Розділ](README.md)

## XML

![img](media/xml.png) Перетворює рядок XML в об’єкт JavaScript та в зворотному напрямку напрямку.

![img](media/xml_cfg.png)

На вході очікує властивості:

- `payload` (*object або string*) -- JavaScript object або XML string.

- `options`(*object*) -- цю необов'язкову властивість можна використовувати для передачі будь-якого з параметрів, підтримуваних базовою бібліотекою, що використовується для перетворення в XML і з нього. Докладнішу інформацію див. ничче 

На виході вузол формує повідомлення:

- `payload` (*object або string*)
  - якщо вхід є string, вузол пробує парсити його як XML та перетворити в JavaScript object.
  - якщо вхід є JavaScript object він пробує з нього створити XML string.

При перетворенні між XML і об'єктом будь-які атрибути XML додаються як властивість за назвою `$` за замовчуванням. Будь-який текстовий вміст додається як властивість під назвою `_`. Ці імена властивостей можна вказати в конфігурації вузла.

Наприклад, наступний фрагмент XML 

```
<p class="tag">Hello World</p>
```


буде конвертовано в об'єкт:

```json
{
  "p": {
    "$": {
      "class": "tag"
    },
    "_": "Hello World"
  }
}
```

Приклад перетворення XML в Object показаний на рисунку нижче. Для атрибута `priority` використане назва властивості-обєкта  `$`, що має такий атрибут. Для включених тегів створюються масиви зі значеннями.

![img](media/xmltoob.png)

Приклад перетворення з Object в XML показаний на рисунку нижче.

![img](media/toxml.png)

### Options

Описані у документах [the xml2js docs](https://github.com/Leonidas-from-XIV/node-xml2js/blob/master/README.md#options)

Apart from the default settings, there are a number of options that can be
specified for the parser. Options are specified by ``new Parser({optionName:
value})``. Possible options are:

  * `attrkey` (default: `$`): Prefix that is used to access the attributes.
    Version 0.1 default was `@`.
  * `charkey` (default: `_`): Prefix that is used to access the character
    content. Version 0.1 default was `#`.
  * `explicitCharkey` (default: `false`) Determines whether or not to use 
    a `charkey` prefix for elements with no attributes.
  * `trim` (default: `false`): Trim the whitespace at the beginning and end of
    text nodes.
  * `normalizeTags` (default: `false`): Normalize all tag names to lowercase.
  * `normalize` (default: `false`): Trim whitespaces inside text nodes.
  * `explicitRoot` (default: `true`): Set this if you want to get the root
    node in the resulting object.
  * `emptyTag` (default: `''`): what will the value of empty nodes be. In case
    you want to use an empty object as a default value, it is better to provide a factory
      function `() => ({})` instead. Without this function a plain object would
    become a shared reference across all occurrences with unwanted behavior.
  * `explicitArray` (default: `true`): Always put child nodes in an array if `true`; otherwise an array is created only if there is more than one.
  * `ignoreAttrs` (default: `false`): Ignore all XML attributes and only create
    text nodes.
  * `mergeAttrs` (default: `false`): Merge attributes and child elements as
    properties of the parent, instead of keying attributes off a child
    attribute object. This option is ignored if `ignoreAttrs` is `true`.
  * `validator` (default `null`): You can specify a callable that validates
    the resulting structure somehow, however you want. See unit tests
    for an example.
  * `xmlns` (default `false`): Give each element a field usually called '$ns'
    (the first character is the same as attrkey) that contains its local name
    and namespace URI.
  * `explicitChildren` (default `false`): Put child elements to separate
    property. Doesn't work with `mergeAttrs = true`. If element has no children
    then "children" won't be created. Added in 0.2.5.
  * `childkey` (default `$$`): Prefix that is used to access child elements if
    `explicitChildren` is set to `true`. Added in 0.2.5.
  * `preserveChildrenOrder` (default `false`): Modifies the behavior of
    `explicitChildren` so that the value of the "children" property becomes an
    ordered array. When this is `true`, every node will also get a `#name` field
    whose value will correspond to the XML nodeName, so that you may iterate
    the "children" array and still be able to determine node names. The named
    (and potentially unordered) properties are also retained in this
    configuration at the same level as the ordered "children" array. Added in
    0.4.9.
  * `charsAsChildren` (default `false`): Determines whether chars should be
    considered children if `explicitChildren` is on. Added in 0.2.5.
  * `includeWhiteChars` (default `false`): Determines whether whitespace-only
     text nodes should be included. Added in 0.4.17.
  * `async` (default `false`): Should the callbacks be async? This *might* be
    an incompatible change if your code depends on sync execution of callbacks.
    Future versions of `xml2js` might change this default, so the recommendation
    is to not depend on sync execution anyway. Added in 0.2.6.
  * `strict` (default `true`): Set sax-js to strict or non-strict parsing mode.
    Defaults to `true` which is *highly* recommended, since parsing HTML which
    is not well-formed XML might yield just about anything. Added in 0.2.7.
  * `attrNameProcessors` (default: `null`): Allows the addition of attribute
    name processing functions. Accepts an `Array` of functions with following
    signature:
    ```javascript
    function (name){
        //do something with `name`
        return name
    }
    ```
    Added in 0.4.14
  * `attrValueProcessors` (default: `null`): Allows the addition of attribute
    value processing functions. Accepts an `Array` of functions with following
    signature:
    ```javascript
    function (value, name){
      //do something with `name`
      return name
    }
    ```
    Added in 0.4.1
  * `tagNameProcessors` (default: `null`): Allows the addition of tag name
    processing functions. Accepts an `Array` of functions with following
    signature:
    ```javascript
    function (name){
      //do something with `name`
      return name
    }
    ```
    Added in 0.4.1
  * `valueProcessors` (default: `null`): Allows the addition of element value
    processing functions. Accepts an `Array` of functions with following
    signature:
    ```javascript
    function (value, name){
      //do something with `name`
      return name
    }
    ```
    Added in 0.4.6