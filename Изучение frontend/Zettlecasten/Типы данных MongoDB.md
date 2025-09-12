2025 09 1214 42
Tags: #MongoDB 
###### Links: 
1) 
# Заметка
Данные в MongoDB хранятся в формате BSON (binary JSON) — расширение над форматом JSON. Поэтому MongoDB поддерживает все типы данных, которые есть в JSON. Но помимо них есть и другие: ObjectId, Date, Regular Expression и даже JavaScript .Со всеми типами вы можно ознакомиться [в документации](https://mongodb.prakticum-team.ru/docs/manual/reference/bson-types/).
Тип ObjectId создан для уникальных итендефикаторов. У каждого документа такой создается автоматически, но его можно добавить  самостоятельно