---
tags:
  - база
created: 2026-01-24
related:
  - "[[Язык регулярных выражений]]"
repeat: spaced every 48 hours
due_at: 2026-07-22T10:32:34.241+03:00
---

# Замена с использованием групп, replace
Метод `replace` использует группы в строке замены через `$n`:

```js
const str = "John Doe";
const regex = /(\w+) (\w+)/;
console.log(str.replace(regex, "$2, $1")); // "Doe, John"
```

**Специальные последовательности в строке замены:**

|Символ|Значение|
|---|---|
|`$$`|Символ $|
|`$&`|Всё совпадение|
|`$``|Текст до совпадения|
|`$'`|Текст после совпадения|
|`$n`|Группа n (n = 1-9)|
|`$<name>`|Именованная группа|

```js
const str = "Hello World";
const regex = /(\w+) (\w+)/;
console.log(str.replace(regex, "$&"));   // "Hello World"
console.log(str.replace(regex, "$`"));   // "" (до совпадения)
console.log(str.replace(regex, "$'"));   // "" (после совпадения)
```
## Ссылки

- 