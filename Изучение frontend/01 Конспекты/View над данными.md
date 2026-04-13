---
tags:
  - база
created: 2026-01-24
related:
  - "[[Computer Science]]"
repeat: spaced every 24 hours
due_at: 2026-02-27T14:05:30.956+03:00
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

```

Благодаря этому подходу можно создать абстракцию над сырыми данными: часть данных скрыть, добавить новые акцессоры или методы. 

## Ссылки

- 