2025 09 2311 24
Tags: #nodejs 
###### Links: 
1) 
# Заметка
Для создания токенов воспользуемся пакетом `jsonwebtoken`. Его нужно установить и импортировать в проект:
```ts
// controllers/users.ts

import jwt from 'jsonwebtoken'; // импортируем модуль jsonwebtoken
```
Затем нужно вызвать метод `jwt.sign`, чтобы создать токен.
