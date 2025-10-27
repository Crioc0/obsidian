---
tags:
  - уровень_0
  - nestjs
---
### Связи с другими Structure Notes

## Последние заметки за неделю

```dataview
LIST
FROM #nestjs   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

## Все заметки о MongoDB

```dataview
TABLE file.ctime as "Создана"
FROM #nestjs  
SORT file.ctime DESC
```
