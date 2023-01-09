DDL
---

### 操作数据库

1.   查询

     ~~~mysql
     SHOW DATABASES;
     ~~~

2.   创建

     ~~~mysql
     CREATE DATABASES 数据库名称;
     
     -- 如果不存在则创建
     CREATE DATABASES IF NOT EXISTS 数据库名称;
     ~~~

3.   删除

     ~~~mysql
     DROP DATABASES 数据库名称;
     
     -- 如果存在则删除
     DROP DATABASES IF NOT EXISTS 数据库名称;
     ~~~

4.   使用数据库

     ~~~mysql
     -- 查看当前使用的数据库
     SELECT DATABASE();
     
     -- 使用数据库
     USE 数据库名称;
     ~~~

### 操作表

1.   查询表

     ~~~mysql
     -- 查询当前数据库下所有表名称
     SHOW TABLES;
     
     -- 查询表结构
     DESC 表名称;
     ~~~

2.   创建

     ~~~mysql
     CREATE TABLE 表名(
     	字段1	数据类型1,
         字段2	数据类型2,
         ...
         字段n	数据类型n
     );
     ~~~

3.   删除

     ~~~mysql
     DROP TABLE 表名;
     
     -- 删除表时判断是否存在
     DROP TABLE IF EXISTS 表名;
     ~~~

4.   修改

     ~~~mysql
     -- 修改表名
     ALTER TABLE 表名 RENAME TO 新的表名;
     
     -- 添加一列
     ALTER TABLE 表名 ADD 列名 数据类型;
     
     -- 修改数据类型
     ALTER TABLE 表名 MODIFY 列名 新数据类型;
     
     -- 修改列名和数据类型
     ALTER TABLE 表名 CHANGE 列名 新列名 新数据类型;
     
     -- 删除列
     ALTER TABLE 表名 DROP 列名;
     ~~~

DML
---

### 添加数据

1.   给指定列添加数据

     ~~~mysql
     INSERT INTO 表名(列名1, 列名2, ...) VALUES(值1, 值2, ...);
     ~~~

2.   给全部列添加数据

     ~~~mysql
     INSERT INTO 表名 VALUES(值1, 值2, ...);
     ~~~

3.   批量添加数据

     ~~~mysql
     INSERT INTO 表名(列名1, 列名2, ...) VALUES(值1, 值2, ...),(值1, 值2, ...), (值1, 值2, ...)...;
     INSERT INTO 表名 VALUES(值1, 值2, ...),(值1, 值2, ...),(值1, 值2, ...)...;
     ~~~

### 修改数据

1.   修改表数据

     ~~~mysql
     -- 如果不加条件，则将所有数据修改
     UPDATE 表名 SET 列名1=值1， 列名2=值2, ... [WHILE 条件];
     ~~~

### 删除数据

1.   删除数据

     ~~~mysql
     -- 如果不加条件，则将所有数据删除。
     DELETE FROM 表名 [WHERE 条件];
     ~~~

DQL
---

**查询语法**

~~~mysql
SELECT 字段列表
FROM 表名列表
WHERE 条件列表
GROUP BY 分组字段
HAVING 分组后条件
ORDER BY 排序字段
LIMIT 分页限定
~~~

### 基础查询

1.   查询多个字段

     ~~~mysql
     SELECT 字段列表 FROM 表名;
     SELECT * FROM 表名;	-- 查询所有数据
     ~~~

2.   去除重复记录

     ~~~mysql
     SELECT DISTINCT 字段列表 FROM 表名;
     ~~~

3.   起别名

     ~~~mysql
     AS: -- AS也可以省略;
     ~~~

### 条件查询(WHERE)

1.   语法

     ~~~mysql
     SELECT 字段列表 FROM 表名 WHERE 条件列表;
     ~~~

2.   条件 

     ~~~mysql
     <>或!=	-- 不等于
     BETWEEN ... AND ...	-- 在某个范围内（都包括）
     IN(...)			-- 多选一
     LIKE 占位符		-- 模糊查询：_单个字符查询 %多个任意字符
     IS NULL		-- 是NULL
     IS NOT NULL	-- 不是NULL
     AND 或 &&	-- 并且
     OR 或 ||		-- 或者
     NOT 或 !		-- 非，不是
     ~~~


### 分组查询(GROUP BY)

*   聚合函数

*   将一列数据作为一个整体，进行纵向计算。

*   分类

    |   函数名    |              功能              |
    | :---------: | :----------------------------: |
    | count(列名) | 统计数量(一般选用不为null的列) |
    |  max(列名)  |             最大值             |
    |  min(列名)  |             最小值             |
    |  sum(列名)  |              求和              |
    |  avg(列名)  |             平均值             |

*   语法

    ~~~mysql
    -- NULL不参与聚合函数运算
    SELECT 聚合函数(列名) FROM 表;
    
    SELECT 字段列表 FROM 表名 [WHERE 分组前条件限定] GROUP BY 分组字段名 [HAVING 分组后条件过滤];
    -- 执行时间：WHERE是分组之前进行限定，HAVING是分组之后
    -- 可判断条件：WHERE不能对聚合函数进行判断,HAVING可以
    -- 执行顺序：WHERE > 聚合函数 > HAVING
    ~~~

    

### 排序查询(ORDER BY)

1.   语法

     ~~~mysql
     // 多个排序条件时，前面条件值一样才会进行第二条排序
     SELECT 字段列表 FROM 表名 ORDER BY 排序字段1 [排序方式1], 排序字段2 [排序方式2]...;
     ASC: 升序（默认）
     DESC: 降序
     ~~~

### 分页查询(LIMIT)

1.   语法

     ~~~mysql
     -- 起始索引 = (当前页码 - 1) * 每页显示的条数 
     SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询条目数;
     ~~~



约束
---

### 约束概念和分类

1.   概念

     *   约束是作用于表中列上的规则，用于限制加入表的数据。
     *   约束的存在保证了数据库中数据的正确性、有效性、和完整性。

2.   分类

     | 约束名称 |                       描述                       |   关键字    |
     | :------: | :----------------------------------------------: | :---------: |
     | 非空约束 |           保证列中所有数据不能有null值           |  NOT NULL   |
     | 唯一约束 |             保证列中所有数据各不相同             |   UNIQUE    |
     | 主键约束 |             唯一标识，要求非空且唯一             | PRIMARY KEY |
     | 检查约束 |             保证列中的值满足某一条件             |    CHECK    |
     | 默认约束 |         保存数据时，未指定值则采用默认值         |   DEFAULT   |
     | 外键约束 | 用来让两个表数据建立连接，保证数据一致性和完整性 | FOREIGN KEY |

### 外键约束

1.   添加约束

     ~~~mysql
     -- 创建表时添加外键约束
     CREATE TABLE 表名(
     	列名 数据类型,
         ...
         [CONSTRAINT] [外键名称] FOREIGN KEY(外键列名) REFERENCES 主表(主表列名)
     );
     
     -- 创建完表后添加外键约束
     ALTER TABLE ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名称) REFERENCES 主表名称(主表列名);
     ~~~

2.   删除约束

     ~~~mysql
     ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
     ~~~



## 多表查询

### 连接查询

#### 内连接

*   查询A、B表交集数据

*   隐式内连接

    ~~~mysql
    SELECT 字段列表 FROM 表1, 表2... WHERE 条件;
    ~~~

*   显式内连接

    ~~~mysql
    SELECT 字段列表 FROM 表1[INNER] JOIN 表2 ON 条件;
    ~~~

#### 外连接

*   左外连接：查询A表所有数据和交集部分数据

    ~~~mysql
    SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件;
    ~~~

*   右外连接：查询B表所有数据和交集部分数据

    ~~~mysql
    SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件;
    ~~~

### 子查询

*   单行单列：作为条件值，使用= != > < 等进行条件判断

    ~~~mysql
    SELECT 字段列表 FROM 表 WHERE 字段名 = (子查询);
    ~~~

*   多行单列：作为条件值，使用in等关键字进行条件判断

    ~~~mysql
    SELECT 字段列表 FROM 表 WHERE 字段名 in (子查询);
    ~~~

*   多行多列：作为虚拟表

    ~~~mysql
    SELECT 字段列表 FROM (子查询) WHERE 条件;
    ~~~

## 事务

### 四大特征

1.   原子性：事务是不可分割的最小操作单位，要么同时成功，要么同时失败
2.   一致性：事务完成时，必须使所有数据都保持一致状态
3.   隔离性：多个事务之间，操作的可见性
4.   持久性：事务一旦提交或回滚，它对数据库中的操作的改变就是永久的
