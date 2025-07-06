2025 06 2120 35
Tags: #vue 
###### Links: 
1) [[Реактивность-основное Composition API]]
# Заметка
В composition API логика компонента определяется использованием импортированных функций API. В одно файловых компонентах обычно используются с ```
```javascript
<script setup>
```
Атрибут setup подсказывает компилятору выполнить специальные преобразования на этапе компиляции
```javascript
<script setup>
import { ref, onMounted } from 'vue'

// реактивное состояние
const count = ref(0)

// функции которые мутируют состояние и вызывают обновления
function increment() {
  count.value++
}

// хуки жизненного цикла
onMounted(() => {
  console.log(`Стартовое значение счётчика — ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Счётчик: {{ count }}</button>
</template>
```