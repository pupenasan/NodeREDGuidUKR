# TensorFlow.js Node.js bindings Windows troubleshooting

https://github.com/tensorflow/tfjs/blob/HEAD/tfjs-node/WINDOWS_TROUBLESHOOTING.md

Пакет tfjs-node використовує пакет [node-gyp](https://github.com/nodejs/node-gyp) для обробки крос-компіляції коду C++, необхідного для прив’язки TensorFlow до Node.js. Це міжплатформне рішення може бути дещо складним на платформах Windows. У цьому посібнику наведено посилання на рішення, перевірені через проблеми в основному [tfjs repo](https://github.com/tensorflow/tfjs).

## 'The system cannot find the patch specified' Exceptions

Це може статися з різних причин. По-перше, перевірте, або не вистачає

- або `cd node_modules/@tensorflow/tfjs-node`, 
- або клонуйте [репозиторій tensorflow/tfjs](https://github.com/tensorflow/tfjs).

Після `cd` або клонування виконайте таку команду (може знадобитися node-gyp інсталювати глобально `npm install -g node-gyp`):

```
node-gyp configure --verbose
```

### Missing `python2`

З докладного виведення, якщо ви бачите щось на зразок:

```
gyp verb check python checking for Python executable "python2" in the PATH
gyp verb `which` failed Error: not found: python2
```

Це означає, що node-gyp очікує «python2» exe десь у `%PATH%`. Спробуйте запустити цю команду від адміністратора (підказка з підвищеними привілейованими правами):

Ви можете спробувати запустити це з адміністративної підказки:

```
$ npm --add-python-to-path='true' --debug install --global windows-build-tools
```

### Щось ще?

Якщо з’являється інший відсутній компонент, надішліть повідомлення про проблему на [tensorflow/tfjs](https://github.com/tensorflow/tfjs/issues/new) із результатом команди `node-gyp configure --verbose`.

## msbuild.exe Exceptions

Перевірте трасування повного стека за допомогою команди `npm install` (або `yarn`). Якщо ви бачите щось на кшталт:

```
gyp ERR! stack Error: C:\Program Files (x86)\MSBuild\14.0\bin\msbuild.exe failed with exit code: 1
```

Можливо, вам доведеться встановити системні інструменти вручну. Це можна зробити за допомогою:

```
npm install -g --production windows-build-tools
```

Якщо це все одно не працює, спробуйте повторно запустити наведену вище команду в привілейованій оболонці.