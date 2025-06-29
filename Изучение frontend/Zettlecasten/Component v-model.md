2025 06 2915 22
Tags: #vue 
###### Links: 
1) [[Основы компонентов]]
# Заметка
`v-model` можно использовать в компоненте для реализации двустороннего связывания.
```js
<!-- Child.vue -->
<script setup>
const model = defineModel()

function update() {
  model.value++
}
</script>

<template>
  <div>Родительский связанный v-model - это: {{ model }}</div>
  <button @click="update">Увеличение</button>
</template>
```
Далее родитель может связать значение с помощью `v-model`:
```js
<!-- Parent.vue -->
<Child v-model="countModel" />
```