---
tags:
---
# HTML


## Последние заметки за неделю

```dataview
LIST
FROM #HTML   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

## Все заметки о MongoDB

```dataview
TABLE file.ctime as "Создана"
FROM #HTML  
SORT file.ctime DESC
```
# Без названия
