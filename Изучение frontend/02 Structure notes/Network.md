---
tags:
  - structure-notes
---
### Связи с другими Structure Notes

[[Computer Science]]

## Подразделы

```dataview
LIST
FROM #network AND #substructure  
SORT file.ctime DESC
```

## Последние заметки за неделю

```dataview
LIST
FROM #network  
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

## Все заметки о MongoDB

```dataview
TABLE file.ctime as "Создана"
FROM #network 
SORT file.ctime DESC
```
