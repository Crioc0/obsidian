---
tags:
  - концепция
  - review
created: 2026-01-24
related:
  - "[[Виды вычислительный контейнеров]]"
repeat: daily
due_at: 2026-01-25T16:03:38.464+03:00
---
# Контейнер Result


## Что это? (Определение)
Контейнер Result похож на Promise, только без состояния Pending. Представляет собой альтернативу исключениям.

Если Option, Result и другие контейнеры совместимы с Promise, такой API станет проще запомнить и компоновать.

Сами Promises совместимы с такими объектами (Thenable) и можно работать с await
## Зачем это нужно? (Применение)
 Вместо использования throw и try catch (исключений) можно просто возвращать Result


## Как это работает? (Принцип)


## Пример 

```js
class Result { 
	static Err(value) { return new Result(0, value); }; 
	static Ok(value) { return new Result(1, value); }; 
	static resolve(value) { return value instanceof Result ? value Result.Ok(value); }; 
	#value; 
	#state = 0; // 0 значит ошибка 
	constructor(state, value = undefined) { 
	this.#state = state; 
	this.#value = value; 
	} 
	
	isErr() { return this.#state === 0; } 
	then(fn) { 
	try { 
		return this.isErr() ? this : Result.resolve(fn(this.#value)); 
		} catch (err) { 
		return Result.Err(err); 
		} 
	 
	catch(fn) { 
		try { 
			return this.isErr() ? Result.resolve(fn(this.#value)) : this; 
		} catch (err) { 
			return Result.Err(err); 
		} 
	} 
}
 
console.log(await Result.Ok(42)); // 42
```