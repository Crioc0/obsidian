2025 09 1214 40
Tags: #nodejs #MongoDB 
###### Links: 
1) [[NodeJS]]
2) [[MongoDB]]
# Заметка
Документы добавляются и запрашиваются из коллекций, а коллекции лежат в базе данных. Поэтому прежде чем делать запрос, нужно подключиться к нужной базе. Для подключения к MongoDB применили пакет `mongodb`:
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