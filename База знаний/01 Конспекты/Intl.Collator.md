---
tags:
  - база
created: 2026-01-24
related:
  - "[[Строки в JS]]"
repeat: spaced every 96 hours

due_at: 2026-07-20T16:41:19.563+03:00

---

# Intl.Collator
**`Intl.Collator`** — объект для **локалезависимого** сравнения строк. Учитывает правила языка.

```js
// Шведская локаль
const swedish = new Intl.Collator('sv');
console.log(swedish.compare('ö', 'z')); // 1 (ö > z в шведском)

// Немецкая локаль
const german = new Intl.Collator('de');
console.log(german.compare('ö', 'z')); // -1 (ö < z в немецком)

// Без учёта регистра и диакритики
const caseInsensitive = new Intl.Collator('en', {sensitivity: 'base'});
console.log(caseInsensitive.compare('A', 'a')); // 0 (равны)
console.log(caseInsensitive.compare('é', 'e')); // 0 (равны)
```

**Параметры:**

- `locale` — язык/регион (`'en'`, `'ru'`, `'sv'`, `'zh-Hans-CN'` и т.д.).
- `sensitivity` — чувствительность (`'base'`, `'accent'`, `'case'`, `'variant'`).
- `caseFirst` — порядок регистра (`'upper'`, `'lower'`).
- `numeric` — числовое сравнение (`'1' < '10'` как числа).

### Сравнение с localCompare

`localeCompare` удобен для простых случаев, но при многократных сравнениях (например, в сортировке больших массивов) рекомендуется использовать `Intl.Collator`, так как он создаётся один раз и переиспользуется, что может дать прирост производительности:

```js
// При каждом сравнении может создаваться внутренний collator
['ä', 'z', 'ö'].sort((a, b) => a.localeCompare(b, 'sv'));

// Collator создаётся один раз и переиспользуется
const collator = new Intl.Collator('sv');
['ä', 'z', 'ö'].sort((a, b) => collator.compare(a, b));
```

**Когда использовать `localeCompare`:**

- Единичные сравнения.
- Простой код без критичных требований к производительности.

**Когда использовать `Intl.Collator`:**

- Сортировка больших массивов (сотни и тысячи элементов).
- Многократные сравнения в циклах.
- Когда нужен тонкий контроль над параметрами сравнения.

### Объединение нормализации и локализованного сравнения


Для корректного сравнения строк с диакритикой часто комбинируют нормализацию и `Intl.Collator`:

```js
const collator = new Intl.Collator('en', {sensitivity: 'base'});
const str1 = "café".normalize('NFC');
const str2 = "cafe\u0301".normalize('NFC'); // "café" (но с комбинируемым символом)
console.log(collator.compare(str1, str2)); // 0 — игнорирует диакритику
```
## Ссылки

- 