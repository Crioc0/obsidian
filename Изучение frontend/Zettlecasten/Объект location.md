2025 02 2116 11
Tags: #javaScript 
###### Links: 
1) 
# Заметка
**Объект location** в JavaScript — это один из дочерних объектов window, который отвечает за адресную строку окна или вкладки браузера.  

**Объект location содержит информацию о расположении текущей веб-страницы**: URL, информацию о сервере, номер порта, протокол. 

**Некоторые свойства объекта location**:

- **href** — полный адрес URL веб-страницы; 
- **origin** — общая схема запроса; 
- **protocol** — протокол (включая двоеточие), например, http: или https:; [1](https://metanit.com/web/javascript/7.4.php)
- **host** — хост, например, localhost.com; [1](https://metanit.com/web/javascript/7.4.php)
- **hostname** — домен, аналогичен хосту, только не включает порт; [1](https://metanit.com/web/javascript/7.4.php)
- **port** — порт, используемый ресурсом; [1](https://metanit.com/web/javascript/7.4.php)
- **pathname** — путь к ресурсу — та часть адреса, которая идёт после хоста после слеша /; [1](https://metanit.com/web/javascript/7.4.php)
- **hash** — идентификатор фрагмента — та часть адреса, которая идёт после символа решётки # (при его наличии); [1](https://metanit.com/web/javascript/7.4.php)
- **search** — строка запроса — та часть адреса, которая идёт после знака вопроса ? (при его наличии); [1](https://metanit.com/web/javascript/7.4.php)
- **username** — имя пользователя, которое указано в адресе; [1](https://metanit.com/web/javascript/7.4.php)
- **password** — пароль, который указан в адресе. [1](https://metanit.com/web/javascript/7.4.php)

**Объект location предоставляет ряд методов**, которые можно использовать для управления адресом веб-страницы:

- **assign(url)** — загружает ресурс, который находится по пути url; [1](https://metanit.com/web/javascript/7.4.php)
- **reload(forcedReload)** — перезагружает текущую веб-страницу; [1](https://metanit.com/web/javascript/7.4.php)
- **replace(url)** — заменяет текущую веб-страницу другим ресурсом, который находится по пути url. [1](https://metanit.com/web/javascript/7.4.php)

