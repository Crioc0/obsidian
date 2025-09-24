---
created: 2025-09-24 10:20
tags:
  - backend
  - basic
  - mongodb
  - database
База данных:
  - "[[02 Structure notes/MongoDB|MongoDB]]"
aliases:
  - objectId
---
# 202509241020

*Ссылка на исходник или контекст (если есть):* https://www.mongodb.com/docs/manual/core/document/#the-_id-field

В MongoDB есть уникальный идентификатор, который создается автоматически. Также его можно задать самостоятельно. ObjectId состоит из трех значений : текущей временной метки (timestamp), случайного числа и счётчика.

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
### Связанные идеи:
* [[202509240819 Какие типы данных есть в MongoDB]]
* [[202509231654 Что такое MongoDB]]
---

*Что стоит развить? Какие вопросы возникли?*