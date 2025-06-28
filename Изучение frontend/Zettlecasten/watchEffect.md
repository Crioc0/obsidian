2025 06 2818 10
Tags: #vue 
###### Links: 
1) [[Наблюдатели]]
# Заметка
Обратный вызов наблюдателя обычно использует то же реактивное состояние, что и источник. Например,  следующий код использует наблюдатель для загрузки удаленного ресурса каждый раз, когда изменяется ссылка `todoId`
```js
const todoId = ref(1)
const data = ref(null)

watch(
  todoId,
  async () => {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
    )
    data.value = await response.json()
  },
  { immediate: true }
)
```
watcher использует `todoId` дважды, один раз в качестве источника, а затем снова внутри обратного вызова.

Это можно упростить с помощью функции [`watchEffect()`](https://ru.vuejs.org/api/reactivity-core.html#watcheffect). `watchEffect()` позволяет нам немедленно выполнить побочный эффект, автоматически отслеживая реактивные зависимости. Приведенный выше пример можно переписать следующим образом:
```js
watchEffect(async () => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  data.value = await response.json()
})
```