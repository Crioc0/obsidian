---
tags:
  - ФП
created: 2026-01-24
related:
repeat: spaced every 144 hours
due_at: 2026-03-24T11:32:57.961+03:00
---
# flip() в каррированных функциях


## Что это? (Определение)
`flip()` — это маленькая, но мощная утилита, которая делает каррированные функции более гибкими, позволяя менять порядок их применения в зависимости от потребностей конкретного сценария.

## Зачем это нужно? (Применение)

1. **Когда порядок аргументов неудобен** для частичного применения
    
2. **При адаптации функций** под определенный интерфейс
    
3. **В функциональных цепочках** для улучшения потока данных
    
4. **При создании point-free стиля** (бесточечного стиля)

## Как это работает? (Принцип)


## Пример 
```js
const flip = (fn) => (...args) => fn(...args.reverse());

// Пример с обычной функцией
const subtract = (a, b) => a - b;
subtract(5, 3); // 2

const flippedSubtract = flip(subtract);
flippedSubtract(5, 3); // 3 - 5 = -2
```
Применение с каррированной функцией
```js
// Каррированная функция
const divide = a => b => a / b;

divide(10)(2); // 5

// Иногда нам нужно сначала передать делитель
const divideBy = flip(divide);

// Теперь можем создавать специализированные функции
const divideBy2 = divideBy(2);
divideBy2(10); // 5 (10 / 2)

const divideBy5 = divideBy(5);
divideBy5(10); // 2 (10 / 5)
```
Пример использования в библиотеке
```js
// В библиотеке Ramda flip используется часто
import { flip, includes, filter } from 'ramda';

const hasValue = flip(includes);

const items = ['apple', 'banana', 'orange'];
const fruitsToCheck = ['apple', 'grape'];

filter(hasValue(items), fruitsToCheck); // ['apple']
```

с этим примером подробнее
Когда мы хотим проверить, содержится ли элемент в массиве, мы обычно думаем так:

- У нас есть массив `items`
- Мы хотим проверить, содержит ли он определенное значение

Но функция `includes` ожидает: `includes(value, array)`

Поэтому если мы хотим создать функцию `hasValue`, которая принимает массив и проверяет, содержит ли он значение, нам нужно:
```js
// Так не сработает, потому что includes ожидает значение первым
const hasValue = (array) => (value) => includes(value, array); 

// Или с каррированием:
const hasValue = (array) => includes(???)(array) // Проблема: includes ждет значение первым
```
Решение следующее
```js
// flip(includes) меняет порядок аргументов:
// Было: includes(value, array) => boolean
// Стало: flip(includes)(array, value) => boolean

const hasValue = flip(includes);
// Теперь hasValue имеет сигнатуру: (array, value) => boolean
// Или в каррированном виде: (array) => (value) => boolean
```
Что происходит в примере
```js
const items = ['apple', 'banana', 'orange'];
const fruitsToCheck = ['apple', 'grape'];

// 1. hasValue(items) возвращает функцию:
//    (value) => includes(value, items)

// 2. filter применяет эту функцию к каждому элементу fruitsToCheck:
//    Для 'apple': hasValue(items)('apple') => includes('apple', items) => true
//    Для 'grape': hasValue(items)('grape') => includes('grape', items) => false

filter(hasValue(items), fruitsToCheck); // ['apple']
```
Визуализация потока данных
```js

///
fruitsToCheck = ['apple', 'grape']
items = ['apple', 'banana', 'orange']

filter(hasValue(items), fruitsToCheck)
  ↓
filter(
  fruit => includes(fruit, ['apple', 'banana', 'orange']),
  ['apple', 'grape']
)
  ↓
[
  'apple'  // проходит проверку: 'apple' ∈ ['apple', 'banana', 'orange']
  // 'grape' не проходит
]
```
## Ссылки
[[Каррирование]] 