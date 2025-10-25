---
tags:
  - уровень_1
---
### Связи с другими Structure Notes

## Последние заметки за неделю

```dataview
LIST
FROM #sql   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

## Все заметки о MongoDB

```dataview
TABLE file.ctime as "Создана"
FROM #sql 
SORT file.ctime DESC
```
