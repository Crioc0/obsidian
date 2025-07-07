2025 07 0716 31
Tags: #vue
###### Links: 
1) 
# Заметка
Аналогично [функции setup](https://vuejs.org/api/composition-api-setup.html) в Composition API Vue, мы можем передать функцию, которая определяет реактивные свойства и методы, и возвращает объект с свойствами и методами, которые мы хотим предоставить.`
```js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const name = ref('Иван')
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }

  return { count, name, doubleCount, increment }
})
```
в setup-хранилище ref становятся свойствами состояния, computed() ге
