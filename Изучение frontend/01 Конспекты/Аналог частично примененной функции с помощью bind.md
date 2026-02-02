---
tags:
  - review
created: 2026-01-24
related:
  - "[[Частично примененные функции]]"
repeat: spaced every 96 hours
due_at: 2026-02-06T16:18:39.524+03:00
---
# Аналог частично примененной функции с помощью bind


## Что это? (Определение)
Применять bind для создания частично примененной функции не очень удобно, так как во-первых, bind первым аргументом принимает значение для аргумента this, во вторых, bind не вызывает функцию, а создает новую

## Улучшенный вариант
```ts
function call(fn,...args){
	if(fn.length > args.length)	{
		return fn.bind(null, ...args)
	}
	
	return fn(...args)
}

const sum = (a,b,c)=>a+b+c
const add42 = call(sum,10,32)

console.log(call(add42,10)); // 52
```


