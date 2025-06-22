2025 06 2212 15
Tags: #vue 
###### Links: 
1) 
# Заметка
Можно размещать выражения внутри шаблонов, но они не всегда удобны ввиду того, что шаблон раздувается и становится сложным для понимания. Поэтому для сложной логики, включающей реактивные данные следует использвать вычисляемые свойства
```js
<script setup>
import { reactive, computed } from 'vue'

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

// ref вычисляемого свойства
const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Да' : 'Нет'
})
</script>

<template>
  <p>Есть опубликованные книги:</p>
  <span>{{ publishedBooksMessage }}</span>
</template>
```
Функция computed() ожидает передачу функции-геттера и возвращает значение в виде ref вычисляемого свойства.
Того же результата можно добиться использованием функции, но тогда значение не будет кэшироваться.
По умолчанию передается только геттер, но в случае необходимости можно передать еще и сеттер
```js
<script setup>
import { ref, computed } from 'vue'

const firstName = ref('John')
const lastName = ref('Doe')

const fullName = computed({
  // геттер (для получения значения)
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // сеттер (при присвоении нового значения)
  set(newValue) {
    // Примечание: это синтаксис деструктурирующего присваивания
    [firstName.value, lastName.value] = newValue.split(' ')
  }
})
</script>
```
С версии 3.4 можно получить предыдущее значение возвращенное вычисляемым свойством, обратившись к первому аргументу геттера
```js

```