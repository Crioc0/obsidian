---
tags:
  - база
created: 2026-01-24
related:
  - "[[Строки в JS]]"
repeat: spaced every 144 hours

due_at: 2026-07-27T14:29:46.113+03:00

---

# Intl.Segmenter

**`Intl.Segmenter`** — объект для разбиения текста на графемы, слова, предложения с учётом локали.

```js
// Разбиение на графемы (визуальные символы)
const segmenter = new Intl.Segmenter('en', {granularity: 'grapheme'});
const segments = segmenter.segment('Hello 😀');
for (const segment of segments) {
    console.log(segment.segment); // H, e, l, l, o, (space), 😀
}

// Разбиение на слова
const wordSegmenter = new Intl.Segmenter('en', {granularity: 'word'});
const words = wordSegmenter.segment('Hello, world!');
for (const w of words) {
    console.log(w.segment); // Hello, , world, !
}
```

**Поддерживаемые уровни:**

- `'grapheme'` — видимые символы (учитывает комбинируемые символы и эмодзи).
- `'word'` — слова (учитывает границы слов в разных языках).
- `'sentence'` — предложения.

## Ссылки

- 