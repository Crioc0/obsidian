---
tags:
  - structure-notes
---
### Связи с другими Structure Notes
[[SQL]]
## Последние заметки за неделю
```dataview
LIST
FROM #postgresql   
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```
## Все заметки о MongoDB
```dataview
TABLE file.ctime as "Создана"
FROM #postgresql  
SORT file.ctime DESC
```
