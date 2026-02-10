---
tags:
  - концепция
  - review
created: 2026-01-24
related:
  - "[[Виды вычислительный контейнеров]]"
repeat: spaced every 56 hours
due_at: 2026-02-12T18:20:15.529+03:00
---
# Контейнер Result


## Что это? (Определение)
Контейнер Result похож на Promise, только без состояния Pending. Представляет собой альтернативу исключениям.

Если Option, Result и другие контейнеры совместимы с Promise, такой API станет проще запомнить и компоновать.

Сами Promises совместимы с такими объектами (Thenable) и можно работать с await
## Зачем это нужно? (Применение)
 Вместо использования throw и try catch (исключений) можно просто возвращать Result


## Как это работает? (Принцип)
Все равно происходит создание микротакски при использовании **await** по концепции **Thenable** объектов, но можно сделать метод unwrap, который будет возвращать значение контейнера или выбрасывать исключение. По сути await работает также, но await функция не дает исключению выйти за её пределы.  А в случае с **unwrap** в **синхронном** контексте выброшенное исключение может наделать дел. Можно создать методы, которые будут возвращать некоторое значение в случае ошибки, например
```js
console.log(Result.Err("Ooops").unwrap(42)); // 42
```
Либо завернуть unwrap внутрь блока if
```js
const value = Result.Err("Ooops"); 
if (!value.isErr()) { 
	const raw = value.unwrap(); 
	console.log(raw); 
	 }
```
Или инвертировать условие
```js
function doSomething(value) { 
	if (value.isErr()) { 
		return value; 
	} 
	value = value.unwrap(); 
	console.log(value); 
	
	return Result.Ok(); }
```

Так же можно повторить логику unwrap с использованием **генераторов**, по сути повторяя логику async await без завязки на микротаски, но код станет зашумленным, а использование генераторов не бесплатно

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

Пример с unwrap
```js
class Result { 
	static Err(value) { return new Result(0, value); }; 
	static Ok(value) { return new Result(1, value); }; 
	static resolve(value) { return value instanceof Result ? value : Result.Ok(value); }; 
	#value; 
	#state = 0; // 0 значит ошибка 
	constructor(state, value = undefined) { 
		this.#state = state; 
		this.#value = value; 
	} 
	
	isErr() { return this.#state === 0; } 
	unwrap() { 
		if (this.isErr()) { 
			throw this.#value; 
		} else { 
			return this.#value; 
		} 
	} 
	unwrapErr() { 
		if (this.isErr()) { 
			return this.#value; 
		} else { 
		throw this.#value; 
		} 
	} 
} 
console.log(Result.Ok(42).unwrap()); // 42 
console.log(Result.Err(42).unwrap()); // Oops
```
Пример с генераторами
```js
function exec(fn) { 
	const ctx = fn() ; 
	function next(step) { 
		try { 
			if (step.done) { 
				return Result.resolve(step.value ) ; 
			} 
			
			return Result.resolve(step.value ) 
				.then((value) => next(ctx.next(value))) 
				.catch((err) => next(ctx.throw(err))); 
		} catch (err) { 
			return Result.Err(err) ; 
		} 
	}
	 
	return next(ctx.next()) ; 
} 

exec (function* (){ 
	let value = yield Result.Ok (42 ) ; 
	console .log(value) ; 
	yield Result.Err ("Ooops" ) 
	}).catch (console .error ); // "Ooops
```