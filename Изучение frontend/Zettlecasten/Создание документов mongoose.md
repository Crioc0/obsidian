2025 09 1818 35
Tags: #mongoose 
###### Links: 
1) 
# Заметка
За создание отвечает метод модели create. Он принимает на вод объект с данными, которые нужно записать в базу.
```ts
// routes/users.js

/*
    всякий код для создания роутеров и т. п.
*/

// импортируем модель
const User = require('../models/user');

router.post('/', (req, res) => {
  const { name, about } = req.body; // получим из объекта запроса имя и описание пользователя

  User.create({ name, about }); // создадим документ на основе пришедших данных
});
```
Метод `create` может быть промисом — ему можно добавить обработчики `then` и `catch`. Так обычно и делают, чтобы вернуть клиенту данные или ошибку:
```ts
// routes/users.js

/*
    всякий код для создания роутеров и т. п.
*/

const User = require('../models/user');

router.post('/', (req, res) => {
  const { name, about } = req.body;

  User.create({ name, about })
    // вернём записанные в базу данные
    .then(user => res.send({ data: user }))
    // данные не записались, вернём ошибку
    .catch(err => res.status(500).send({ message: 'Произошла ошибка' }));
});
```