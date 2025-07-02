2025 07 0214 40
Tags: #vue 
###### Links: 
1) 
# Заметка
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