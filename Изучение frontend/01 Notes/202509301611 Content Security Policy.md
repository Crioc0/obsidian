---
created: 2025-09-30 16:11
tags:
  - security
repeat: spaced every day
due_at: 2025-10-24T06:00:00.000+03:00
---
# 202509301611 Content Security Policy

*Ссылка на StructureNote:* [[Security]]
*Ссылка на исходник или контекст (если есть):* [ЯПрактикум](https://practicum.yandex.ru/learn/backend-nodejs/courses/16b47298-e20d-4fde-9619-1ab305039a00/sprints/564238/topics/511a777e-323b-4964-9150-d06eaeb48080/lessons/7fb4f5c7-cb70-4243-904c-c4ff8d37469a/)

Если хакер все равно внедряет скрипт в сайт, на помощь приходит инструкция Content Security Policy

Есть два варианта установить инструкцию.

1) В метатеге. Можно добавить в раздел `head` тег `meta` и описать ограничения там:

```ts
<meta http-equiv="Content-Security-Policy" content="ИНСТРУКЦИИ">
```

```ts
Content-Security-Policy: /* ИНСТРУКЦИИ */
```

Есть 5 видов инструкций:

- `default-src` — обязательная инструкция, задаёт источник всех видов ресурсов по умолчанию;
- `script-src` — источник скриптов;
- `img-src` — изображения;
- `media-src` — аудио- и видео-файлы;
- `style-src` — файлы стилей.
После имени инструкции указывают сами источники через пробел. Чтобы указать домен сайта как источник, устанавливают ключевое слово

```ts
"script-src 'self' *.site.com"; // скрипты можно загружать с самого сайта, либо с поддоменов site.com, например, с https://example.site.com
```

В конце каждой инструкции должна стоять точка с запятой

```ts
Content-Security-Policy: default-src 'self'; img-src *; media-src media1.com media2.com; script-src userscripts.example.com
```

### Связанные идеи:

* [[202509301511 XSS]]

---

*Что стоит развить? Какие вопросы возникли?*
