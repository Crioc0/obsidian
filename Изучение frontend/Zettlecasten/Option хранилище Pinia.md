2025 07 0716 30
Tags: #vue 
###### Links: 
1) 
# Заметка
Аналогично Options API в Vue, мы также можем передать объект опций со свойствами `state`, `actions` и `getters`.
```js
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0, name: 'Иван' }),
  getters: {
    doubleCount: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++
    },
  },
})
```
Можно представить `state` как `data` хранилища, `getters` как `computed` свойства хранилища и `actions` как `methods`.

Option-хранилища должны быть интуитивными и простыми в использовании для начала работы.