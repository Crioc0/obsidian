---
tags:
  - review
  - концепция
created: 2026-01-24
related:
repeat: spaced every 48 hours
due_at: 2026-02-26T15:27:48.037+03:00
---
# Как curry работает с контейнерами


## Что это? (Определение)
При применении каррированной функции к контейнеру появляется контейнер с функцией.
Теперь нельзя применить map или flatMAp без вспомогательной лямбды: 
```js
Option.Some(42).map(sum).map(fn=>fn(10))
```
На практике чаще всего передаваемым аргументом будет Option

Но возникает проблема -  функция не знает, как работать с этим Option
```js
findAge("Боб").map(curry((a+b)=>a+b)).map(sum=>sum(findAge("Джен")))

// TypeError : sum ждет число, а получает Option<number>
```

Можно вызвать функцию на контейнере напрямую с помощью map, но появляется обертка в виде Option Option
```js
findAge("Боб").
	.map(curry((a,b)=>a+b))
	.map(sum=>findAge("Джен").map(sum)) //Option<Option<number>>
```
Для избегания этого можно использовать flatMap
```js
findAge("Боб").
	.map(curry((a,b)=>a+b))
	.flatMap(sum=>findAge("Джен").map(sum)) //<Option<number>
```

Чтобы не городить flatMap, можно использовать аппликативные функторы
Он будет вызывать функцию в контексте контейнера с переданными аргументами. результатом буде значение также упакованное в контейнер
```js
Option.Some(42).map(sum).ap(10) // Some(52)
Option.None.map(sum).ap(Option.Some(10)) // None
Option.Some(42).map(sum).ap(Option.None) // None
```


## Зачем это нужно? (Применение)


## Как это работает? (Принцип)
```js
const sum = curry((a,b)=>a+b)

Option.Some(42).map(sum)
```

## Пример 


## Ссылки
[[Аппликативные функторы]] 
[[Вычислительные контейнеры]]