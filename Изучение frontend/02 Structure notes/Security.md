---
tags:
  - предмет
---
### Связи с другими Structure Notes

[[Computer Science]]

## Последние заметки за неделю

```dataview
LIST
FROM #security   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

## Все заметки о MongoDB

```dataview
TABLE file.ctime as "Создана"
FROM #security  
SORT file.ctime DESC
```
