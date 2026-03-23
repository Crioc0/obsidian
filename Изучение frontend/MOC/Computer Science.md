---
tags:
  - MOC
---
# Computer Science
### Связи с другими Structure Notes

[[]]

## Последние заметки за неделю

```dataview
LIST
FROM #база   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

## Все заметки о MongoDB

```dataview
TABLE file.ctime as "Создана"
FROM #база  
SORT file.ctime DESC
```
# Без названия
