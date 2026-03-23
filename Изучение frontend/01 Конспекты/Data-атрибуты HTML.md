---
tags:
  - HTML
created: 2026-01-24
related:
  - "[[HTML]]"
repeat: spaced every 258 hours
due_at: 2026-03-29T06:00:00.000+03:00
---
# Data-атрибуты HTML


## Что это? (Определение)
Дата-атрибуты - специальные атрибуты, которые помогают хранить дополнительные данные прямо в HTML-тэгах

## Зачем это нужно? (Применение)
Для хранения данных, для работы с которыми не нужно пользоваться сторами, и избегать prop-drilling(не рекомендуется, это крайний способ).

Также можно использовать data-атрибут как селектор, и получать значение при помощи attr

## Как это работает? (Принцип)
Названия атрибутов должны начинаться с **data-**, и далее указывается имя, которое нужно. Данные, которые хранятся в дата-атрибутах, не отображаются в поисковых движках и внешних сервисах. Их можно получить через JavaScript, получив элемент и обратившись к свойству dataset. Чтобы добавить массив в data-атрибут, необходимо сделать преобразование в JSON

## Пример 
```js
<style>
	div::after {
		content: attr(data-color)
	}
	
	div[data-color="red"] {
		background-color:red
	}
</style>

<div id="my-div" data-color="red">Тест</div>
<script>
	const div = document.getElementById('my-div')
	
	console.log(div.dataset.color)
	
	div.dataset.arr = JSON.stringify([1,2,3])
	
	console.log(JSON.parse(div.dataset.arr))
</script>
```

