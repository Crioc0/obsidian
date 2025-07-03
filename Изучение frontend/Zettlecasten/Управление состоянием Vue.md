2025 07 0309 28
Tags: 
###### Links: 
1) 
# Заметка
Технически каждый экземпляр компонента Vue уже "управляет" своим реактивным состоянием. Возьмём для примера простой компонент счетчика:
```js
<script setup>
import { ref } from 'vue'

// состояние
const count = ref(0)

// действия
function increment() {
  count.value++
}
</script>

<!-- представление -->
<template>{{ count }}</template>
```