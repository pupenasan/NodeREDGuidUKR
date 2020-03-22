## cos put (зберегти об’єкт в IBM COS)

![img](media/cos_put.png) Цей вузол відправляє об’єкт на збереження в IBM COS (рис.13.3). 

![img](media/13_3.png)

рис.13.3.Налаштування вузлу cos put

Вузол має входи:

- `payload (string | buffer)` – корисне навантаження повідомлення (вміст об’єкту), що ініціює відправку. 
- `bucket (string)` – існуючий bucket, в який буде збережено об’єкт.
- `create (string)` – назва bucket, що потрібно створити, якщо він не існує. Опція Create вказує чи потрібно створювати новий bucket.
- `objectname (string)` – унікальне ім’я збереженого файлу в Cloud Object Storage Service.
- `mode (string)` – показує звідки завантажувати вміст об’єкту, з файлу чи з корисного навантаження.
- `filename (string)` – ім’я файлу, якщо завантаження відбувається з файлу 
- `filepath (string)` – шлях до файлу, , якщо завантаження відбувається з файлу.
- `geturl (Boolean)` якщо необхідно отримати URL об’єкту, тоді вказується `true`.

Вузол має виходи.

Стандартний вихід:  

- `payload (string)` – вузол повертає     об’єкт `msg.payload`, або     записує в `filename`, якщо використовується режим збереження в     файл.
- `objectname (string)`  – ім’я об’єкту  `msg.objectname`.
- `url (string)` – Якщо `msg.geturl` встановлено, `msg.url` буде містити WebLink URL на об’єкт.

Вихід при помилці:

- `error (string)` – код помилки.

Поле `msg.payload` вміщує завантажений файл, або у випадку режиму запису в файл є тільки тригером, що показує на те, що файл записано. 

Параметри налаштування вузла `msg.filename`, `msg.filepath` та  `msg.fileformat` є типово встановленими значеннями і можуть бути переписані відповідними полями вхідного повідомленнями.

Вузол повертає `msg.payload` і назву об’єкту `msg.objectname` або `msg.error` з кодом помилки. 

Якщо необхідно отримати URL об’єкту, що генерується, необхідно активувати поле HMAC. 

Вузол використовує S3-API функції IBM Cloud Object Storage Service. 