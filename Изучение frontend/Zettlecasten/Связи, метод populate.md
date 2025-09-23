2025 09 2310 59
Tags: #mongoose 
###### Links: 
1) 
# Заметка
Построение связи начинается со схемы. Чтобы связать один документ с другим на уровне схемы, можно указать на уровне схемы тип поля `mongoose.Schema.Types.ObjectId` и свойство `ref`. В ref записывается имя модели, на которую мы ссылаемся.
```ts
const adSchema = new mongoose.Schema({
  title: {
    type: String,
    minlength: 2,
    maxlength: 20,
    required: true,
  },
  text: {
    type: String,
    minlength: 2,
    required: true,
  },
  // создаём поле creator
  creator: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'user',
    required: true
  },
});
```
При создании документа в поле  с `ref` мы записывает `_id` 