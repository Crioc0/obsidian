---
tags:
  - review
created: 2026-01-24
related:
repeat: spaced every 24 hours
due_at: 2026-02-06T16:18:39.524+03:00
---
# Применение ap с массивами


## Что это? (Определение)
Стандартный map передает дополнительные аргументы своему фунаргу и не учитывает частичное применение фунарга, поэтому нужно делать свою реализацию map

```js
function map(ctx, fn) { 
	const res = new Array(ctx.length); 
	
	for (let i = 0; i < ctx.length; i++) { 
		res[i] = call(fn, ctx[i]);
	} 
	return res; 
} 

function ap(ctx, arr) { 
	return ctx.flatMap((fn) => map(arr, x => call(fn, x))); 
}
```

```js
const modifiers = ['primary', 'secondary', 'disabled'];
 const states = ['hover', 'active', 'focus']; 
 const classes1 = ap(ap([(mod, state) => `btn-${mod}-${state}`], modifiers), states); 
 // [ // 'btn-primary-hover', 
 // 'btn-primary-active', 
 // 'btn-primary-focus', 
 // 'btn-secondary-hover', 
 // 'btn-secondary-active', 
 // 'btn-secondary-focus', 
 // 'btn-disabled-hover', 
 // 'btn-disabled-active', 
 // 'btn-disabled-focus' 
 // ] 
 console.log(classes1);
```
## Зачем это нужно? (Применение)


## Как это работает? (Принцип)


## Пример 


## Ссылки