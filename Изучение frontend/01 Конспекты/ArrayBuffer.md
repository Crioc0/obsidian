---
tags:
  - база
created: 2026-01-24
related:
  - "[[Типизированные массивы]]"
repeat: spaced every 24 hours
due_at: 2026-02-27T14:05:30.956+03:00
---

# ArrayBuffer

Любой типизированный массив можно создать на основе сырой памяти. Для JS для для представления таких значений есть ArrayBuffer и SharedArrayBuffer. Главная особенность такого создания, что типизированный массив не будет аллоцировать новую память, а использовать переданную. Фактически, в таком случае просто создается «обертка». Если в сырой памяти есть какие-то значения, то они будут интерпретироваться как значения массива. Можно получить доступ к буферу типизированного массива через геттер .buffer

```js
const buffer = new ArrayBuffer(1024); // Размер буфера указывается в байтах 
const arr1 = new Float64Array(buffer); 
console.log(arr1.length); // 128, так как один элемент Float64 занимает 0 байт 
console.log(arr1[0]); // 0, так как вся память проинициализирована нулями по умолчанию 

// Можно инициализировать небольшой буфер с возможностью роста 
const buffer2 = new ArrayBuffer(8, {maxByteLength: 1024}); 
const arr2 = new BigInt64Array(buffer2); 
console.log(arr2.length); // 1 
console.log(arr2[0]); // 0n 

// Меняем размер буфера 
arr2.buffer.resize(32); 

console.log(arr2.length); // 4
```

ArrayBuffer это честное представление потока байт, и можно прочитать любые данные таким образом

```js
const buffer = new ArrayBuffer(1024); // Размер буфера указывается в байтах
console.log(buffer.byteLength); // 1024
const 1 = {1:1,2:3}
console.log(buffer.resizable); // false // Можно передать владение буфера в другую память или поток console.log(buffer.detached); // false // Создает копию памяти и новый ArrayBuffer с возможностью задать диапазон копирования console.log(buffer.slice(0, 10)); // Отдали владение буфером и явно указали, что нас интересуют лишь первые 64 байта. // Допускается задать больше размер, чем у исходного буфера (но не больше maxByteLength если он задан). // Еще есть метод transferToFixedLength, который убирает возможно resizable у буфера, если таковая имелась. const newBuffer = buffer.transfer(64); console.log(newBuffer.byteLength); // 64 console.log(buffer.detached); // true console.log(buffer.byteLength); // 0, так как мы отдали владения буфером

```

## Ссылки

- 