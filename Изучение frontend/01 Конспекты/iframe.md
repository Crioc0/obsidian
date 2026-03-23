---
tags:
  - HTML
created: 2026-01-24
related:
  - "[[HTML]]"
repeat: spaced every 354 hours
due_at: 2026-04-02T06:00:00.000+03:00
---
# iframe


## Что это? (Определение)
HTML iframe (inline frame) нужен для встраивания одной HTML-страницы в другую.

## Зачем это нужно? (Применение)
Для показа изолированного контента и скриптов другой страницы в родительскую страницу.
Чаще всего используется для вставки видео с видео-хостингов, интеграций карт. Также можно использовать iframe для интеграции микрофронтендов, отображая 

## Как это работает? (Принцип)
iframe встраивается в страницу, при этом внутренняя логика и стили инкапсулированы и не зависимы от родительской страницы.


## Пример 
```html
<iframe src="https://example.com/another-page.html"></iframe>
```

```html
<iframe
  id="inlineFrameExample"
  title="Inline Frame Example"
  width="300"
  height="200"
  src="https://www.openstreetmap.org/export/embed.html?bbox=-0.004017949104309083%2C51.47612752641776%2C0.00030577182769775396%2C51.478569861898606&amp;layer=mapnik">
</iframe>
```
