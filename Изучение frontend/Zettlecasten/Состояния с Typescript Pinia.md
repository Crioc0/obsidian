2025 07 0716 43
Tags: #vue #typescript 
###### Links: 
1) [[Typescript]]
# Заметка
Для того чтобы сделать ваше состояние совместимым с TypeScript, вам не нужно много делать: убедитесь, что включен флаг [`strict`](https://www.typescriptlang.org/tsconfig#strict) или, по крайней мере, [`noImplicitThis`](https://www.typescriptlang.org/tsconfig#noImplicitThis), и Pinia автоматически будет выводить тип вашего состояния! Тем не менее, есть несколько случаев, когда вам следует помочь TypeScript с некоторыми явными преобразованиями типов:
``
```