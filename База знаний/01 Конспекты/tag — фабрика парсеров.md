---
tags:
  - парсерКомбинаторыJS
created: 2026-08-30
related:
  - "[[Реализация комбинаторов в JS]]"
repeat: spaced every 24 hours
due_at: 2026-08-30T06:00:00.000+03:00
---

# tag — фабрика парсеров


`tag` — базовый парсер, распознающий строку или регулярное выражение:

```ts
export function tag(pattern: Iterable<string | RegExp> | RegExp): Parser<string> {
    const patterns = pattern instanceof RegExp ? [pattern] : [...pattern];

    return (iter) => {
        let result = "";

        for (const test of Iterator.from(patterns).flatMap(flat).map(createTest)) {
            const char = iter.peek();
            if (char == null || !test(char)) {
                throw new Error(`Expected pattern "${[...patterns].join("")}"`);
            }
            result += char;
            iter.next();
        }

        return [result, iter];
    };
}
```

**Пример использования:**

```ts
const parser = tag("hello");
const [result, iter] = parser(new ParserIterator("hello world"));
console.log(result); // "hello"
```

# tag -
- 