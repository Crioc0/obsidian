2025 06 2817 24
Tags: #vue 
###### Links: 
1) [[Директивы в Vue]]
# Заметка
При работе с формами часто требуется синхронизировать состояния элементов ввода в форме с соответствующим состоянием в JavaScript. Добавлять вручную привязки значений и обработчики событий изменения может быть обременительно:
```js
<input
  :value="text"
  @input="event => text = event.target.value"
>
```
Директива v-model помогает упростить вышесказанное до 
```js
<input v-model="text">
```
Кроме того, `v-model` может быть использована на полях различных типов, элементах `<textarea>` и `<select>`. Она автоматически разворачивается на различные пары свойств и событий DOM в зависимости от элемента на котором используется:

- Элементы `<input>` с текстовым типом и `<textarea>` используют свойство `value` и событие `input`;
- Элементы `<input type="checkbox">` и `<input type="radio">` используют свойство `checked` и событие `change`;
- Элементы `<select>` используют свойство `value` и событие `change`.

## Обычное использование
Текст
```js
<p>Сообщение: {{ message }}</p>
<input v-model="message" placeholder="отредактируй меня" />
```

### Многострочный текст
```js
<span>Многострочное сообщение:</span>
<p style="white-space: pre-line;">{{ message }}</p>
<textarea v-model="message" placeholder="введите несколько строчек"></textarea>
```

### Чекбоксы
```js
<input type="checkbox" id="checkbox" v-model="checked" />
<label for="checkbox">{{ checked }}</label>
```
Список чекбоксов, привязанных к массиву или значениям [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set):
```js
const checkedNames = ref([])

<div>Отмеченные имена: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames" />
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
<label for="mike">Mike</label>
```
### Радиокнопки
```js
<div>Выбрано: {{ picked }}</div>

<input type="radio" id="one" value="Один" v-model="picked" />
<label for="one">Один</label>

<input type="radio" id="two" value="Два" v-model="picked" />
<label for="two">Два</label>
```

### Выпадающие списки
```js
<div>Выбрано: {{ selected }}</div>

<select v-model="selected">
  <option disabled value="">Выберите один из вариантов</option>
  <option>А</option>
  <option>Б</option>
  <option>В</option>
</select>
```
Выбор нескольких вариантов из списка (с привязкой к массиву):
```js
<div>Выбраны: {{ selected }}</div>

<select v-model="selected" multiple>
  <option>А</option>
  <option>Б</option>
  <option>В</option>
</select>
```

Динамическое отображение списка опций с помощью `v-for`:
```js
const selected = ref('A')

const options = ref([
  { text: 'Один', value: 'A' },
  { text: 'Два', value: 'B' },
  { text: 'Три', value: 'C' }
])
```