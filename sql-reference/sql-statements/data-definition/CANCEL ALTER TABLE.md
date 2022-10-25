# CANCEL ALTER TABLE

## 功能

该语句用于撤销一个执行中的 ALTER 操作。



## 语法

1、撤销 ALTER TABLE COLUMN 操作：

```SQL
CANCEL ALTER TABLE COLUMN
FROM [database.]table;
```

2、撤销 ALTER TABLE ROLLUP 操作：

```SQL
CANCEL ALTER TABLE ROLLUP
FROM [database.]table;
```

3、根据 `job id` 批量撤销 ROLLUP 操作：

```sql
CANCEL ALTER TABLE ROLLUP
FROM [database.]table (jobid,...);
--注意：该命令为异步操作，具体是否执行成功需要使用`show alter table rollup`查看任务状态确认。
```

> 说明：
>
> * CANCEL ALTER 命令无法撤销状态为 PENDING 的 Schema Change 任务。假设 ALTER 任务由于某些原因卡在 PENDING 状态，目前需要等待任务超时（ALTER 任务超时参数为 fe.conf `alter_table_timeout_second`，默认值为 86400 秒）。



## 示例

1、撤销针对 `example_db.table1` 的 ALTER COLUMN 操作：

```sql
CANCEL ALTER TABLE COLUMN
FROM example_db.table1;
```

2、撤销 `example_db.table2` 下的 ADD ROLLUP 操作：

```sql
CANCEL ALTER TABLE ROLLUP
FROM example_db.table2;
```

3、根据 `job id` 撤销 `example_db.table3` 下的 ADD ROLLUP 操作：

```sql
CANCEL ALTER TABLE ROLLUP
FROM example_db.table3 (12138,12333);
```

