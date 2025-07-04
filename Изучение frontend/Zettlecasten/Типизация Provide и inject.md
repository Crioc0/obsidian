2025 07 0410 10
Tags: #vue #typescript 
###### Links: 
1) 
# Заметка
Provide и inject обычно выполняются в отдельных компонентах. Для правильной типизации внедряемых значений Vue предоставляет интерфейс `InjectionKey`, который представляет собой общий тип, расширяющий `Symbol`. Он может быть использован для синхронизации типа внедряемого значения между провайдером и потребителем:
```js
import { provide, inject } from 'vue'
import type { InjectionKey } from 'vue'

const key = Symbol() as InjectionKey<string>

provide(key, 'foo') // предоставление нестрокового значения приведет к ошибке

const foo = inject(key) // тип foo: string | undefined
```
