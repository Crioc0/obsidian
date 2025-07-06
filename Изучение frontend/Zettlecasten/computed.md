2025 07 0611 13
Tags: #vue
###### Links: 
1) [[Вычисляемые свойства в VUE(computed)]]
# Заметка
Принимает геттер-функцию и возвращает иммутабельный реативный ref-объект для возвращаемого значения из геттера. Также можно вернуть объект, используя функции `get` и `set` для создания ref-объекта с возможностью записи.
**Тип**
```js
// только для чтения
function computed<T>(

  getter: (oldValue: T | undefined) => T,
  // см. ссылку "Отладка вычисляемых свойств" ниже
  debuggerOptions?: DebuggerOptions
): Readonly<Ref<Readonly<T>>>

// с возможностью записи
function computed<T>(
  options: {
    get: (oldValue: T | undefined) => T
    set: (value: T) => void
  },
  debuggerOptions?: DebuggerOptions
): Ref<T>
```
**Пример**
Создание вычисляемого ref-объекта только для чтения:
```js
const count = ref(1)
const plusOne = computed(() => count.value + 1)

console.log(plusOne.value) // 2

plusOne.value++ // ошибка
```
Создание вычисляемого ref-объекта с возможностью записи:
```js
const count = ref(1)
const plusOne = computed({
  get: () => count.value + 1,
  set: (val) => {
    count.value = val - 1
  }
})

plusOne.value = 1
console.log(count.value) // 0
```
Отладка