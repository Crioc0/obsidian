---
repeat: spaced every 24 hours
created: 2025-10-08 14:26
tags:
  - vue
due_at: 2025-10-24T10:45:17.476+03:00
---
# 202510081426 Transition group

*Ссылка на StructureNote:*
*Ссылка на исходник или контекст (если есть):*

`<TransitionGroup>` это встроенный компонент, предназначенный для создания анимации при добавлении, удалении и изменении порядка элементов или компонентов, которые отображаются в списке.

## Отличия от `<Transition>`[​](https://ru.vuejs.org/guide/built-ins/transition-group.html#differences-from-transition)

`<TransitionGroup>` поддерживает те же параметры, классы CSS-переходов, и JavaScript-хуки слушателей, что и `<Transition>`, со следующими отличиями:

- По умолчанию он не отображает элемент-обертку. Однако вы можете указать элемент, который будет отображаться с помощью атрибута `tag`.
- [Режимы переходов](https://ru.vuejs.org/guide/built-ins/transition.html#transition-modes) недоступны, так как мы больше не переключаемся туда-сюда между взаимоисключающими элементами.
- Элементы внутри **всегда должны** иметь уникальный атрибут `key`.
- Классы CSS-перехода будут применяться к отдельным элементам в списке, а не к самой группе / контейнеру.

## Анимация добавления / удаления элементов списка

Вот пример анимации перехода добавления / удаления элементов `v-for` списка используя `<TransitionGroup>`:

```js
<TransitionGroup name="list" tag="ul">
  <li v-for="item in items" :key="item">
    {{ item }}
  </li>
</TransitionGroup>
```

```js
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
```

Чтобы при удалении или добавлении элементы не прыгали, нужно добавить несколько дополнительных правил CSS

```js
.list-move, /* применять переход к движущимся элементам */
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

/* убедитесь, что удаляющиеся элементы выведены из потока, чтобы 
анимации перемещения могли быть рассчитаны правильно. */
.list-leave-active {
  position: absolute;
}
```

## Задержка переходов списка[​](https://ru.vuejs.org/guide/built-ins/transition-group.html#staggering-list-transitions)

Настраивая JavaScript-переходы через data-атрибуты, также можно настроить задержку для переходов в списке. Сначала мы отображаем индекс элемента как data-атрибут в DOM:

```js
<TransitionGroup
  tag="ul"
  :css="false"
  @before-enter="onBeforeEnter"
  @enter="onEnter"
  @leave="onLeave"
>
  <li
    v-for="(item, index) in computedList"
    :key="item.msg"
    :data-index="index"
  >
    {{ item.msg }}
  </li>
</TransitionGroup>
```

Затем, в JavaScript-хуках, мы анимируем элемент с задержкой, отталкиваясь от этого data-атрибута.

```js
function onEnter(el, done) {
  gsap.to(el, {
    opacity: 1,
    height: '1.6em',
    delay: el.dataset.index * 0.15,
    onComplete: done
  })
}
```

# Связанные идеи:

* [[202510081419 Встроенные компоненты в Vue]]

---

*Что стоит развить? Какие вопросы возникли?*
