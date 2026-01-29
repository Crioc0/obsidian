---
tags:
  - концепция
  - review
created: 2026-01-24
related:
  - "[[Виды вычислительный контейнеров]]"
repeat: spaced every day
due_at: 2026-01-30T06:00:00.000+03:00
---
# Контейнер Option


## Что это? (Определение)
Контейнер предоставляет единый плоский API вместо if/else

## Зачем это нужно? (Применение)
Позволяет избавиться от специальных константа: -1, null, NaN и так далее

## Как это работает? (Принцип)


## Пример 
```js
getUserById(42) 
// Если такого пользователя нет, то вернет None 
.flatMap((user) => getUserFriends(user)) 
// Выполниться, только если такой пользователь найден 
// getUserFriends(user) вернет None, если друзей нет 
.map(friends => friends.filter(({name}) => name.startWith("B")));
// Функция выполнится только в случае Some
```
Пример контейнера Option с использованием классов
```js
class Option { 
	static None = new Option(0); 
	static Some(value) { return new Option(1, value); }; 
	#value; 
	#state = 0; // 0 значит данных нет 
	constructor(state, value = undefined) { 
		this.#state = state; 
		this.#value = value; } 
	isNone() { return this.#state === 0; } 
	
	or(value) { return this.isNone() ? Option.Some(value) : this; } 
	
	flatMap(fn) { return this.isNone() ? this : fn(this.#value); } 
	
	map(fn) { return this.isNone() ? this : Option.Some(fn(this.#value)); 
}
```