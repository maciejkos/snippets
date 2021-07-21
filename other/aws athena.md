1. Get all distinct values of a partitioning field sorted
```sql
SELECT distinct partition_value
FROM information_schema.__internal_partitions__
WHERE table_schema = 'my_table_schema'
        AND table_name = 'my_table_name'
        AND partition_key = 'my_specific_key'
ORDER BY partition_value
```