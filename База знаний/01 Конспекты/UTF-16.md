---
tags:
  - база
created: 2026-01-24
related:
  - "[[Юникод (Unicode)]]"
repeat: spaced every 350 hours

due_at: 2026-08-13T06:00:00.000+03:00

---

# UTF-16

**UTF-16 (Unicode Transformation Format — 16-bit)** — кодировка, в которой:

- Символы из BMP (U+0000..U+FFFF) кодируются **одним 16-битным значением**.
- Символы за пределами BMP (U+10000..U+10FFFF) кодируются **суррогатной парой** (два 16-битных значения).
![[Pasted image 20260707163753.png]]
**Характеристики:**

- Переменная длина: 2 или 4 байта.
- Используется в JavaScript, .NET, Java, Windows API.
- Конечный порядок байтов (endianness) важен — есть BOM (Byte Order Mark).
## Ссылки

- 