---
tags:
  - концепция
  - review
created: 2026-01-24
related:
repeat: spaced every 144 hours
due_at: 2026-03-24T11:32:58.818+03:00
---
# Контейнер Lazy


## Что это? (Определение)
Контейнер Lazy нужен для ленивых вычислений. Это монадическое вычисление

## Зачем это нужно? (Применение)

Ленивыми называются вычисление, которые делаются не сразу, а по явному требованию. Например, пока пользователь не нажмет на кнопку или не включит специальную настройку

## Как это работает? (Принцип)

Мы можем выстраивать цепочки ленивых вычислений Вычисления произойдут только при явно вызове функции Повторные вызовы будут сразу возвращать готовый ответ без вычислений
## Пример 
```js
const readConfig = new Lazy(initConfig).then(applyConfig); console.log(readConfig.call()); // Функция выполниться только теперь
console.log(readConfig.call()); // Повторный вызов делаться не будет - сразу вернется результат 
console.log(readConfig.call());
```

```js
class Lazy {
	#work; 
	#value; 
	#state = 0; // 0 значит, что содержимое не вычислялось 
	constructor(work) { 
		this.#work = work; 
	} 
	call(thisArg, ...args) { 
		if (this.#state !== 0) { 
			return this.#value; 
		} 
		this.#state++; 
		return this.#value = this.#work.apply(thisArg, args); 
	} 
	then(work) { 
		return new Lazy(() => work(this.call())); 
	} 
}
```