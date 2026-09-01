---
tags:
  - парсерКомбинаторыJS
created: 2026-08-30
related:
  - "[[Реализация парсер комбинаторов в JS]]"
repeat: spaced every 48 hours
due_at: 2026-09-03T20:30:50.646+03:00
---

# seq — последовательность


`seq` применяет несколько парсеров последовательно, возвращая массив результатов:

```ts
export function seq<T extends Parser<any>[]>(...parsers: T): Parser<{
    [K in keyof T]: ReturnType<T[K]>[0];
}> {
    return (iter) => {
        const results = [];
        for (const parser of parsers) {
            try {
                const [result, nextIter] = parser(iter.clone());
                iter = nextIter;
                results.push(result);
            } catch (cause) {
                throw new Error("Expected sequence", { cause });
            }
        }
        return [results, iter] as any;
    };
}
```

**Пример использования:**

```ts
const parser = seq(tag("Hello"), tag(" "), tag("World"));
const [result] = parser(new ParserIterator("Hello World"));
console.log(result); // ["Hello", " ", "World"]
```

# Ссылки
- 