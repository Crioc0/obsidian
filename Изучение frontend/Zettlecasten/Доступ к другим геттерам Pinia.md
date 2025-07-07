2025 07 0717 17
Tags: #vue 
###### Links: 
1) 
# Заметка
Как и в случае с вычисляемыми свойствами, вы можете комбинировать несколько геттеров. Доступ к любому другому геттеру осуществляется через `this`. В этом случае **вам нужно будет указать возвращаемый тип** для геттера:
```js
export const useCounterStore = defineStore('counter', {
  state: () => ({
    count: 0,
  }),
  getters: {
    doubleCount(state) {
      return state.count * 2
    },
    doubleCountPlusOne(): number {
      return this.doubleCount + 1
    },
  },
})
```