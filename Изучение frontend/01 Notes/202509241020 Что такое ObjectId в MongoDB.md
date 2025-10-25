---
created: 2025-09-24 10:20
tags:
  - backend
  - basic
  - mongodb

aliases:
  - objectId

repeat: spaced every 48 hours
due_at: 2025-10-26T08:32:30.918+03:00
---
# 202509241020 Что такое ObjectId в MongoDB

*Ссылка на StructureNote:* [[02 Structure notes/MongoDB|MongoDB]]

*Ссылка на исходник или контекст (если есть):* [[202509240819 Типы данных есть в MongoDB]]

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

* https://www.mongodb.com/docs/manual/core/document/#the-_id-field

---

*Что стоит развить? Какие вопросы возникли?*
