---
tags:
  - база
created: 2026-01-24
related:
  - "[[Итераторы]]"
repeat: spaced every 48 hours
due_at: 2026-08-06T11:04:11.839+03:00
---

# Iterator и Iterable

**Итерируемый объект (Iterable)** — это объект, у которого есть метод `Symbol.iterator`, возвращающий итератор. Метод `Symbol.iterator` вызывается каждый раз, когда нужно начать обход заново (например, при входе в `for...of` или при вызове spread).

```js
// Проверка, является ли объект итерируемым
const isIterable = obj => typeof obj?.[Symbol.iterator] === 'function';

console.log(isIterable([]));      // true
console.log(isIterable('hello')); // true
console.log(isIterable(new Set())); // true
console.log(isIterable({}));       // false
```

**Как работает обход через Iterable:**

1. При входе в `for...of` вызывается `collection[Symbol.iterator]()`.
2. Метод возвращает свежий итератор.
3. `for...of` автоматически вызывает `next()` до `done: true`.
4. При повторном обходе создаётся новый итератор.

```js
// Каждый for...of создаёт новый итератор
const arr = [1, 2, 3];

for (const value of arr) {
    console.log(value); // 1, 2, 3
}

for (const value of arr) {
    console.log(value); // 1, 2, 3 — обход заново
}
```

### Пример создания итератора в коде

Чтобы объект стал итерируемым, нужно реализовать метод `[Symbol.iterator]`:

```js
class MyCollection {
    constructor(data) {
        this.data = data;
    }

    [Symbol.iterator]() {
        let index = 0;
        const data = this.data;

        return {
            next() {
                if (index < data.length) {
                    return {value: data[index++], done: false};
                }
                return {done: true};
            }
        };
    }
}

const collection = new MyCollection([10, 20, 30]);

// Теперь работает for...of
for (const item of collection) {
    console.log(item); // 10, 20, 30
}

// Теперь работает spread
const arr = [...collection]; // [10, 20, 30]

// Теперь работает деструктуризация
const [first, second] = collection;
console.log(first, second); // 10, 20
```

### Итератор тоже должен быть Iterable

**Важно:** итератор, возвращаемый методом `Symbol.iterator`, тоже должен быть итерируемым (иметь свой `Symbol.iterator`, возвращающий самого себя). Это позволяет использовать итераторы в `for...of` и других конструкциях, хотя на практике `for...of` чаще работает с коллекциями напрямую.

```js
class Range {
    constructor(start, end) {
        this.start = start;
        this.end = end;
    }

    [Symbol.iterator]() {
        let current = this.start;
        const end = this.end;

        const iterator = {
            next() {
                if (current <= end) {
                    return {value: current++, done: false};
                }
                return {done: true};
            },

            [Symbol.iterator]() {
                return this; // итератор сам себя возвращает
            }
        };
        return iterator;
    }
}

const range = new Range(1, 3);
for (const value of range[Symbol.iterator]()) {
    console.log(value); // 1, 2, 3
}
```

### Общая схема работы

```js
Коллекция → [Symbol.iterator]() → Итератор → { next() → { value, done } }
```

1. У коллекции есть метод `Symbol.iterator`.
2. При вызове он возвращает объект-итератор.
3. У итератора есть метод `next()`.
4. `next()` возвращает объект с полями `value` и `done`.
5. Итератор тоже должен быть итерируемым (`[Symbol.iterator]` → `this`).

### Явная работа с итератором для возобновляемого обхода

Иногда нужно управлять итератором вручную, чтобы приостанавливать и возобновлять обход:

```js
const iterator = [1, 2, 3, 4, 5][Symbol.iterator]();

// Обрабатываем по одному элементу
const first = iterator.next().value;  // 1
const second = iterator.next().value; // 2
// ... делаем что-то между
const third = iterator.next().value;  // 3
```

## Ссылки

- 