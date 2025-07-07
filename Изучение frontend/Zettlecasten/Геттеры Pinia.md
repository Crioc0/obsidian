2025 07 0717 15
Tags: #vue 
###### Links: 
1) [[Доступ к другим геттерам Pinia]]
# Заметка
Геттеры (getters) являются эквивалентом [вычисляемых свойств](https://vuejs.org/guide/essentials/computed.html) для состояния хранилища. Их можно определить с помощью свойства `getters` в `defineStore()`. Они принимают `state` как первый параметр для поощрения использования стрелочной функции:
```js
export const useCounterStore = defineStore('counter', {
  state: () => ({
    count: 0,
  }),
  getters: {
    doubleCount: (state) => state.count * 2,
  },
})
```
В большинстве случаев геттеры полагаются только на состояние, однако, им может потребоваться использовать другие геттеры. Для этого мы можем получить доступ к _экземпляру всего хранилища_ через `this` при определении через обычную функцию, **но при этом необходимо определить тип возвращаемого значения (в TypeScript)**. Это связано с известным ограничением в TypeScript и **не затрагивает геттеры, определенные с помощью стрелочной функции, а также геттеры, не использующие `this`**:
```js
export const useCounterStore = defineStore('counter', {
  state: () => ({
    count: 0,
  }),
  getters: {
    // автоматически определяет тип возвращаемого значения как число
    doubleCount(state) {
      return state.count * 2
    },
    // тип возвращаемого значения **должен** быть явно задан
    doublePlusOne(): number {
      // автозаполнение и типизация для всего хранилища ✨
      return this.doubleCount + 1
    },
  },
})
```
Теперь вы можете получить доступ к геттеру напрямую через экземпляр хранилища:
```js
<script setup>
import { useCounterStore } from './counterStore'

const store = useCounterStore()
</script>

<template>
  <p>Double count is {{ store.doubleCount }}</p>
</template>
```