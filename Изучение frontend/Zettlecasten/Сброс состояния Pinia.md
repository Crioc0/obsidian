2025 07 0716 48
Tags: 
###### Links: 
1) 
# Заметка
В [option-хранилищах](https://pinia-ru.netlify.app/core-concepts/#option-stores) вы можете сбросить состояние до его начального значения, вызвав на хранилище метод `$reset()` :
```js
const store = useStore()

store.$reset()
```
При этом вызывается функция `state()`, которая создает новый объект state и заменяет им текущее состояние.

В [setup-хранилищах](https://pinia-ru.netlify.app/core-concepts/#setup-stores) необходимо создать собственный метод `$reset()`:
```js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)

  function $reset() {
    count.value = 0
  }

  return { count, $reset }
})
```