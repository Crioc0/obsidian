---
tags:
  - парсерКомбинаторыJS
created: 2026-08-30
related:
  - "[[Реализация парсер комбинаторов в JS]]"
repeat: spaced every 96 hours
due_at: 2026-09-08T09:34:56.740+03:00
---

# repeat — повторение

`repeat` повторяет парсер указанное число раз:

```ts
export interface RepeatOptions {
    min?: number;
    max?: number;
}

export function repeat<T>(parser: Parser<T>, { min = 1, max = Infinity }: RepeatOptions = {}): Parser<T[]> {
    return (iter) => {
        const results = [];
        let count = 0;

        while (count < max) {
            try {
                const [result, nextIter] = parser(iter.clone());
                iter = nextIter;
                results.push(result);
                count++;
            } catch {
                if (count >= min) break;
                throw new Error(`Expected at least ${min} matches, got ${count}`);
            }
        }

        return [results, iter];
    };
}
```

**Пример использования:**

```ts
const parser = repeat(tag(/\d/), { min: 1 });
const [result] = parser(new ParserIterator("123abc"));
console.log(result); // ["1", "2", "3"]
```

# Ссылки
- 