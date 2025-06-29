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
Значение, возвращаемое функцией `defineModel()`, представляет собой `ref`. К ней можно получить доступ и изменить так же, как и любую другую `ref`, за исключением того, что она действует как двустороннее связывание между родительским значением и локальным значением:

- Значение `.value` синхронизировано со значением, связанным с родительским `v-model`;
- Когда оно изменяется дочерним элементом, это приводит к обновлению значения, связанного с родителем.

реализация того же  дочернего компонента, который был показан выше до версии 3.4:
```js
<!-- Child.vue -->
<script setup>
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])
</script>

<template>
  <input
    :value="props.modelValue"
    @input="emit('update:modelValue', $event.target.value)"
  />
</template>
```
Затем `v-model="foo"` в родительском компоненте будет скомпилирован в:
```js
<!-- Parent.vue -->
<Child
  :modelValue="foo"
  @update:modelValue="$event => (foo = $event)"
/>
```
