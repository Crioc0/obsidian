---
tags:
  - концепция
  - review
created: 2026-01-24
related:
repeat: spaced every 48 hours
due_at: 2026-02-04T16:18:41.281+03:00
---
# Promise API взамен исключений


## Что это? (Определение)
API Promise в JS удобно использовать в качестве замены [[Недостатки исключений | исключений]], но Promise имеет асинхронный дизайн, каждый then, catch и finally всегда выполняется отложено (создают микротаску), и если использовать Promise для синхронного кода, будут проблемы с производительностью

## Зачем это нужно? (Применение)


## Как это работает? (Принцип)


## Пример 
```js
function readConfig() { 
	return readFileSync("/etc/app/config.json") 
		.catch(_ => fs.readFile("~/.config/app.json")) 
		.catch(_ => fs.readFile("config.json")) 
		.then(content => { 
		if (content.trim().length > 0) { 
			return content; 
		} 
		throw "Empty config"; }) 
		.then(JSON.parse) 
		.catch(_ => ({})); // Дефолтные настройки 
}
 
readConfig().then(console.log);
```