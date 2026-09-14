---
tags:
  - парсерКомбинаторыJS
created: 2026-08-30
related:
  - "[[Реализация парсер комбинаторов в JS]]"
repeat: spaced every 36 hours
due_at: 2026-09-16T08:22:00.663+03:00
---

# opt — опциональный парсер



`opt` — частный случай `repeat` с `min: 0, max: 1`:

```ts
export function opt<T>(parser: Parser<T>): Parser<T[]> {
    return repeat(parser, { min: 0, max: 1 });
}
```
# Ссылки
- 