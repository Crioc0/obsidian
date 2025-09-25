---
tags:
  - structure-notes
---
### Связи с другими Structure Notes
[[MongoDB]]
## Последние заметки за неделю
```dataview
LIST
FROM #mongoose   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```
## Все заметки о MongoDB
```dataview
TABLE file.ctime as "Создана"
FROM #mongoose
SORT file.ctime DESC
```
