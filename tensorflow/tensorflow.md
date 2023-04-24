# Робота з tensorflow

Щоб використовувати вузли з tensorflow у Node-RED необхідно поставити  `@tensorflow/tfjs-node` .

## Особливості встановлення @tensorflow/tfjs-node на Windows 

https://www.npmjs.com/package/@tensorflow/tfjs-node

- встановити середовище збирання Visual C++:  [Visual Studio Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools) (using "Visual C++ build tools" workload) or [Visual Studio Community](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community) (using the "Desktop development with C++" workload)
- встановити `node-gyp`

```
npm install -g node-gyp
```



### Джерела

### Встановлення на Windows 

Для підтримки збірки Windows і OSX для `node-gyp` потрібен Python 2.7. Перед встановленням `@tensorflow/tfjs-node` або `@tensorflow/tfjs-node-gpu` переконайтеся, що у вас є ця версія. Машини з Python 3.x не встановлять прив’язки належним чином.

*Щоб дізнатися більше про усунення несправностей у Windows, перегляньте [WINDOWS_TROUBLESHOOTING.md](windowstroubleshooting.md).*

#### Встановлення `node-gyp`

https://github.com/nodejs/node-gyp

Установіть поточну версію Python із [пакета Microsoft Store](https://www.microsoft.com/en-us/p/python-310/9pjpw5ldxlz5).

Встановіть інструменти та конфігурацію вручну:

- Установіть середовище збирання Visual C++:  [Visual Studio Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools) (using "Visual C++ build tools" workload) or [Visual Studio Community](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community) (using the "Desktop development with C++" workload)
- Запустіть cmd, `npm config set msvs_version 2017`

Якщо наведені вище кроки вам не допомогли, перегляньте [Microsoft's Node.js Guidelines for Windows](https://github.com/Microsoft/nodejs-guidelines/blob/master/windows-environment.md#compiling-native-addon-modules) fдля отримання додаткових порад.

Щоб націлити нативний ARM64 Node.js у Windows 10 на ARM, додайте компоненти "Visual C++ compilers and libraries for ARM64" and  "Visual C++ ATL for ARM64".



