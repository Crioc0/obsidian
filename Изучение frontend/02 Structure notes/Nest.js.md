---
tags:
  - structure-notes
---
### Связи с другими Structure Notes
[[Zettlecasten/Express|Express]] [[02 Structure notes/NodeJS|NodeJS]]
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
FROM # 
SORT file.ctime DESC
```
