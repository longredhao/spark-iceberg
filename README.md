Apache Spark with Iceberg
=========================


### Sample Queries:
```
CREATE TABLE local.db.table (id bigint, data string) USING iceberg;
INSERT INTO local.db.table VALUES (1, 'a'), (2, 'b'), (3, 'c');
SELECT count(1) as count, data FROM local.db.table GROUP BY data;

DESCRIBE NAMESPACE default;
DESCRIBE TABLE local.db.table;

SELECT * FROM local.db.table.snapshots;

```

### TABLE PARTITIONED BY category 
```
CREATE TABLE local.db.sample (
    id bigint,
    data string,
    category string)
USING iceberg
PARTITIONED BY (category)
```

### TABLE PARTITIONED BY buckets
```
CREATE TABLE local.db.sample (
    id bigint,
    data string,
    category string,
    ts timestamp)
USING iceberg
PARTITIONED BY (bucket(16, id), days(ts), category)
```

### ALTER TABLE ... WRITE ORDERED BY¶ 
```
ALTER TABLE local.db.sample WRITE ORDERED BY category, id

-- use optional ASC/DEC keyword to specify sort order of each field (default ASC)
ALTER TABLE local.db.sample WRITE ORDERED BY category ASC, id DESC

-- use optional NULLS FIRST/NULLS LAST keyword to specify null order of each field (default FIRST)
ALTER TABLE local.db.sample WRITE ORDERED BY category ASC NULLS LAST, id DESC NULLS FIRST
```


### Reference:
* [https://iceberg.apache.org/getting-started/](https://iceberg.apache.org/getting-started/)
* [https://iceberg.apache.org/spark/](https://iceberg.apache.org/spark/)

