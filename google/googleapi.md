| [На головну](../) | [ < Розділ > ](README.md) |
| ----------------- | ------------------------- |
|                   |                           |

# Вузол для роботи з Google API ([node-red-contrib-google](https://flows.nodered.org/node/node-red-contrib-google))

## Можливості

Цей вузол є обгорткою для офіційних клієнтських API API Node.js: [google-api-nodejs-client](https://github.com/google/google-api-nodejs-client).

Список доступних API надається в Інтернеті через [Google API Discovery Service](https://developers.google.com/discovery/).

Пакет містить два вузли:

- вузол конфігурації, створений для підтримки зв’язку з сервісами Google API (*google-conn*) 
- та звичайний вузол, що забезпечує можливість виклику будь-якого методу будь-якого API, відкритого через офіційний клієнт `Node.js` Google.

## Конфігурування

- Створіть новий сервісний обліковий запис, якщо його ще немає та завантажте об’єкт облікових даних JSON для нього. Надайте цьому обліковому запису доступ до необхідних сервісів. Детальніше можете ознайомитися за [цим посиаланням](https://pupenasan.github.io/ProgIngContrSystems/%D0%94%D0%BE%D0%B2%D1%96%D0%B4%D0%BD%D0%B8%D0%BA%D0%B8/googleauth.html?fbclid=IwAR0nyEx86eXOWj1xzy8Ddt0KcDc5XC4zw50yGmg8JXoplGPurO4W_6XtZ6A) 


- Вставте вміст цього файлу в поле Ключ JSON вашого *google-conn* вузла.