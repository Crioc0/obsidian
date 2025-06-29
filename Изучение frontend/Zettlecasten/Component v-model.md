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
Поскольку `defineModel` объявляет входные параметры, вы можете также объявить входные параметры основного свойства, передав его в `defineModel`:
```js
// делает v-model обязательным
const model = defineModel({ required: true })

// установка значения по умолчанию
const model = defineModel({ default: 0 })
```
## Аргументы `v-model`
`v-model` может принимать аргумент:
```js
<MyComponent v-model:title="bookTitle" />
```
В дочернем компоненте мы можем поддерживать соответствующий аргумент, передав строку в `defineModel()` в качестве его первого аргумента:
```js
<!-- MyComponent.vue -->
<script setup>
const title = defineModel('title')
</script>

<template>
  <input type="text" v-model="title" />
</template>
```
Если необходимо передать входные параметры, то их следует передавать после имени модели:
```js
const title = defineModel('title', { required: true })
```
Использование до версии 3.4
```js
<!-- MyComponent.vue -->
<script setup>
defineProps({
  title: {
    required: true
  }
})
defineEmits(['update:title'])
</script>

<template>
  <input
    type="text"
    :value="title"
    @input="$emit('update:title', $event.target.value)"
  />
</template>
```
## Множественные привязки `v-model`
Используя возможность указывать конкретное свойство и событие, как мы узнали ранее с [аргументами `v-model`](https://ru.vuejs.org/guide/components/v-model.html#v-model-arguments), теперь мы можем создать несколько `v-model` на одном экземпляре компонента.

Каждый `v-model` будет синхронизироваться с разным свойством, без необходимости в дополнительных параметрах в компоненте:
```js
<UserName
  v-model:first-name="first"
  v-model:last-name="last"
/>

<script setup>
const firstName = defineModel('firstName')
const lastName = defineModel('lastName')
</script>

<template>
  <input type="text" v-model="firstName" />
  <input type="text" v-model="lastName" />
</template>
```
Использование до версии 3.4
```js
<script setup>
defineProps({
  firstName: String,
  lastName: String
})

defineEmits(['update:firstName', 'update:lastName'])
</script>

<template>
  <input
    type="text"
    :value="firstName"
    @input="$emit('update:firstName', $event.target.value)"
  />
  <input
    type="text"
    :value="lastName"
    @input="$emit('update:lastName', $event.target.value)"
  />
</template>
```
