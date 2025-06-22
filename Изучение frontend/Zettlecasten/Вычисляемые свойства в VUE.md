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
Функция computed() ожидает передачу функции-геттера и возращет значение в виде ref вычисляемого свойтства.
Того же резаультата можно добиться 