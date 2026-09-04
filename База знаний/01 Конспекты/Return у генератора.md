---
tags:
  - генераторы
created: 2026-08-30
related:
  - "[[Генераторы]]"
repeat: spaced every 54 hours
due_at: 2026-09-05T23:06:58.638+03:00
---

# Return у генератора
У генератора есть метод `return()`, который:

1. Завершает выполнение генератора.
2. Возвращает переданное значение.
3. Делает все последующие вызовы `next()` возвращающими `{ done: true }`.

```js
function* generate() {
    yield 1;
    yield 2;
    yield 3;
}

const gen = generate();
console.log(gen.next().value); // 1
console.log(gen.return('завершено')); // { value: 'завершено', done: true }
console.log(gen.next()); // { done: true }
```
# Ссылки
- 