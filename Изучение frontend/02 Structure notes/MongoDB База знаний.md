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

```dataviewjs
const notes = dv.pages('#mongodb').sort(p => p.file.ctime, 'desc');

// Создаем реальные ссылки в содержании заметки
dv.paragraph("**Все заметки MongoDB:**");
for (let note of notes) {
    dv.paragraph(`- [[${note.file.name}]]`);
}
```

###### Ссылки
```dataview
LIST "[[" + file.name + "]]"
FROM #mongodb
SORT file.ctime DESC
```
