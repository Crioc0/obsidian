---
tags:
  - база
created: 2026-01-24
related:
  - "[[Язык регулярных выражений]]"
repeat: spaced every 96 hours
due_at: 2026-08-19T19:34:36.955+03:00
---

# Ретроспективные проверки (lookbehind)
**Ретроспективная проверка** проверяет, что ПЕРЕД текущей позицией находится определённый шаблон.

|Тип|Синтаксис|Значение|
|---|---|---|
|Позитивный lookbehind|`(?<=...)`|Проверяет, что шаблон был раньше|
|Негативный lookbehind|`(?<!...)`|Проверяет, что шаблон НЕ был раньше|

```js
// Позитивный lookbehind: найти "cat" только после "dog"
const regex = /(?<=dog )cat/;
console.log(regex.test("dog cat"));  // true
console.log(regex.test("bird cat")); // false

// Негативный lookbehind: найти "cat" не после "dog"
const regex2 = /(?<!dog )cat/;
console.log(regex2.test("bird cat")); // true
console.log(regex2.test("dog cat"));  // false
```

**Важно:** lookbehind в JavaScript поддерживается только в современных браузерах (ES2018+).
## Ссылки

- 