---
tags:
  - Итераторы
created: 2026-08-24
related:
  - "[[Итераторы]]"
repeat: spaced every 162 hours
due_at: 2026-09-13T13:54:33.381+03:00
---

# Iterator в JS

В современном JavaScript существует **глобальный объект `Iterator`** — это встроенный класс/тип, представляющий итераторы. Объекты, которые являются итераторами, имеют прототип `Iterator.prototype`, на котором доступны методы-адаптеры (`map`, `filter` и другие).

**Важно:** объект, который просто имеет метод `next()` — это ещё не полноценный итератор. Это просто объект с методом `next()`. Чтобы он стал настоящим итератором с прототипом `Iterator.prototype` и всеми встроенными методами, его нужно создать через `Iterator.from`.

`Iterator.from` — это фабрика, которая создаёт **настоящий объект типа Iterator**. Без него объект с `next()` — просто объект, даже если он ведёт себя как итератор. **Однако для работы с `for...of` и spread (`...`) достаточно, чтобы объект был итерируемым (имел `[Symbol.iterator]`)**. Настоящий тип `Iterator` для этого не обязателен.

```js
// Просто объект с next() — НЕ настоящий итератор
function createSimpleRange(start, end) {
    let current = start;
    return {
        next() {
            if (current <= end) {
                return {value: current++, done: false};
            }
            return {done: true};
        }
    };
}

const simple = createSimpleRange(1, 3);
console.log(simple.next().value); // 1 — работает
console.log(simple.map); // undefined — нет методов!

// Настоящий итератор через Iterator.from
const realIterator = Iterator.from(createSimpleRange(1, 3));
console.log(realIterator.next().value); // 1
console.log(realIterator.map); // [Function: map] — методы доступны!
console.log(realIterator instanceof Iterator); // true (или есть Symbol.toStringTag)
```

Проверить, является ли объект итератором, можно через `Symbol.toStringTag`:

```js
const range = createSimpleRange(1, 3);
const realIterator = Iterator.from(range);

console.log(realIterator[Symbol.toStringTag]); // 'Iterator'
console.log(range[Symbol.toStringTag]); // undefined
```

`Iterator.from` создаёт итератор из:

1. **Итерируемого объекта** (Iterable) — вызывает `[Symbol.iterator]()`.
2. **Итератора** — возвращает его же (если он уже настоящий итератор).
3. **Любого объекта с методом `next()`** — оборачивает его, добавляя прототип `Iterator.prototype` и все встроенные методы.

```js
// Из итерируемого объекта
const fromArray = Iterator.from([1, 2, 3]);
console.log(fromArray[Symbol.toStringTag]); // 'Iterator'

// Из итератора (если уже настоящий — возвращает его же)
const fromIterator = Iterator.from(realIterator);
console.log(fromIterator === realIterator); // true (или обёртка)

// Из объекта с next()
const custom = {
    next() {
        return {value: 42, done: false};
    }
};
const fromCustom = Iterator.from(custom);
console.log(fromCustom[Symbol.toStringTag]); // 'Iterator'
console.log(fromCustom.next().value); // 42
console.log(fromCustom.map(x => x * 2).next().value); // 84 — методы работают!
```

# Ссылки

- 