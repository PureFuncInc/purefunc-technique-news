https://cloud.tencent.com/developer/article/1705974

-- 传统limit，文件扫描
```sql
SELECT * FROM tableName ORDER BY id LIMIT 500000,2;
```

-- 子查询方式，索引扫描
```sql
SELECT 
	* 
FROM 
	tableName 
WHERE 
	id >= (SELECT id FROM tableName ORDER BY id LIMIT 500000, 1) LIMIT 2;
```

```sql
SELECT
	*
FROM 
	tableName AS t1
		JOIN (SELECT id FROM tableName ORDER BY id LIMIT 500000, 1) AS t2
WHERE
	t1.id > t2.id 
ORDER BY 
	t1.id 
LIMIT 2;
```

[[SQL]]
