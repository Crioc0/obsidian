2025 07 0309 20
Tags: #vue 
###### Links: 
1) 
# Заметка
Команда Vue поддерживает [eslint-plugin-vue](https://github.com/vuejs/eslint-plugin-vue), плагин [ESLint](https://eslint.org/), поддерживающий правила линтинга, специфичные для SFC.

Пользователи, ранее использовавшие Vue CLI, могут привыкнуть к тому, что линтеры настраиваются через загрузчики webpack. Однако при использовании сборки на основе Vite наша общая рекомендация такова:

1. `npm install -D eslint eslint-plugin-vue`, затем следуйте [руководству по настройке](https://eslint.vuejs.org/user-guide/#usage) `eslint-plugin-vue`.
    
2. Установите расширения ESLint для IDE, например [ESLint для VS Code](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint), чтобы получать обратную связь от линтера прямо в редакторе во время разработки. Это также позволяет избежать лишних затрат на линтинг при запуске сервера разработки.
    
3. Запускайте ESLint как часть команды для создания production сборки, чтобы получить полную обратную связь от линтера перед публикацией в production.
    
4. (Необязательно) Инструменты настройки, такие как [lint-staged](https://github.com/okonet/lint-staged) для автоматического анализа измененных файлов при фиксации git.