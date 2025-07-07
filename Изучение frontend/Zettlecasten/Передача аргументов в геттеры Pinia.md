2025 07 0717 18
Tags: #vue 
###### Links: 
1) 
# Заметка
_Геттеры_ на самом деле под капотом являются _вычисляемыми свойствами_, поэтому нельзя передавать им какие-либо параметры. Однако вы можете вернуть функцию из _геттера_, чтобы принимать любые аргументы:
```js
export const useStore = defineStore('main', {
  getters: {
    getUserById: (state) => {
      return (userId) => state.users.find((user) => user.id === userId)
    },
  },
})
```
и использовать в компоненте:
```js
<script setup>
import { storeToRefs } from 'pinia'
import { useUserListStore } from './store'

const userList = useUserListStore()
const { getUserById } = storeToRefs(userList)
// обратите внимание, вам придется использовать `getUserById.value`,
// чтобы получить доступ к функции в пределах <script setup>
</script>

<template>
  <p>User 2: {{ getUserById(2) }}</p>
</template>
```
Обратите внимание, что при этом **геттеры больше не кэшируются**. Они являются обычными функциями, которые вы вызываете. Однако вы можете кэшировать некоторые результаты внутри самого геттера, что необычно, но может оказаться более производительным:
```js
export const useStore = defineStore('main', {
  getters: {
    getActiveUserById(state) {
      const activeUsers = state.users.filter((user) => user.active)
      return (userId) => activeUsers.find((user) => user.id === userId)
    },
  },
})
```