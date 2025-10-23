---
created: 2025-10-06 10:39
tags:
  - sql
repeat: spaced every day
due_at: 2025-10-24T06:00:00.000+03:00
---
# 202510061039 QuerryBuilder

*Ссылка на StructureNote:* 
*Ссылка на исходник или контекст (если есть):* 

QueryBuilder — библиотека, которая помогает описать SQL запрос кодом на вашем языке программирования. Она ничего не знает о структуре вашей базы и оперирует теми данными, которые вы передаёте в её функции.

Например, вот так может выглядеть запрос, составленный при помощи Knex (одного из популярных Query Builder для Node.JS):

```ts
knex('tableName')
  .insert({
    email: "ignore@example.com",
    name: "John Doe"
  })
  .onConflict('email')
  .merge()
```

На выходе он будет преобразован в примерно такой запрос (в случае использования MySQL):

```sql
insert into `tableName` (`email`, `name`) values ('ignore@example.com', 'John Doe') on duplicate key update `email` = values(`email`), `name` = values(`name`)
```

QueryBuilder позволяет интегрировать SQL-запросы более органично, разделяя запрос на части, которые проще понимать и обрабатывать. Например, так:

```ts
knex
  .select('year', knex.raw('SUM(profit)')).from('sales')
  .groupByRaw('year WITH ROLLUP')
```

При выполнении этого кода на выходе мы получим запрос

```ts
select `year`, SUM(profit) from `sales` group by year WITH ROLLUP
```

### Связанные идеи:

* [[202509290926 Реляционные БД]]
---

*Что стоит развить? Какие вопросы возникли?*
