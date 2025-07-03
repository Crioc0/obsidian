2025 07 0309 21
Tags: #vue 
###### Links: 
1) [[VueRouter]]
# Заметка
Vue хорошо подходит для создания SPA. Для большинства SPA рекомендуется использовать официально поддерживаемую библиотеку Vue Router
## Простая маршрутизация с нуля
Если вам нужна только очень простая маршрутизация и вы не хотите привлекать полнофункциональный роутер, то можно обойтись [динамическими компонентами](https://ru.vuejs.org/guide/essentials/component-basics.html#dynamic-components) и обновлять текущее состояние компонента, прослушивая [`hashchange` события](https://developer.mozilla.org/en-US/docs/Web/API/Window/hashchange_event) браузера или используя [History API](https://developer.mozilla.org/en-US/docs/Web/API/History).
```js
<script setup>
import { ref, computed } from 'vue'
import Home from './Home.vue'
import About from './About.vue'
import NotFound from './NotFound.vue'

const routes = {
  '/': Home,
  '/about': About
}

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || NotFound
})
</script>

<template>
  <a href="#/">Главная страница</a> |
  <a href="#/about">О нас</a> |
  <a href="#/non-existent-path">Несуществующая ссылка</a>
  <component :is="currentView" />
</template>
```