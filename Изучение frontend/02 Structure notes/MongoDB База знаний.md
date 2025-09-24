#mongodb 

# Карта знаний: [[202509231654 Что такое MongoDB|MongoDB]] 

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

###### Ссылки
```dataview
LIST file.link
FROM #mongodb
SORT file.ctime DESC
```
