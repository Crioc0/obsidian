2025 09 1214 42
Tags: #mongodb
###### Links: 
1) 
# Заметка
Данные в MongoDB хранятся в формате BSON (binary JSON) — расширение над форматом JSON. Поэтому MongoDB поддерживает все типы данных, которые есть в JSON. Но помимо них есть и другие: ObjectId, Date, Regular Expression и даже JavaScript .Со всеми типами вы можно ознакомиться [в документации](https://mongodb.prakticum-team.ru/docs/manual/reference/bson-types/).
Тип ObjectId создан для уникальных итендефикаторов. У каждого документа такой создается автоматически, но его можно добавить  самостоятельно.
ObjectId складывается из трёх значений: текущей временной метки (timestamp), случайного числа и счётчика. Такой состав ObjectId обеспечивает уникальность значения.

В JavaScript с ObjectId чаще всего работают просто как со строкой, но для запросов к MongoDB необходимо конструировать именно объект:
```ts
import { ObjectId } from 'mongodb';

// строка со значением ObjectId
const _id = "507f1f77bcf86cd799439011";

// такой запрос ничего не вернёт, потому что мы передали строку вместо объекта ObjectId
db.collection.find({ _id: _id });

// а этот запрос сработает правильно
db.collection.find({ _id: new ObjectId(_id) });
```