---
tags:
  - ФП
created: 2026-01-24
related:

  - "[[Аппликативные функторы]]"
repeat: spaced every 144 hours
due_at: 2026-03-29T13:07:55.614+03:00

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

Можно применять с несколькими функциями
```js
/// [ 100, 200, 300, 1000, 2000, 3000 ] 
console.log(ap([(x) => x * 100, (x) => x * 1000], [1, 2, 3]));
```
## Зачем это нужно? (Применение)


## Как это работает? (Принцип)


## Пример 


## Ссылки