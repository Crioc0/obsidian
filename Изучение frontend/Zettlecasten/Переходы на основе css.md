2025 06 3017 31
Tags: #vue 
###### Links: 
1) 
# Заметка
### Классы перехода
Для переходов появления/исчезновения применяются шесть классов.![[transition-classes.DYG5-69l.png]]
1. `v-enter-from`: Начало анимации появления элемента. Добавляется перед вставкой элемента, удаляется через один кадр после вставки элемента.
2. 1. `v-enter-active`: Активное состояние появления элемента. Этот класс остаётся на элементе в течение всей анимации появления. Добавляется перед вставкой элемента, удаляется по завершении перехода/анимации. Этот класс можно использовать для установки длительности, задержки или функции плавности (easing curve) анимации появления.
3. 1. `v-enter-to`: Завершение анимации появления элемента. Добавляется через один кадр после вставки элемента (тогда же удаляется `v-enter-from`), а удаляется после завершения перехода или анимации.
4. 1. `v-leave-from`: Начало анимации исчезновения элемента. Добавляется сразу после вызова анимации исчезновения, а удаляется через один кадр.
5. 1. `v-leave-active`: Активное состояние анимации исчезновения. Этот класс остаётся на элементе в течение всей анимации исчезновения. Он добавляется при вызове анимации исчезновения, а удаляется после завершения перехода или анимации. Этот класс можно использовать для установки длительности, задержки или функции плавности (easing curve) анимации исчезновения.
6. 1. `v-leave-to`: Завершение анимации исчезновения элемента. Добавляется через один кадр после вызова анимации исчезновения (тогда же удаляется `v-leave-from`), а удаляется после завершения перехода или анимации.
### Именованные переходы
Переход может быть назван с помощью свойства `name`:
```js
<Transition name="fade">
  ...
</Transition>
```
Для именованного перехода его классы переходов будут иметь префикс с названием, а не `v`
```js
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
```
### CSS-переходы
`<Transition>` чаще всего используется в сочетании с [собственными CSS-переходами](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions), как показано в базовом примере выше. CSS-свойство `transition` - это сокращение, позволяющее указать множество аспектов перехода, включая свойства, которые должны быть анимированы, длительность перехода и [функции плавности](https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function).
```js
<Transition name="slide-fade">
  <p v-if="show">привет</p>
</Transition>
```

```js
/*
  Анимации появления и исчезновения могут иметь
  различные продолжительности и функции плавности.
*/
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
```
### CSS-анимации
[Собственные CSS-анимации](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations) применяются таким же образом, что и CSS-переходы. Они отличаются лишь тем, что `*-enter-from` удаляется не сразу после вставки элемента, а при наступлении события `animationend`.

Для большинства CSS-анимаций мы можем просто объявить их в классах `*-enter-active` и `*-leave-active`. Вот пример:
```js
<Transition name="bounce">
  <p v-if="show" style="text-align: center;">
    Привет, вот какой-то задорный текст!
  </p>
</Transition>
```

```js
.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}
```
### Пользовательские классы переходов
Вы также можете указать пользовательские классы переходов, передав в `<Transition>` следующие входные параметры:

- `enter-from-class`
- `enter-active-class`
- `enter-to-class`
- `leave-from-class`
- `leave-active-class`
- `leave-to-class`

Они будут заменять обычные имена классов. Это особенно полезно, если вы хотите объединить систему переходов Vue с существующей библиотекой анимации CSS, например [Animate.css](https://daneden.github.io/animate.css/):
```js
<!-- при условии, что Animate.css добавлен на странице -->
<Transition
  name="custom-classes"
  enter-active-class="animate__animated animate__tada"
  leave-active-class="animate__animated animate__bounceOutRight"
>
  <p v-if="show">привет</p>
</Transition>
```
### Совместное использование переходов и анимаций
Для определения завершения анимации Vue использует слушатели событий с типом `transitionend` или `animationend`, в зависимости от типа применяемых CSS-правил. Если используется только один подход из них, Vue определит правильный тип автоматически. Если нужно использовать оба подхода, то в таких случаях потребуется явное указание типа события, на которое должен ориентироваться Vue. Для этого нужно использовать атрибут `type` со значением `animation` или `transition`:
```js
<Transition type="animation">...</Transition>
```
### Вложенные переходы и явные длительности переходов
Хотя классы перехода применяются только к непосредственному дочернему элементу `<Transition>`, мы можем переходить к вложенным элементам с помощью вложенных CSS-селекторов:
```js
<Transition name="nested">
  <div v-if="show" class="outer">
    <div class="inner">
      Привет
    </div>
  </div>
</Transition>
```

```js
/* правила, нацеленные на вложенные элементы */
.nested-enter-active .inner,
.nested-leave-active .inner {
  transition: all 0.3s ease-in-out;
}

.nested-enter-from .inner,
.nested-leave-to .inner {
  transform: translateX(30px);
  opacity: 0;
}

/* ... другие необходимые CSS не указаны */
```