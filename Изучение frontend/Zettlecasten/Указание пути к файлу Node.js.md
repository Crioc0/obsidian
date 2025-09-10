2025 09 1011 49
Tags: #javaScript 
###### Links: 
1) 
# Заметка
Не стоит указывать что относительные пути, так как в случае перемещения исполняемого файла код перестанет работать из за того, что отностельный путь высчитывается от файла, где исполняется код.
Нужно задавать динамические пути, то есть не прописывать путь явно, а получать его из информации о самом модуле.
## Получение информации о модуле
Любой модуль Node.js содержит информацию о самом себе и окружении. Внутри любого модуля есть переменный `__filename` и `__dirname`. Они хранят имя файла модуля и путь к папке, где лежит модуль соответственно.
```ts
// app.ts

console.log(__filename); // /usr/local/project/app.js
console.log(__dirname); // /usr/local/project
```
## Преобразование пути
Для преобразования пути используется модуль `path` и метод `join`.Он учитывает контекст, поэтому не возникнет проблем с разделителями
```ts
// read-file.ts

import * as fsPromises from 'fs/promises';
import path from 'path';

export const readFile = () => {
  const filepath = path.join(__dirname, 'file.txt'); // собрали абсолютный путь к файлу
  fsPromises.readFile(filepath, { encoding: 'utf8' })
    .then((data) => {
      console.log(data);
    })
    .catch(err => {
      console.log(err);
    });
};
```