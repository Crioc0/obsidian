---
tags:
  - Итераторы
created: 2026-08-30
related:
  - "[[Итераторы]]"
repeat: spaced every 54 hours
due_at: 2026-09-05T23:06:15.675+03:00
---

# Передача данных в next
В `next()` можно передать значение, которое станет результатом предыдущего `yield`:

```js
function* interactive() {
    const a = yield 'Введите a';
    const b = yield 'Введите b';
    return a + b;
}

const gen = interactive();
console.log(gen.next()); // { value: 'Введите a', done: false }
console.log(gen.next(5)); // { value: 'Введите b', done: false }
console.log(gen.next(3)); // { value: 8, done: true }
```
# Ссылки
- 