---
tags:
  - база
created: 2026-01-24
related:
  - "[[Строки в JS]]"
repeat: spaced every 542 hours

due_at: 2026-08-31T06:00:00.000+03:00

---

# Метод localeCompare
Для локалезависимого сравнения строк в JavaScript существует метод `localeCompare()`. Он возвращает число, указывающее, какая строка идёт раньше в соответствии с правилами текущей (или указанной) локали.

```js
// Базовое сравнение
console.log("ö".localeCompare("z", "sv")); // 1 (ö > z в шведском)
console.log("ö".localeCompare("z", "de")); // -1 (ö < z в немецком)

// Без учёта регистра
console.log("A".localeCompare("a", "en", {sensitivity: 'base'})); // 0 (равны)

// Числовое сравнение
console.log("10".localeCompare("2", undefined, {numeric: true})); // 1 (10 > 2 как числа)
console.log("10".localeCompare("2")); // -1 (лексикографически "10" < "2")
```

**Параметры localeCompare:**

|Параметр|Значения|Описание|
|---|---|---|
|`locale`|`'en'`, `'ru'`, `'sv'`, `'de'` и т.д.|Язык/регион для сравнения|
|`sensitivity`|`'base'`, `'accent'`, `'case'`, `'variant'`|Чувствительность к регистру и диакритике|
|`caseFirst`|`'upper'`, `'lower'`, `'false'`|Приоритет регистра|
|`numeric`|`true`, `false`|Числовое сравнение (для версий, номеров)|
|`ignorePunctuation`|`true`, `false`|Игнорировать знаки препинания|

**Применение:**

- Сортировка списков имён, городов, стран с учётом локальных правил.
- Поиск и фильтрация с учётом акцентов (`sensitivity: 'base'`).
- Сравнение версий (`numeric: true`).
## Ссылки

- 