---
tags:
  - structure-notes
---
### Связи с другими Structure Notes
[[JavaScript]]
## Последние заметки за неделю
```dataview
LIST
FROM #vue   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```
## Все заметки о MongoDB
```dataview
TABLE file.ctime as "Создана"
FROM #vue  
SORT file.ctime DESC
```
