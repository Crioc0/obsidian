2025 07 0309 19
Tags: #vue 
###### Links: 
1) 
# Заметка
## Тестирование[​](https://ru.vuejs.org/guide/scaling-up/tooling.html#testing)

Основная статья: [Testing Guide](https://ru.vuejs.org/guide/scaling-up/testing.html).

- [Cypress](https://www.cypress.io/) рекомендуется для E2E-тестирования. Он также может быть использован для тестирования компонентов Vue SFC с помощью [Cypress Component Test Runner](https://docs.cypress.io/guides/component-testing/introduction).
    
- [Vitest](https://vitest.dev/) - это программа тестирования, созданная членами команды Vue / Vite и ориентированная на скорость. Он специально разработан для приложений на базе Vite, чтобы обеспечить такой же мгновенный цикл обратной связи для модульного/компонентного тестирования.
    
- [Jest](https://jestjs.io/) можно заставить работать с Vite с помощью [vite-jest](https://github.com/sodatea/vite-jest). Однако это рекомендуется делать только в том случае, если у вас есть существующие тестовые наборы на базе Jest, которые необходимо перенести на Vite, поскольку Vitest предоставляет аналогичные функции с гораздо более эффективной интеграцией.