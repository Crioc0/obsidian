2025 09 1011 59
Tags: #nodejs 
###### Links: 
1) 
# Заметка
## Чтение всех файлов директории
Для этого есть метод `fs.readdir`. Он читает все файлы внутри директории. Первый аргумент метода — путь к директории. Второй — колбэк, в котором описано, что делать с полученными данными.
```ts
import fs from 'fs';
// колбэк-версия метода readdir
fs.readdir('.', (err, files) => {
  if (err) {
        console.log(`Произошла ошибка ${err.message}`)
    return;
  }

  console.log('data: ', files);
});
```
Если работа с Promise-версией, в случае успеха результат попадет в обработчик `then`, а ошибка будет обработана в методе catch
Это справедливо для всех методов модуля `fs`
```ts
import fs from 'fs';
// а вот так можно работать с его Promise-собратом
fs.promises.readdir('.')
    .catch((err)=>console.log(`Произошла ошибка ${err.message}`))
    .then((files)=>console.log('data: ', files))
```