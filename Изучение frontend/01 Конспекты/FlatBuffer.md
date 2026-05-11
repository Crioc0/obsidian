---
tags:
  - база
created: 2026-01-24
related:
  - "[[View-подход чтения данных]]"
repeat: spaced every 48 hours
due_at: 2026-05-13T21:05:20.360+03:00
---

# FlatBuffer

FlatBuffers — это формат, который идёт ещё дальше: он не требует десериализации вообще. Данные хранятся в памяти в таком виде, что их можно читать напрямую.

**Как это работает:**

1. Вы описываете схему (похоже на Protobuf).
2. Генерируется код, который умеет "замораживать" объекты в специальный буфер.
3. Для чтения вы создаёте "вьюшку" поверх буфера и читаете поля по смещениям.

**Создание FlatBuffer:**

```js
let builder = new flatbuffers.Builder();

// Создаём строку
let name = builder.createString("Alice");

// Начинаем строить объект Person
Person.startPerson(builder);
Person.addName(builder, name);
Person.addAge(builder, 30);
let alice = Person.endPerson(builder);

builder.finish(alice);

// Теперь в builder.asUint8Array() лежат готовые данные
let buffer = builder.asUint8Array();
```

**Чтение FlatBuffer (без десериализации!):**

```js
// Получаем Person прямо из буфера
let person = Person.getRootAsPerson(buffer);

// Читаем поля — они извлекаются из буфера "на лету"
console.log(person.name());  // "Alice" — мгновенно, без создания объектов
console.log(person.age());   // 30
```

**Когда использовать FlatBuffers:**

- Игровые ресурсы (модели, текстуры, карты уровней) — чтобы загружать их мгновенно
- Большие массивы чисел (например, научные данные, координаты 3D-моделей)
- Системы с жёсткими ограничениями по времени (DSP, real-time)
- Мобильные приложения с ограниченным объёмом памяти

## Ссылки

- 