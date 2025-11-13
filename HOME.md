
## Recent
``` dataview
table
file.mtime as "Edited"
from "/" and -"External"
sort file.mtime desc
limit 5
```

---

> [!box] ## Subjects
> 
> ``` dataview
> list
> from #subject and -"Templates/subject.md" and -"External"
> sort file.name
> ```