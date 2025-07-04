2025 06 2816 03
Tags: #vue 
###### Links: 
1) [[]]
# Заметка
Для работы с динамическими классами можно использовать v-bind для вычисления строки выражения, но это не очень удобно, так как заниманиться контакенацие строк может привести к оштибкам. Для этого Vue предоставляет директиве v-bind специальные улучшения при работе с class и style. Кроме строк, выражения могут принимать массивы и объекты.

## Объектный синтаксис
Можно передавать объект в `:class` (сокращение для `v-bind:class`) для динамической установки или удаления CSS-классов:
```js
<div :class="{ active: isActive }"></div>
```
Также можно использовать вместе с обычным атрибутом class, и управлять несколькими классами
```js
const isActive = ref(true)
const hasError = ref(false)

<div
  class="static"
  :class="{ active: isActive, 'text-danger': hasError }"
></div>
```
Так как это рефы, класс ,будут динамически меняться
Также можно использовать [[Вычисляемые свойства в VUE(computed)| Вычисляемые свойства]], который возвращает итоговый объект
```js
const isActive = ref(true)
const error = ref(null)

const classObject = computed(() => ({
  active: isActive.value && !error.value,
  'text-danger': error.value && error.value.type === 'fatal'
}))
<div :class="classObject"></div>
```
## Синтаксис массивов
Можно передать список классов массивом.
```js
const activeClass = ref('active')
const errorClass = ref('text-danger')

<div :class="[activeClass, errorClass]"></div>
```
Переключать классы в массиве в зависимости от условия можно с помощью тернарного оператора
```js
<div :class="[isActive ? activeClass : '', errorClass]"></div>
```
Также можно использовать смешанный синтаксис
```js
<div :class="[{ [activeClass]: isActive }, errorClass]"></div>
```
## Работа с компонентами
При использовании атрибута `class` на пользовательском компоненте с одним корневым элементом, классы будут добавлены к этому корневому элементу. Существующие классы на этом элементе останутся и не будут перезаписаны.
Если у компонента несколько корневых элементов, то потребуется определить какой из них будет получать эти классы. Это реализуется добавлением свойства `$attrs` на элемент:
```js
<!-- шаблон MyComponent с использованием $attrs -->
<p :class="$attrs.class">Привет</p>
<span>Это дочерний компонент</span>

<MyComponent class="baz" />

<p class="baz">Привет</p>
<span>Это дочерний компонент</span>
```

## Привязка inline-стилей
Объектный синтаксис для `:style` выглядит почти как для CSS, за исключением того, что это объект JavaScript и соответствует свойству style элемента javascript
```js
const activeColor = ref('red')
const fontSize = ref(30)

<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```
Хотя рекомендуется использовать ключи в camelCase, `:style` также поддерживает ключи CSS-свойств в kebab-case (соответствует тому, как они используются в реальном CSS) — например:
```js
<div :style="{ 'font-size': fontSize + 'px' }"></div>
```
### Автоматические префиксы[​](https://ru.vuejs.org/guide/essentials/class-and-style.html#auto-prefixing)

Если использовать CSS-свойство, которое требует [вендорного префикса](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix) в `:style`, Vue автоматически добавит соответствующий префикс. Во время выполнения будет проверять какие стилевые свойства поддерживаются в текущем браузере. Если определённое свойство не поддерживается браузером, то будут проверены различные варианты префиксов, чтобы попытаться найти тот, который поддерживается.
```js
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```