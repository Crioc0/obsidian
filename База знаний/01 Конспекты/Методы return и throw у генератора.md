---
tags:
  - автоматы
created: 2026-08-30
related:
  - "[[Итераторы]]"
repeat: spaced every 54 hours
due_at: 2026-09-05T23:06:58.997+03:00
---

# Методы return и throw у генератора
**`return(value)`** — завершает генератор с указанным значением.

**`throw(error)`** — генерирует исключение в месте приостановки генератора.

```js
function* generator() {
    try {
        yield 1;
        yield 2;
    } catch (e) {
        console.log('Поймано:', e.message);
        yield 3;
    }
}

const gen = generator();
console.log(gen.next().value); // 1
console.log(gen.throw(new Error('ошибка!'))); // 'Поймано: ошибка!', { value: 3, done: false }
```

## Пример: throw в генераторе

[](https://gist.github.com/kobezzza/9aeed48ade43c245b3cce64a5603f179#%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-throw-%D0%B2-%D0%B3%D0%B5%D0%BD%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%B5)

`throw()` позволяет обрабатывать ошибки внутри генератора:

```js
function* processData() {
    let data;
    try {
        data = yield 'get data';
        data = yield 'process data';
    } catch (e) {
        console.log('Ошибка обработки:', e.message);
        data = 'default';
    }
    return data;
}

const gen = processData();
gen.next(); // { value: 'get data', done: false }
gen.next('user data'); // { value: 'process data', done: false }
gen.throw(new Error('network error')); // 'Ошибка обработки: network error', { value: 'default', done: true }
```
# Ссылки
- 