---
tags:
  - Итераторы
created: 2026-01-24
related:
  - "[[Итераторы]]"
repeat: spaced every 182 hours
due_at: 2026-08-22T06:00:00.000+03:00
---

# Композиция итераторов и встроенный API Iterator Helpers

Итераторы можно не только создавать, но и **комбинировать**, строя цепочки преобразований без создания промежуточных массивов. Это позволяет обрабатывать данные лениво: каждое значение проходит через всю цепочку преобразований только тогда, когда оно запрашивается.

### Iterator Helpers (Stage 3)

Современный JavaScript предоставляет встроенные методы для работы с итераторами: `map`, `filter`, `take`, `drop`, `reduce` и другие. Все эти методы ленивые — они возвращают новый итератор, который вычисляет значения по требованию.

```js
// Создаём итератор, генерирующий бесконечную последовательность чисел
function createNumbersIterator() {
    let i = 0;
    return Iterator.from({ // Используем фабрику Iterator.from, чтобы появился встроенный API
        next() {
            return {value: i++, done: false};
        }
    });
}

const numbers = createNumbersIterator();

// Ленивая цепочка: умножаем на 2, оставляем только > 5, берём первые 3
const result = numbers
    .map(x => x * 2)
    .filter(x => x > 5)
    .take(3);

// Значения вычисляются по требованию
for (const value of result) {
    console.log(value); // 6, 8, 10
}
```

### Пример: итератор zip


Напишем свой адаптер `zip`, который объединяет два итератора в один, возвращая пары значений:

```js
function createZipIterator(iterable1, iterable2) {
    const iter1 = iterable1[Symbol.iterator]();
    const iter2 = iterable2[Symbol.iterator]();

    return Iterator.from({
        next() {
            const next1 = iter1.next();
            const next2 = iter2.next();

            if (next1.done || next2.done) {
                return {done: true};
            }

            return {value: [next1.value, next2.value], done: false};
        }
    });
}

// Использование с массивами
const names = ['Alice', 'Bob', 'Charlie'];
const ages = [25, 30, 35];

// for...of
for (const [name, age] of createZipIterator(names, ages)) {
    console.log(`${name} is ${age} years old`);
}

// Spread
const pairs = [...createZipIterator(names, ages)];
console.log(pairs); // [['Alice', 25], ['Bob', 30], ['Charlie', 35]]
```

После того как мы создали свой адаптер, его можно комбинировать со встроенными методами:

```js
function createZipIterator(iterable1, iterable2) {
    const iter1 = iterable1[Symbol.iterator]();
    const iter2 = iterable2[Symbol.iterator]();

    return Iterator.from({
        next() {
            const next1 = iter1.next();
            const next2 = iter2.next();

            if (next1.done || next2.done) {
                return {done: true};
            }

            return {value: [next1.value, next2.value], done: false};
        }
    });
}

const names = ['Alice', 'Bob', 'Charlie', 'David'];
const ages = [25, 30, 35, 40];

// Фильтруем пары, где возраст больше 30, и берём только имена
const result = createZipIterator(names, ages)
    .filter(([name, age]) => age > 30)
    .map(([name, age]) => name);

for (const name of result) {
    console.log(name); // 'Charlie', 'David'
}
```

### Преимущества композиции

1. **Ленивость** — значения вычисляются только тогда, когда они нужны.
2. **Экономия памяти** — нет промежуточных коллекций.
3. **Читаемость** — цепочки методов читаются как последовательность преобразований.
4. **Универсальность** — работают с любыми итерируемыми объектами.

**Итог:** итераторы позволяют строить API, которые не диктуют потребителю, как хранить и обрабатывать данные. В сочетании с ленивостью это даёт мощный инструмент для работы с данными, который экономит память и позволяет обрабатывать бесконечные последовательности.

## Ссылки

- 