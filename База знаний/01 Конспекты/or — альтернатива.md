---
tags:
  - парсерКомбинаторыJS
created: 2026-08-30
related:
  - "[[Реализация парсер комбинаторов в JS]]"
repeat: spaced every 54 hours
due_at: 2026-09-05T23:06:23.214+03:00
---

# or — альтернатива

`or` пробует парсеры по порядку и возвращает результат первого успешного:

```ts
export function or<T extends Parser<any>[]>(...parsers: T): Parser<
    T extends (infer R extends Parser<any>)[] ? ReturnType<R>[0] : never
> {
    return (iter) => {
        let cause;
        for (const parser of parsers) {
            try {
                return parser(iter.clone());
            } catch (err) {
                cause = err;
            }
        }
        throw new Error("Expected one of the alternatives", { cause });
    };
}
```

**Пример использования:**

```ts
const parser = or(tag("true"), tag("false"), tag("null"));
const [result] = parser(new ParserIterator("true"));
console.log(result); // "true"
```

# Ссылки
- 