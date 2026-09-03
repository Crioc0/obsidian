---
tags:
  - regexp
created: 2026-01-24
related:
  - "[[Регулярные выражения]]"
repeat: spaced every 421 hours
due_at: 2026-09-21T06:00:00.000+03:00
---

# Регулярные выражения в JavaScript, класс RegExp

В JavaScript регулярные выражения представлены объектом `RegExp`:

```js
// Создание регулярного выражения
const regex1 = /pattern/;          // литерал
const regex2 = new RegExp("pattern"); // конструктор
const regex3 = /pattern/flags;     // с флагами
```

### Методы строк, принимающие регулярки


|Метод|Описание|
|---|---|
|`str.match(regex)`|Возвращает совпадения или null|
|`str.matchAll(regex)`|Возвращает итератор по всем совпадениям|
|`str.search(regex)`|Возвращает индекс первого совпадения|
|`str.replace(regex, replacement)`|Заменяет совпадения|
|`str.replaceAll(regex, replacement)`|Заменяет все совпадения|
|`str.split(regex)`|Разбивает строку по разделителю|
|`regex.test(str)`|Проверяет, есть ли совпадение|
|`regex.exec(str)`|Продвинутый поиск с группами|

```js
const str = "Hello 123 World 456";
const regex = /\d+/g;

console.log(str.match(regex));   // ["123", "456"]
console.log(str.search(regex));  // 6 (индекс первой цифры)
console.log(str.replace(regex, "X")); // "Hello X World X"
console.log(regex.test(str));    // true
```

## Ссылки

- 