---
tags:
  - база
created: 2026-01-24
related:
  - "[[Computer Science]]"
repeat: spaced every 561 hours
due_at: 2026-06-04T06:00:00.000+03:00
---

# View над данными

Подход, когда есть отдельно данные и отдельно представление (view) для этих данных популярен самых разных задач.

Главный плюс в этом подходе в том, что можно иметь много потребителей одних и тех же данных, но предоставлять им разный API доступа. При этом копировать данные для каждого потребителя не обязательно.

```js
class User {
  get has18() {
    return new Date().getFullYear() - this.#data.birthdate.getFullYear() >= 18;
  }
  get canProgramming() {
    return this.#data.skills.includes("programming");
  }
  get name() {
    return this.#data.name;
  }
  set name(name) {
    this.#data.name = name;
  }
  #data;
  constructor(data) {
    this.#data = data;
  }
}
class Users {
  #data;
  constructor(data) {
    this.#data = data;
  }
  at(index) {
    return new User(this.#data.at(index));
  }
}

const data = [
  {
    name: "Bob",
    birthdate: new Date(1990, 1, 1),
    skills: ["programming", "sing"],
  },
  { name: "Ben", birthdate: new Date(1989, 11, 10), skills: ["sing"] },
];
const users = new Users(data);
console.log(users.at(0).has18);

```

Благодаря этому подходу можно создать абстракцию над сырыми данными: часть данных скрыть, добавить новые акцессоры или методы. Так же избегается избыточное копирование - можно добавить копирование при записи, если это потребуется. Для разных потребителей мы можем делать разные представления Особенно это удобно для различных миграций

## Ссылки

- 