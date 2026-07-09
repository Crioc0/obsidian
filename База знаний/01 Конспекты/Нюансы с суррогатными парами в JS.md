---
tags:
  - база
created: 2026-01-24
related:
  - "[[Строки в JS]]"
repeat: spaced every 48 hours
due_at: 2026-07-11T18:58:08.987+03:00
---

# Нюансы с суррогатными парами в JS

|Операция|Поведение|Правильный способ|
|---|---|---|
|`str.length`|Считает 16-битные единицы|`[...str].length`|
|`str[0]`|Возвращает суррогат|`[...str][0]`|
|`charAt()`|Возвращает суррогат|`[...str][0]`|
|`charCodeAt()`|Возвращает 16-битный код|`codePointAt()`|
|`fromCharCode()`|Не работает с > U+FFFF|`fromCodePoint()`|
|`split('')`|Разбивает по суррогатам|`[...str]`|
|Регулярные выражения|`.` не захватывает суррогатную пару полностью|Флаг `u` (unicode)|

```js
const str = "😀";

// До ES6 (неправильно)
console.log(str.charCodeAt(0)); // 55357 (D83D)
console.log(str.charCodeAt(1)); // 56832 (DE00)

// С ES6 (правильно)
console.log(str.codePointAt(0)); // 128512 (1F600)
console.log(String.fromCodePoint(128512)); // "😀"

// Регулярные выражения с флагом u
console.log(/^.$/.test(str)); // false
console.log(/^.$/u.test(str)); // true
```


## Ссылки

- 