2025 07 0611 33
Tags: #vue 
###### Links: 
1) 
# Заметка
Принимает объект (реактивный или обычный) или [ref-объект](https://ru.vuejs.org/api/reactivity-core.html#ref) и возвращает доступную только для чтения прокси к оригиналу.
**Тип**
```JS
function readonly<T extends object>(
  target: T
): DeepReadonly<UnwrapNestedRefs<T>>
```
**Подробности**