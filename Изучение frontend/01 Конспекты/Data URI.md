---
tags:
  - база
created: 2026-01-24
related:
  - "[[View-подход чтения данных]]"
repeat: spaced every 96 hours
due_at: 2026-05-18T11:38:51.407+03:00
---

# Data URI

Data URI — это способ включить файл (изображение, шрифт, любые бинарные данные) прямо в текстовый документ (HTML, CSS, JSON).

**Формат Data URI:**

```js
data:[<MIME-тип>][;charset=<кодировка>][;base64],<данные>
```

**Примеры использования:**

1. **Встраивание маленькой иконки в CSS (чтобы не было лишнего HTTP-запроса):**

```css
   .icon-search {
   background-image: url("data:image/svg+xml,%3Csvg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"%3E%3Cpath fill="%23333" d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/%3E%3C/svg%3E");
   }    
```

2. **Генерация ссылки для скачивания файла на лету:**
 ```js
  function downloadJSON(data, filename) {
  const jsonString = JSON.stringify(data, null, 2);
  const blob = new Blob([jsonString], { type: "application/json" });
  const url = URL.createObjectURL(blob);  // создаём временный URL
  
   const link = document.createElement("a");
  link.href = url;
  link.download = filename;
   link.click();
  
  URL.revokeObjectURL(url); // освобождаем память
  }
   
  ```

3. **Создание изображения из пользовательского ввода:**

 ```js
   function generateQRCode(text) {
   // Где-то получаем буфер с QR-кодом (например, от библиотеки)
  const qrBuffer = qrLibrary.generate(text);
   
   // Превращаем в Data URL
   const blob = new Blob([qrBuffer], { type: "image/png" });
   const dataUrl = URL.createObjectURL(blob);
 
   document.getElementById("qr-image").src = dataUrl;
   }
 ```

4. **Data URI в HTML:**

 ```html
   <img src="data:image/svg+xml,%3Csvg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"%3E%3Ccircle cx="50" cy="50" r="40" fill="red"/%3E%3C/svg%3E">
 ```

5. **Генерация Data URI для текста:**

  ```js
  function createDataURI(text, mime = "text/plain") {
  return `data:${mime};charset=utf-8,${encodeURIComponent(text)}`;
  }
   
   const link = document.createElement("a");
   link.href = createDataURI("Hello, world!", "text/plain");
   link.download = "hello.txt";
   link.click(); // скачивается текстовый файл
  
  ```

**Плюсы Data URI:**

- **Снижение числа HTTP-запросов** — всё находится в одном файле.
- **Удобство распространения** — один HTML-файл содержит всё: стили, иконки и скрипты.
- **Нет проблем с CORS** — данные лежат прямо в документе.

**Минусы Data URI:**

- **Данные занимают больше места** (base64 увеличивает объём на 33%).
- **Кэширование не работает** — каждый раз, когда меняется родительский файл, меняется и встроенное изображение.
- **Тяжело поддерживать** — смешивание контента и представления.

## Ссылки

- 