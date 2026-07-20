---
tags:
  - база
created: 2026-01-24
related:
  - "[[Язык регулярных выражений]]"
repeat: spaced every 48 hours
due_at: 2026-07-22T10:34:25.858+03:00
---

# Свойство lastIndex у регулярного выражения

Свойство `lastIndex` хранит позицию, с которой будет начат следующий поиск. Используется с флагами `g` и `y`.

```js
const regex = /cat/g;
console.log(regex.lastIndex); // 0
regex.test("cat cat cat");
console.log(regex.lastIndex); // 3
regex.test("cat cat cat");
console.log(regex.lastIndex); // 7
```

**Важно:** `lastIndex` сбрасывается при неудачном поиске.

## Ссылки

- 