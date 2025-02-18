2025 02 172205
Tags: #react #библиотеки
Links: 

Для реализации star-raiting я использовал следующие библиотеки :
1) @fortawesome/react-fontawesome
2) @fortawesome/free-regular-svg-icons
Последовательность следующая - я создал массив при помощи `Array` и заполнил его элементами с помощью `fill`. Далее этот массив я перебрал с помощью `map`, создав для каждого элемента `div` с компонентом `FontAwesomeIcon`. Для возможности выбора текущего элемента использовал два `useState`, для `currentStar` с изменением при клике, и `setHoverItem`. Для реализации подсвечивания к каждой итерации map добавлял следующую конструкцию.
```js
        const currentStyle = index <= currentStar ? { color: "gold" } : {};

        const hoverStyle = index <= hoverItem ? { color: "gold" } : {};
```


