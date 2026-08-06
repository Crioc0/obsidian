---
tags:
  - база
created: 2026-01-24
related:
  - "[[Итераторы]]"
repeat: spaced every 96 hours
due_at: 2026-08-10T17:46:07.178+03:00
---

# Итераторы как основа API

Итераторы — это не просто механизм обхода коллекций. Это мощный инструмент для проектирования API, который делает код универсальным и отделяет логику генерации данных от логики их потребления.

Рассмотрим типичную задачу: функция `split`, которая разбивает строку на части. Если мы реализуем её так, что она возвращает массив, мы навязываем вызывающему коду конкретную структуру данных:

```js
function split(str, delimiter) {
    const result = [];
    let current = '';
    for (let i = 0; i < str.length; i++) {
        const char = str[i];
        if (char === delimiter) {
            result.push(current);
            current = '';
        } else {
            current += char;
        }
    }
    result.push(current);
    return result;
}

// Вызывающий код вынужден работать с массивом
const parts = split('a,b,c', ',');
console.log(parts[0]); // 'a'
console.log(parts[1]); // 'b'
console.log(parts[2]); // 'c'
```

В чём проблема? Мы не знаем, как вызывающий код хочет обрабатывать части строки. Возможно, ему нужно сохранить их в Set, возможно, обработать по одной без сохранения всех сразу, возможно, записать в файл. Возвращая массив, мы заставляем его хранить все элементы в памяти, даже если это не нужно.

Если же мы переходим в плоскость итераторов, код становится универсальным. Создаём объект, который реализует `Symbol.iterator` и возвращает итератор с методом `next()`:

```js
function createSplitIterator(str, delimiter) {
    let index = 0;
    let current = '';

    const iterator = {
        next() {
            if (index >= str.length && current === '') {
                return {done: true};
            }

            while (index < str.length) {
                const char = str[index++];
                if (char === delimiter) {
                    const result = {value: current, done: false};
                    current = '';
                    return result;
                }
                current += char;
            }

            const result = {value: current, done: false};
            current = '';
            return result;
        },
        [Symbol.iterator]() {
            return this; // итератор сам себя возвращает
        }
    };

    return iterator;
}
```

Теперь вызывающий код может использовать `for...of`, spread и передавать объект напрямую в конструкторы Set и Map:

```js
// for...of
for (const part of createSplitIterator('a,b,c', ',')) {
    console.log(part); // 'a', 'b', 'c'
}

// Spread — собираем в массив
const parts = [...createSplitIterator('a,b,c', ',')];
console.log(parts); // ['a', 'b', 'c']

// Передаём в конструктор Set
const unique = new Set(createSplitIterator('a,b,c', ','));
console.log(unique); // Set {'a', 'b', 'c'}
```

**Ключевая идея:** итератор — это контракт между производителем данных и потребителем. Производитель не знает, как потребитель будет использовать данные. Потребитель сам решает, какую структуру данных использовать и когда остановиться. Это делает API гибким и универсальным.

## Ссылки

- 