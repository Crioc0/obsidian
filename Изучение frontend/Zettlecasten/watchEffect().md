2025 07 0611 48
Tags: #vue 
###### Links: 
1) 
# Заметка
Немедленно запускает функцию, отслеживая её зависимости с помощью системы реактивности, а затем повторно вызывает лишь при изменении этих зависимостей
**Тип**
```js
function watchEffect(
  effect: (onCleanup: OnCleanup) => void,
  options?: WatchEffectOptions
): WatchHandle

type OnCleanup = (cleanupFn: () => void) => void

interface WatchEffectOptions {
  flush?: 'pre' | 'post' | 'sync' // по умолчанию: 'pre'
  onTrack?: (event: DebuggerEvent) => void
  onTrigger?: (event: DebuggerEvent) => void
}

interface WatchHandle {
  (): void // callable, same as `stop`
  pause: () => void
  resume: () => void
  stop: () => void
}
```