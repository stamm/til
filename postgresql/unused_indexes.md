When postgresql query plan use index, it increment counter on idx_scan.

I find 2 queries to select the biggest unused or little used indexes:

```sql
SELECT
    schemaname || ‘.’ || relname AS table,
    indexrelname AS index,
    pg_size_pretty(pg_relation_size(i.indexrelid)) AS index_size,
    idx_scan as index_scans
FROM pg_stat_user_indexes ui
JOIN pg_index i ON ui.indexrelid = i.indexrelid
WHERE NOT indisunique AND idx_scan < 200 AND pg_relation_size(relid) > 1024 * 1024
ORDER BY pg_relation_size(i.indexrelid) / nullif(idx_scan, 0) DESC NULLS FIRST,
pg_relation_size(i.indexrelid) DESC;
```


```sql
SELECT idstat.schemaname AS schema_name,
idstat.relname AS table_name,
indexrelname AS index_name,
idstat.idx_scan AS times_used,
pg_size_pretty(pg_relation_size(idstat.relid)) AS table_size,
pg_size_pretty(pg_relation_size(indexrelid)) AS index_size,
n_tup_upd + n_tup_ins + n_tup_del as num_writes,
indexdef AS definition
FROM pg_stat_user_indexes AS idstat
JOIN pg_indexes ON indexrelname = indexname
JOIN pg_stat_user_tables AS tabstat ON idstat.relname = tabstat.relname
WHERE idstat.idx_scan < 200
AND indexdef !~* 'unique'
AND pg_relation_size(idstat.indexrelid) > 1048576
ORDER BY pg_relation_size(idstat.indexrelid) DESC;
```
