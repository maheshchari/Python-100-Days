## MySQL相关知识

### 存储引擎

1. InnoDB
2. MyISAM

### 数据类型

### 索引

#### 索引的类型

1. B-Tree索引
2. HASH索引
3. R-Tree索引（空间索引）
4. Full-text索引（全文索引）

### 视图

查询的快照，可以将访问权限控制到列上。

```SQL
create view ... as select ...
drop view ...
```

### 存储过程

```SQL
create procedure ... (params)
begin
...
end;

call ...
```

```Python
cursor.callproc('...')
```

### 触发器

不能用，因为多个行锁可能直接升级为表锁，导致性能低下。

### 事务控制

### SQL注入攻击

### 数据分区

### SQL优化

#### 优化步骤

1. 通过`show status`了解各种SQL的执行频率。

   ```SQL
   show status like 'com_%';
   show status like 'innodb_%';
   show status like 'connections';
   show status like 'slow_queries';
   ```

2. 定位低效率的SQL语句 - 慢查询日志。

   ```SQL
   show processlist
   ```

3. 通过`explain`了解SQL的执行计划。

   - select_type：查询类型（simple、primary、union、subquery）
   - table：输出结果集的表
   - type：访问类型（ALL、index、range、ref、eq_ref、const、NULL）
   - possible_keys：查询时可能用到的索引
   - key：实际使用的索引
   - key_len：索引字段的长度
   - rows：扫描的行数
   - extra：额外信息

4. 通过`show profiles`和`show profile for query`分析SQL。

#### SQL优化

1. 优化insert语句
2. 优化order by语句
3. 优化group by语句
4. 优化嵌套查询
5. 优化or条件
6. 优化分页查询
7. 使用SQL提示
   - USE INDEX
   - IGNORE INDEX
   - FORCE INDEX

#### 配置优化

1. 调整max_connections
2. 调整back_log
3. 调整table_open_cache
4. 调整thread_cache_size
5. 调整innodb_lock_wait_timeout

#### 架构优化

1. 通过拆分提高表的访问效率
   - 垂直拆分
   - 水平拆分
2. 逆范式理论
   - 数据表设计的规范程度称之为范式（Normal Form）
     - 1NF：列不能再拆分
     - 2NF：所有的属性都依赖于主键
     - 3NF：所有的属性都直接依赖于主键（消除传递依赖）
     - BCNF：消除非平凡多值依赖
3. 使用中间表提高统计查询速度

### 数据备份

#### 导入和导出

1. select ... into outfile ...
2. load data infile ... into table ...
3. mysqldump
4. mysqlimport

#### ibbackup工具

#### xtrabackup工具

### 主从复制

### 集群

