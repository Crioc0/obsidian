2025 06 3016 26
Tags: #vue
###### Links: 
1) 
# Заметка
В контексте приложений Vue "composable" функция — это функция, использующая Composition API Vue для инкапсуляции и повторного использования **логики с отслеживанием состояния**.
Если нужно повторно использовать логику с отслеживанием состояния в нескольких компонентах, можно извлечь логику во внешний файл как компонуемую функцию.
```js
// mouse.js
import { ref, onMounted, onUnmounted } from 'vue'

// по соглашению имена composables функций начинаются с "use"
export function useMouse() {
  // состояние, инкапсулированное и управляемое composable
  const x = ref(0)
  const y = ref(0)

  // composable может обновлять своё управляемое состояние с течением времени.
  function update(event) {
    x.value = event.pageX
    y.value = event.pageY
  }

  // composable объект также может подключаться к жизненному циклу своего
  // компонента-владельца для настройки и удаления побочных эффектов.
  onMounted(() => window.addEventListener('mousemove', update))
  onUnmounted(() => window.removeEventListener('mousemove', update))

  // представлять управляемое состояние в качестве возвращаемого значения
  return { x, y }
}
```
И вот как его можно использовать в компонентах:
```js
<script setup>
import { useMouse } from './mouse.js'

const { x, y } = useMouse()
</script>

<template>Положение мыши: {{ x }}, {{ y }}</template>
```