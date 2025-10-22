---
tags:
  - structure-notes
---
### Связи с другими Structure Notes

[[SQL]] [[Database]] [[Network]]

## Подразделы

```dataview
LIST
FROM #computerScience  AND #substructure  
SORT file.ctime DESC
```

## Последние заметки за неделю

```dataview
LIST
FROM #computerScience  
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

## Все заметки о ComputerScience

```dataview
TABLE file.ctime as "Заметки"
FROM #ComputerScience 
SORT file.ctime DESC
```
