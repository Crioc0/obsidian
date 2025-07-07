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