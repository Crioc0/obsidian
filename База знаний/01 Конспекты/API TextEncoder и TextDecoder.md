---
tags:
  - база
created: 2026-01-24
related:
  - "[[Строки в JS]]"
repeat: spaced every 184 hours

due_at: 2026-07-29T06:00:00.000+03:00

---

# API TextEncoder и TextDecoder

Современные среды предоставляют API для преобразования строк в байты и обратно:

**TextEncoder** — преобразует строку в `Uint8Array` в кодировке UTF-8.

```js
const encoder = new TextEncoder();
const bytes = encoder.encode("Привет, мир!");
// Uint8Array [208, 159, 208, 190, ...]
```

**TextDecoder** — преобразует байты обратно в строку.

```js
const decoder = new TextDecoder('utf-8');
const str = decoder.decode(bytes);
// "Привет, мир!"
```

Поддерживаются и другие кодировки: `'utf-8'`, `'windows-1251'`, `'iso-8859-1'` и др.

## Ссылки

- 