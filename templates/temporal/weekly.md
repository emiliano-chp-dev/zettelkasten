```dataview
TABLE created, due, completed
FROM "tasks/daily"
WHERE completed AND file.ctime >= this.week-start AND file.ctime <= this.week-end
```

