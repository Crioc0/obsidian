---
tags:
  - генераторы
created: 2026-08-30
related:
  - "[[Генераторы]]"
repeat: spaced every 54 hours
due_at: 2026-09-05T23:06:45.524+03:00
---

# Оператор yield со звездочкой
`yield*` делегирует выполнение другому генератору или итерируемому объекту:

```js
function* generateNumbers() {
    yield* [1, 2, 3];
}

function* generateLetters() {
    yield* 'abc';
}

function* generateAll() {
    yield* generateNumbers();
    yield* generateLetters();
}

const gen = generateAll();
console.log([...gen]); // [1, 2, 3, 'a', 'b', 'c']
```
# Ссылки
- 