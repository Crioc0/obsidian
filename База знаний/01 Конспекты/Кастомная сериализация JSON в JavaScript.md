---
tags:
  - JSON
created: 2026-01-24
related:
  - "[[JSON]]"
repeat: spaced every 1406 hours
due_at: 2026-09-13T06:00:00.000+03:00
---

# Кастомная сериализация JSON в JavaScript

Классы могут определять свой метод `toJSON()`, который вызывается при `JSON.stringify()`. Это полезно для скрытия чувствительных данных или преобразования сложных объектов.

```js
class User {
    constructor(name, password, createdAt) {
        this.name = name;
        this.password = password;  // не хотим отправлять пароль
        this.createdAt = createdAt;  // объект Date, нужно преобразовать
    }

    toJSON() {
        // Возвращаем только то, что хотим сериализовать
        return {
            name: this.name,
            createdAt: this.createdAt.toISOString()  // Date → строка
        };
    }
}

const user = new User("Alice", "secret123", new Date());
console.log(JSON.stringify(user));
// {"name":"Alice","createdAt":"2024-01-15T10:30:00.000Z"}
// Пароль не попал в вывод — отлично!
```

**Обратный процесс: кастомная десериализация через reviver-функцию:**

```js
const jsonString = '{"name":"Alice","birthday":"2024-01-15"}';

// Вторым аргументом можно передать reviver-функцию
const data = JSON.parse(jsonString, (key, value) => {
    if (key === "birthday") return new Date(value);  // строка → Date
    return value;
});

console.log(data.birthday.getMonth());  // 0 (январь) — это уже настоящая дата
```

**Опасность ручного парсинга через eval:**

```js
// ОПАСНО! Никогда так не делайте:
const data = eval("(" + jsonString + ")");  // уязвимо для XSS-атак

// БЕЗОПАСНО:
const data = JSON.parse(jsonString);
```

## Ссылки

- 