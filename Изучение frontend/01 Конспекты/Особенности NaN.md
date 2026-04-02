---
tags:
  - база
created: 2026-01-24
related:
  - "[[Тип number и стандарт IEEE 754]]"
repeat: spaced every 96 hours
due_at: 2026-04-06T15:39:26.200+03:00
---
# Особенности NaN

**NaN (Not a Number)** — специальное значение, обозначающее "не число". Возникает при математически некорректных операциях.

```js
console.log(0 / 0);           // NaN
console.log(Math.sqrt(-1));   // NaN
console.log(parseInt("abc")); // NaN
```

**Ключевые особенности NaN:**

- NaN не равно самому себе
- Любая операция с NaN даёт NaN
- Для проверки на NaN используется `Number.isNaN()`, а не глобальная `isNaN()`

```js
console.log(NaN === NaN);           // false — важный нюанс!
console.log(Number.isNaN(NaN));     // true
console.log(isNaN("abc"));          // true — глобальная isNaN сначала преобразует
console.log(Number.isNaN("abc"));   // false — Number.isNaN не преобразует
```
## Ссылки
