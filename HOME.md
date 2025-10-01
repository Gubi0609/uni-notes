
## Recent
``` dataview
table
file.mtime as "Edited"
from "/"
sort file.mtime desc
limit 5
```

---

> [!box] ## Subjects
> 
> ``` dataview
> list
> from #subject and -"Templates/subject.md"
> sort file.name
> ```