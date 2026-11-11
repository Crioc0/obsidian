### Материалы

- [x] [Using promises — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
  - Промисы, `then/catch/finally`, chaining, error handling
- [x] [Promise — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
  - Состояния промиса, конструктор, `then`, `catch`, `finally`
- [x] [await — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)
  - Как `await` ждёт промис, top-level await, обработка rejected promises
- [x] [Promise — Glossary — MDN](https://developer.mozilla.org/en-US/docs/Glossary/Promise)
  - Краткое определение промиса
- [x] [Using the Fetch API — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
  - `fetch`, `Response`, `response.ok`, JSON, ошибки, отмена
- [x] [AbortController — MDN](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)
  - Создание контроллера и вызов `abort()`
- [x] [AbortSignal — MDN](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal)
  - Как `signal` связывает отмену с `fetch`
- [ ] [Working with JSON — MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON)
  - Практический пример `fetch` + `response.json()`

### Порядок чтения

1. [ ] [Using promises — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises) — до раздела **Error handling**
2. [ ] [await — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) — особенно поведение при rejected promise
3. [ ] [Using the Fetch API — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) — `response.ok`, `response.status`, `response.json()`
4. [ ] [AbortController — MDN](https://developer.mozilla.org/en-US/docs/Web/API/AbortController) и [AbortSignal — MDN](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal) — перед практикой с отменой запроса
5. [ ] [Working with JSON — MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON) — как пример рабочего паттерна загрузки данных