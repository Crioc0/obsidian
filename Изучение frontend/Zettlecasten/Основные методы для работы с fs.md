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
## Создание папок
С этим поможет метод `fs.mkdir`. Он принимает два параметра: имя новой папки и колбэк с единственным аргументом — ошибкой. Первым параметром можно передать имя папки вместе с путём, где нужно создать папку.
```ts
import fs from 'fs';

fs.mkdir('incomingData/data', (err) => {
  if (err) console.log(err);
});
```
## Запись данных в файл
`
Для этого есть метод `fs.writeFile`. Принимает три параметра:

- файл, куда нужно записать данные;
- сами данные, записанные строкой;
- колбэк для обработки ошибки.
```ts
import fs from 'fs';

fs.writeFile('data.json', JSON.stringify([1, 2, 3]), (err) => {
  if (err) console.log(err);
});
```
## Удаление файлов
Это делает метод `fs.unlink`. У него два параметра: имя файла и колбэк для обработки ошибок.
```ts
import fs from 'fs';

fs.unlink('data.json', (err) => {
  if (err) {
    console.log(err);
    return;
  }

  console.log('Файл удалён!');
});
```