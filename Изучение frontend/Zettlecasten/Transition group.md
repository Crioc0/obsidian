2025 07 0214 58
Tags: #vue 
###### Links: 
1) 
# Заметка
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
Чтобы удаляющиеся элементы были выведены 