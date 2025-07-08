2025 07 0817 33
Tags: #vue 
###### Links: 
1) [[https://learn.javascript.ru/mutation-observer]]
# Заметка
`MutationObserver` – это встроенный объект, наблюдающий за DOM-элементом и запускающий колбэк в случае изменений.

Сначала нужно создать наблюдатель за изменениями с помощью callback-функции, и прикрепляем его к DOM-узлу
```js
`let` observer `=` `new` `MutationObserver``(`callback`)``;`
```