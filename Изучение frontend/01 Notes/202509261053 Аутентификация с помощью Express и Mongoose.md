---
created: 2025-09-26 10:53
tags:
  - backend
  - authentication
  - express
  - mongoose
repeat: spaced every day
due_at: 2025-10-24T06:00:00.000+03:00
hidden: false
---
# 202509261053 Аутентификация с помощью Express и Mongoose

*Ссылка на StructureNote:* [[MongoDB]] [[02 Structure notes/Mongoose|Mongoose]]
*Ссылка на исходник или контекст (если есть):* [ЯПрактикум](https://practicum.yandex.ru/learn/backend-nodejs/courses/16b47298-e20d-4fde-9619-1ab305039a00/sprints/564238/topics/a4928f0d-5f69-4053-bea3-fa90d3a2a89f/lessons/24dcb381-2616-47de-ba41-18aacaa0df57/) 

Для того, чтобы авторизовать пользователя, нужно получить данные из req и сравнить из с данными из БД. Чтобы проверить захешированный пароль, нужно взять  пароль, полученный от пользователя, захешировать его и сравнить его с паролем, хранящимся в БД.

Для этого можно использовать метод `bcrypt.compare`

Метод `bcrypt.compare` работает асинхронно, поэтому результат нужно вернуть и обработать в следующем `then`. Если хеши совпали, в следующий `then` придёт `true`, иначе — `false`

```ts
// controllers/users.ts

export const login = (req: Request, res: Response) => {
  const { email, password } = req.body;

  return User.findOne({ email })
    .then((user) => {
      if (!user) {
        return Promise.reject(new Error('Неправильные почта или пароль'));
      }

      return bcrypt.compare(password, user.password);
    })
    .then((matched) => {
      if (!matched) {
        // хеши не совпали — отклоняем промис
        return Promise.reject(new Error('Неправильные почта или пароль'));
      }

      // аутентификация успешна
      res.send({ message: 'Всё верно!' });
    })
    .catch((err) => {
      res
        .status(401)
        .send({ message: err.message });
    });
};
```

### Связанные идеи:

* [[202509260844 Хэширование паролей в NodeJS]]
---

*Что стоит развить? Какие вопросы возникли?*
