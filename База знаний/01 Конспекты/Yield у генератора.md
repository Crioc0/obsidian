---
tags:
  - генераторы
created: 2026-08-30
related:
  - "[[Генераторы]]"
repeat: spaced every 36 hours
due_at: 2026-09-03T08:31:41.619+03:00
---

# Yield у генератора
`yield` — ключевое слово, которое:

1. Возвращает значение из генератора.
2. Приостанавливает выполнение функции.
3. Сохраняет состояние (локальные переменные, позицию в коде).

```js
function* example() {
    console.log('Начало');
    yield 1;
    console.log('После первого yield');
    yield 2;
    console.log('После второго yield');
    return 3;
}

const gen = example();
gen.next(); // 'Начало', { value: 1, done: false }
gen.next(); // 'После первого yield', { value: 2, done: false }
gen.next(); // 'После второго yield', { value: 3, done: true }
```
# Ссылки
- 