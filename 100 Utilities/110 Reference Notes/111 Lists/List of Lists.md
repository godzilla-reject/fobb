```dataview
LIST

FROM #list 

where !contains(file.folder, "200 Templates")

SORT file.name ASC
```