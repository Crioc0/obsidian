#section

## Последние заметки за неделю
```dataview
LIST
FROM #mongodb 
WHERE file.ctime >= date(now) - dur(7 days)
SORT file.ctime DESC
```




## Все заметки о MongoDB
```dataview
TABLE file.ctime as "Создана"
FROM #mongodb 
SORT file.ctime DESC
```



