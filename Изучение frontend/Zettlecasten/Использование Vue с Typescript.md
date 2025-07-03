2025 07 0319 34
Tags: #vue #typescript
###### Links: 
1) 
# Заметка
Vue написан на TypeScript и обеспечивает первоклассную поддержку TypeScript. Все официальные пакеты Vue поставляются с декларациями типов, которые должны работать "из коробки".
### `defineComponent()`[​](https://ru.vuejs.org/guide/typescript/overview.html#definecomponent)

Чтобы TypeScript мог правильно выводить типы внутри опций компонентов, необходимо определить компоненты с помощью функции [`defineComponent()`](https://ru.vuejs.org/api/general.html#definecomponent):
```js
import { defineComponent } from 'vue'

export default defineComponent({
  // включен вывод типа
  props: {
    name: String,
    msg: { type: String, required: true }
  },
  data() {
    return {
      count: 1
    }
  },
  mounted() {
    this.name // тип: string | undefined
    this.msg // тип: string
    this.count // тип: number
  }
})
```
`defineComponent()` также поддерживает вывод входных параметров, переданных в `setup()`, при использовании Composition API без `<script setup>`: