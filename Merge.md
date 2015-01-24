
### 方式1
```sql
MERGE INTO target AS t
USING (SELECT @Key1 AS Key1, @Kye2 AS Key2, @Col3 AS Col3, @Col4 AS Col4, @Col5 AS Col5) AS s
ON (t.Key1 = s.Key1 AND t.Key2 = s.Key2)
WHEN MATCHED THEN
  UPDATE SET Col3 = s.Col3, Col4 = s.Col4, Col5 = s.Col5
WHEN NOT MATCHED BY TARGET THEN
  INSERT (Key1, Key2, Col3, Col4, Col5) VALUES (s.Key1, s.Key2, s.Col3, s.Col4, s.Col5)
WHEN NOT MATCHED BY SOURCE AND s.Key1 = @Key1 THEN
  DELETE;
```


### 方式2
```csharp
conn.Merge(mergeSql, sourceSql, new { source });
```

```sql
-- mergeSql
MERGE INTO target AS t
USING @source AS s
ON (t.Key1 = s.Key1 AND t.Key2 = s.Key2)
WHEN MATCHED THEN
  UPDATE SET Col3 = s.Col3, Col4 = s.Col4, Col5 = s.Col5
WHEN NOT MATCHED BY TARGET THEN
  INSERT (Key1, Key2, Col3, Col4, Col5) VALUES (s.Key1, s.Key2, s.Col3, s.Col4, s.Col5)
WHEN NOT MATCHED BY SOURCE AND s.Key1 = 'CommonKey' THEN
  DELETE;

-- sourceSql
INSERT INTO @source VALUES (@Key1, @Key2, @Col3, @Col4, @Col5);
```

```sql
--sql1
DECLARE @source table()
  Key1 nvarchar(max),
  Key2 int NOT NULL,
  Col3 nvarchar(max),
  Col4 smallint NOT NULL,
  Col5 tinyint NOT NULL);

--sql2 xN
INSERT INTO @source VALUES (@Key1, @Key2, @Col3, @Col4, @Col5);

--sql3
MERGE INTO target AS t
USING @source AS s
ON (t.Key1 = s.Key1 AND t.Key2 = s.Key2)
WHEN MATCHED THEN
  UPDATE SET Col3 = s.Col3, Col4 = s.Col4, Col5 = s.Col5
WHEN NOT MATCHED BY TARGET THEN
  INSERT (Key1, Key2, Col3, Col4, Col5) VALUES (s.Key1, s.Key2, s.Col3, s.Col4, s.Col5)
WHEN NOT MATCHED BY SOURCE AND s.Key1 = 'CommonKey' THEN
  DELETE;
```
