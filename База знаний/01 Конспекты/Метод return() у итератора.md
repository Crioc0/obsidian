---
tags:
  - Итераторы
created: 2026-08-24
related:
  - "[[Итераторы]]"
repeat: spaced every 24 hours
due_at: 2026-08-25T11:49:50.682+03:00
---

# Метод return() у итератора

Итераторы могут реализовывать метод `return()` — вызов этого метода имеет семантику досрочного прерывания итератор. Это позволяет освободить ресурсы (закрыть файлы, отменить запросы).

`return()` вызывается автоматически при досрочном завершении обхода в `for...of` через `break`, `return` или `throw`.

```js
// Пользовательский итератор с return
function createResourceIterator() {
    let isClosed = false;
    let count = 0;
    return {
        next() {
            if (isClosed) return {done: true};
            if (count < 5) {
                return {value: count++, done: false};
            }
            return {done: true};
        },
        return() {
            console.log('Ресурсы освобождены');
            isClosed = true;
            return {done: true};
        },
        [Symbol.iterator]() {
            return this;
        }
    };
}

// Автоматический вызов return при break в for...of
for (const value of createResourceIterator()) {
    console.log(value); // 0, 1, 2
    if (value === 2) {
        break; // 'Ресурсы освобождены' — return вызван автоматически
    }
}
```

**Важно:** после `break` и автоматического вызова `return()` итератор может считаться завершённым, но это **не является строгим контрактом**. Последующие вызовы `next()` **не обязаны** возвращать `{ done: true }` — это зависит от конкретной реализации итератора.

Однако такое поведение (возврат `{ done: true }`) характерно для:

- **Генераторов** — после `return()` они останавливаются.
- **Итераторов, созданных через встроенные адаптеры (filter, map и другие)** — они также завершаются.
- **Пользовательских итераторов**, где разработчик явно реализовал такое поведение.

```js
// Генератор — после return next() возвращает done: true
function* generate() {
    yield 1;
    yield 2;
    yield 3;
}

const iter = generate();

for (let value of iter) {
    console.log(value); // 1
    break;
}

// Цикл не выполнится
for (let value of iter) {
    console.log(value);
}
```

**Особенности `return()` у разных итераторов:**

|Тип итератора|Наличие `return()`|Поведение после `return()`|
|---|---|---|
|Итератор массива|❌ Нет|—|
|Итератор Set|❌ Нет|—|
|Итератор Map|❌ Нет|—|
|Генератор|✅ Есть|Останавливает итератор|
|`Iterator.from()`|✅ Есть|**Ничего не делает по умолчанию**|
|Адаптеры (`map`, `filter`, `take` и др.)|✅ Есть|Останавливает итератор|
|Пользовательский итератор|Опционально|Зависит от реализации|

```js
const iter1 = Iterator.from({
    next: () => ({value: Math.random(), done: false}),
});

console.log(iter1.return);       // [Function: return] — есть
console.log(iter1.next().value); // 0.06991565441438674

console.log(iter1.return());     // { value: undefined, done: true }
console.log(iter1.next().value); // 0.21482656954031065 — итератор НЕ остановился!

const iter2 = iter1.take(2);

console.log(iter2.return());     // { value: undefined, done: true }
console.log(iter2.next());       // { value: undefined, done: true }

console.log(iter1.next());       // { value: 0.9314648124277558, done: false }
```

У встроенных итераторов (массивы, Set, Map) метода `return()` нет, поэтому `break` просто завершает обход без каких-либо дополнительных действий.

```js
// У итератора массива нет return
const arrIter = [1, 2, 3][Symbol.iterator]();
console.log(arrIter.return); // undefined

// break в for...of просто завершает обход
for (const value of arrIter) {
    console.log(value);
    break; // return не вызывается (его нет)
}

// Обход продолжиться
for (const value of arrIter) {
   console.log(value);
   break; // return не вызывается (его нет)
}
```

**Вывод:** не полагайтесь на то, что после `return()` итератор обязательно завершится. Это поведение характерно для генераторов, но не является обязательным для всех итераторов. У итераторов, созданных через `Iterator.from` и его адаптеров, метод `return()` присутствует, но по умолчанию ничего не делает (если его изначально не было). Важно понимать, что адаптеры (`map`, `filter`, `take`) при вызове `return()` останавливают только себя, но **не останавливают родительский итератор** — он продолжает существовать и может быть использован дальше.

# Ссылки

- 