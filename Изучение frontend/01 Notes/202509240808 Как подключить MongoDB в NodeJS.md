---
created: 2025-09-24 08:08
tags:
  - backend
  - mongodb
  - nodejs
  - basic


---
# 202509240808 Как подключить MongoDB в NodeJS

*Ссылка на StructureNote:* [[02 Structure notes/MongoDB|MongoDB]]

*Ссылка на исходник или контекст (если есть):* [Курс Яндекс практикум по NodeJS](https://practicum.yandex.ru/profile/backend-nodejs/)

Для работы в NodeJS требуется модуль `mongodb`

```ts
import { MongoClient } from 'mongodb';

/* Создаём экземпляр MongoClient, передав URL для подключения к MongoDB */
const client = new MongoClient('mongodb://localhost:27017');

/* Подключаемся. Обратите внимание на то, что метод асинхронный */
await client.connect();

/* Получаем доступ к нужной базе данных */
const db = client.db('myDatabase');

/* Теперь мы можем обращаться к любой коллекции из базы данных */
db.users
db.books
```

### Связанные идеи:

---

*Что стоит развить? Какие вопросы возникли?*
1) Особенности подключения
