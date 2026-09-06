---
tags:
  - парсерКомбинаторыJS
created: 2026-08-30
related:
  - "[[Реализация парсер комбинаторов в JS]]"
repeat: spaced every 81 hours
due_at: 2026-09-10T04:58:39.800+03:00
---

# map — преобразование результата

`map` преобразует результат парсера через функцию:

```ts
export function map<I, O>(
    parser: Parser<I>,
    mapFn: (...args: ParserResult<I>) => ParserResult<O>
): Parser<O> {
    return (iter) => mapFn(...parser(iter));
}
```

# Ссылки
- 