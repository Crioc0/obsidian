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
