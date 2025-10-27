---
tags:
  - уровень_0
  - typeORM
---
### Связи с другими Structure Notes

[[]]

## Последние заметки за неделю

```dataview
LIST
FROM #typeORM   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

## Все заметки о MongoDB

```dataview
TABLE file.ctime as "Создана"
FROM #typeORM  
SORT file.ctime DESC
```
