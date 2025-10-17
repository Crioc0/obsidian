---
created: 2025-10-08 14:22
tags:
  - vue
---
# 202510081422 JavaScript хуки в Transition
*Ссылка на StructureNote:*
*Ссылка на исходник или контекст (если есть):* 

Вы можете подключиться к процессу перехода с помощью JavaScript, прослушивая события на компоненте `<Transition>`:
```js
<Transition
  @before-enter="onBeforeEnter"
  @enter="onEnter"
  @after-enter="onAfterEnter"
  @enter-cancelled="onEnterCancelled"
  @before-leave="onBeforeLeave"
  @leave="onLeave"
  @after-leave="onAfterLeave"
  @leave-cancelled="onLeaveCancelled"
>
  <!-- ... -->
</Transition>
```
```js
// вызывается перед вставкой элемента в DOM.
// используется для установки состояния "enter-from" элемента
function onBeforeEnter(el) {}

// вызывается через один кадр после вставки элемента.
// используйте его для запуска анимации входа.
function onEnter(el, done) {
  // вызов обратного вызова done для индикации окончания перехода
  // необязателен, если используется в сочетании с CSS
  done()
}

// вызывается по завершении перехода enter.
function onAfterEnter(el) {}

// вызывается, когда переход enter отменяется до завершения.
function onEnterCancelled(el) {}

// вызывается перед хуком leave.
// В большинстве случаев следует использовать только хук leave
function onBeforeLeave(el) {}

// вызывается, когда начинается переход к leave.
// используйте его для запуска анимации ухода.
function onLeave(el, done) {
  // вызов обратного вызова done для индикации окончания перехода
  // необязательно, если используется в сочетании с CSS
  done()
}

// вызывается, когда переход к leave завершен
// элемент был удален из DOM.
function onAfterLeave(el) {}

// доступно только при использовании переходов v-show
function onLeaveCancelled(el) {}
```
Эти хуки могут использоваться как в сочетании с CSS-переходами/анимацией, так и самостоятельно.
При использовании переходов, основанных только на JavaScript, обычно рекомендуется добавить параметр `:css="false"`
```js
<Transition
  ...
  :css="false"
>
  ...
</Transition>
```
При использовании `:css="false"` мы также полностью отвечаем за контроль окончания перехода. В этом случае обратные вызовы `done` необходимы для хуков `@enter` и `@leave`. В противном случае хуки будут вызываться синхронно и переход завершится немедленно.
Демонстрация использования [GSAP library](https://gsap.com/) для выполнения анимации. Конечно, вы можете использовать любую другую библиотеку анимации, например [Anime.js](https://animejs.com/) или [Motion One](https://motion.dev/).
# Связанные идеи:
* [[202510081420 Transition]]
---

*Что стоит развить? Какие вопросы возникли?*