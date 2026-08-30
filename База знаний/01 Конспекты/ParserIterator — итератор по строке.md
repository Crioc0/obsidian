---
tags:
  - парсерКомбинаторыJS
created: 2026-08-30
related:
  - "[[Реализация комбинаторов в JS]]"
repeat: spaced every 24 hours
due_at: 2026-08-30T06:00:00.000+03:00
---

# ParserIterator — итератор по строке


```ts
export class ParserIterator {
    readonly input: string;
    #position = 0;

    constructor(input: string, position = 0) {
        this.input = input;
        this.changePosition(position);
    }

    [Symbol.iterator]() {
        return this;
    }

    peek() {
        return this.#getChar(this.position);
    }

    next() {
        const value = this.#getChar(this.position);
        if (value === undefined) {
            return { value, done: true };
        }
        this.#position += value.length;
        return { value, done: false };
    }

    changePosition(position: number) {
        this.#position = position;
    }

    clone() {
        return new ParserIterator(this.input, this.position);
    }

    #getChar(index: number): string | undefined {
        const str = this.input;
        const code = str.charCodeAt(index);

        // Поддержка суррогатных пар (эмодзи)
        if (code >= 0xD800 && code <= 0xDBFF && index + 1 < str.length) {
            const next = str.charCodeAt(index + 1);
            if (next >= 0xDC00 && next <= 0xDFFF) {
                return str.slice(index, index + 2);
            }
        }

        return str[index];
    }
}
```
# Ссылки
- 