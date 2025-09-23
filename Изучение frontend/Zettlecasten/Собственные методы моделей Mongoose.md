2025 09 2311 11
Tags: #mongoose 
###### Links: 
1) 
# Заметка
Методы модели реализуют базовые CRUD-операции и некоторые служебные, такие как работа с индексами. В Monoose можно использовать не только встроенные методы, но и описывать встроенные. Благодаря этому:

- Можно упаковать логику работы с документами внутрь модели. Везде, где импортирована модель, будут доступны и наши собственные методы.
- Однозначно связать действия в БД с указанной моделью.
- Сократить объём кода.
Чтобы добавить собственный метод,  его нужно записать в свойства `statics` нужной схемы.
```ts
// models/user.ts

import mongoose from 'mongoose';

interface IUser {
    email: string;
    password: string;
}

interface UserModel extends mongoose.Model<IUser> {
  findUserByCredentials: (email: string, password: string) => Promise<mongoose.Document<unknown, any, IUser>>
}

const userSchema = new mongoose.Schema<IUser, UserModel>({
  email: {
    type: String,
    required: true,
    unique: true
  },
  password: {
    type: String,
    required: true,
    minlength: 8
  }
});

// добавим метод findUserByCredentials схеме пользователя
// у него будет два параметра — почта и пароль
userSchema.static('findUserByCredentials', function findUserByCredentials(email: string, password: string) {

};

export default mongoose.model('user', userSchema);
```
Описываемая функция не должна быть стрелочной, так как иначе `this` было бы задано статически, так как стрелочные функции запоминают значение `this` при объявлении.
Примем реализации ф
