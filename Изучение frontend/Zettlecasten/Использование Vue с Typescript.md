2025 07 0319 34
Tags: #vue #typescript
###### Links: 
1) [[TS с CompositionAPI]]
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
```js
import { defineComponent } from 'vue'

export default defineComponent({
  // включен вывод типа
  props: {
    message: String
  },
  setup(props) {
    props.message // тип: string | undefined
  }
})
```

### Использование в однофайловых компонентах[​](https://ru.vuejs.org/guide/typescript/overview.html#usage-in-single-file-components)

Чтобы использовать TypeScript в SFC, добавьте атрибут `lang="ts"` к тегам `<script>`. При наличии `lang="ts"` все шаблонные выражения также проходят более строгую проверку типов.
```vue
<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      count: 1
    }
  }
})
</script>

<template>
  <!-- включена проверка типов и автозаполнение -->
  {{ count.toFixed(2) }}
</template>
```

`lang="ts"` может также использоваться с `<script setup>`:


```vue
<script setup lang="ts">
// TypeScript включен
import { ref } from 'vue'

const count = ref(1)
</script>

<template>
  <!-- включена проверка типов и автозаполнение -->
  {{ count.toFixed(2) }}
</template>
```
### TypeScript в шаблонах[​](https://ru.vuejs.org/guide/typescript/overview.html#typescript-in-templates)

Шаблон `<template>` также поддерживает TypeScript в выражениях привязки, когда используется `<script lang="ts">` или `<script setup lang="ts">`. Это полезно в тех случаях, когда вам нужно выполнить приведение типов в выражениях шаблона.

## `Generic` компоненты[​](https://ru.vuejs.org/guide/typescript/overview.html#generic-components)

`Generic` компоненты поддерживаются в двух случаях:

- В `SFC`: [`<script setup>` с `generic` атрибутом](https://ru.vuejs.org/api/sfc-script-setup.html#generics)
- Рендер-функции / `JSX` компоненты: [сигнатура функции `defineComponent()`](https://ru.vuejs.org/api/general.html#function-signature)