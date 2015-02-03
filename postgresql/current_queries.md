Show current queries from psql
```sql
SELECT query FROM pg_stat_activity WHERE state='active';
```

or from bash with reload every second:

```bash
watch -n1 "echo \"SELECT query FROM pg_stat_activity WHERE state='active';\" | psql idinaidi_development"
```
