# Node-RED Contrib Browser Utils

https://github.com/ibm-early-programs/node-red-contrib-browser-utils

Вузли Node-RED для таких функцій браузера, як завантаження файлів, камера та мікрофон.

```
npm install node-red-contrib-browser-utils
```

## Camera

![image-20230405152348486](media/image-20230405152348486.png)

Браузер робить знімок камерою за замовчуванням, коли натискається кнопка поруч із вузлом. Вузол виводить його як буфер PNG. Вузол `camera` має затримку 2000 мс, щоб запобігти повільному запуску драйвера камери, що спричиняє проблеми в деяких браузерах.

Підтримувані браузери

- Chrome
- Firefox

## Microphone

![image-20230405152341525](media/image-20230405152341525.png)

Браузер починає запис після натискання кнопки поруч із вузлом і припиняє його, коли кнопку натискає знову. Вузол виводить його як буфер WAV.

## File upload

![image-20230405152332516](media/image-20230405152332516.png)

Вузол приймає файл для завантаження та виводить його як буфер.