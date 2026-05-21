---
tags:
  - MOC

---

# Moc

### Связи с другими Structure Notes

## Последние заметки за неделю

```dataview
LIST
FROM #  
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```

##

```dataview
TABLE file.ctime as "Создана"
  
SORT file.ctime DESC
```
