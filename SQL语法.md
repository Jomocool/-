# SQL语法

[SQL 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/sql/sql-tutorial.html)

## 一、SQL教程

### 1. SQL简介

**SQL**(Structuted Query Language:结构化查询语言)是用于管理关系数据库管理系统（RDBMS）的标准的计算机语言。SQL的范围包括数据插入、查询、更新和删除，数据库模式创建和修改，以及数据访问控制。

**要创建一个显示数据库中数据的网站，需要：**

- RDBMS数据库程序（比如MS Access、SQL Server、MySQL）
- 是用服务器端脚本语言，比如PHP或ASP
- 使用SQL来获取想要的数据
- 使用HTML/CSS

**RDBMS：**

- RDBMS 指关系型数据库管理系统，全称 Relational Database Management System。

- RDBMS 是 SQL 的基础，同样也是所有现代数据库系统的基础，比如 MS SQL Server、IBM DB2、Oracle、MySQL 以及 Microsoft Access。

- RDBMS 中的数据存储在被称为表的数据库对象中。

- 表是相关的数据项的集合，它由列和行组成。



### 2. SQL语法

一个数据库通常包含一个或多个表。每个表中有一个名字标识，表中包含带有数据的记录（行）

```sql
mysql> use RUNOOB;#选择RUNOOB数据库
Database changed

mysql> set names utf8;#设置使用UTF8字符集
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT * FROM Websites;#读取数据表的所有信息
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
| 1  | Google       | https://www.google.cm/    | 1     | USA     |
| 2  | 淘宝          | https://www.taobao.com/   | 13    | CN      |
| 3  | 菜鸟教程      | http://www.runoob.com/    | 4689  | CN      |
| 4  | 微博          | http://weibo.com/         | 20    | CN      |
| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
+----+--------------+---------------------------+-------+---------+
5 rows in set (0.01 sec)
```

SQL对大小写不敏感：SELECT与select相同



**一些最重要的SQL命令：**

- SELECT-从数据库中提取数据
- UPDATE-更新数据库中的数据
- DELETE-从数据库中删除数据
- INSERT INTO-向数据库中插入新数据
- CREATE DATABASE-创建新数据库
- ALTER DATABASE-修改数据库
- CREATE TABLE-创建新表
- ALTER TABLE-变更数据库表
- DROP TABLE-删除表
- CREATE INDEX-创建索引（搜索键）
- DROP INDEX-删除索引



### 3. SQL SELECT语句

SELECT语句用于从数据库中选取数据

SELECT语句用于从数据库中选取数据。

结果被存储在一个结果表中，称为结果集

![](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522000515756.png)

```sql
SELECT cloumn1,column2,... FROM table_name;#选择多个字段
SELECT * from table_name;#选择所有字段

#输出
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)
```



### 4. SQL SELECT DISTINCT语句

在表中，一个列可能会包含多个重复值，SQL SELECT DISTINCT语句用于返回唯一不同的值

![](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522000515756.png)

```sql
SELECT DISTINCT country FROM Websites;

#输出
+---------+
| country |
+---------+
| USA     |
| CN      |
+---------+
2 rows in set (0.00 sec)
```



### 5. SQL WHERE子句

WHERE语句用于提取满足指定条件的记录，相当于if



**SQL WHERE 语法**

```sql
SELECT column1,column2,... FROM table_name WHERE condition
```



**WHERE子句示例**

![](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522000515756.png)

```sql
mysql> SELECT * FROM Websites WHERE country='CN';
+------+--------------+-------------------------+-------+---------+
| id   | name         | url                     | alexa | country |
+------+--------------+-------------------------+-------+---------+
|    2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/  |  4689 | CN      |
|    4 | 微博         | http://weibo.com/       |    20 | CN      |
+------+--------------+-------------------------+-------+---------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM Websites WHERE id=1;
+------+--------+------------------------+-------+---------+
| id   | name   | url                    | alexa | country |
+------+--------+------------------------+-------+---------+
|    1 | Google | https://www.google.cm/ |     1 | USA     |
+------+--------+------------------------+-------+---------+
1 row in set (0.00 sec)
```



**文本字段 vs 数值字段**

SQL使用单引号来环绕文本值（大部分数据系统也接受双引号）
如果是数值字段，不要使用引号



**WHERE子句中的运算符**

![image-20230522103118080](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522103118080.png)



### 6. SQL AND & OR 运算符

AND & OR运算符用于基于一个以上的条件对记录进行过滤



**示例**

![](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522000515756.png)

```sql
mysql> SELECT * FROM Websites WHERE country='CN' AND alexa > 50;
+------+--------------+------------------------+-------+---------+
| id   | name         | url                    | alexa | country |
+------+--------------+------------------------+-------+---------+
|    3 | 菜鸟教程     | http://www.runoob.com/ |  4689 | CN      |
+------+--------------+------------------------+-------+---------+
1 row in set (0.00 sec)

mysql> SELECT * FROM Websites WHERE country='CN' OR country='USA';
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM Websites WHERE alexa>15 AND (country='CN' OR country='USA');
+------+--------------+------------------------+-------+---------+
| id   | name         | url                    | alexa | country |
+------+--------------+------------------------+-------+---------+
|    3 | 菜鸟教程     | http://www.runoob.com/ |  4689 | CN      |
|    4 | 微博         | http://weibo.com/      |    20 | CN      |
+------+--------------+------------------------+-------+---------+
2 rows in set (0.00 sec)
```



### 7. SQL ORDER BY 关键字

ORDER BY关键字用于对结果集按照一个列或者多个列进行排序

ORDER BY关键字默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，可以使用DESC关键字



**SQL ORDER BY语法**

```sql
SELECT column1,column2,... 
FROM table_name 
ORDER BY column1,column2,... ASC|DESC;
```



**示例**

![](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522000515756.png)

```sql
#下面的 SQL 语句从 "Websites" 表中选取所有网站，并按照 "alexa" 列排序：
mysql> SELECT * FROM Websites ORDER BY alexa;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)

#下面的 SQL 语句从 "Websites" 表中选取所有网站，并按照 "alexa" 列降序排序：
mysql> SELECT * FROM Websites ORDER BY alexa DESC;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)

#下面的 SQL 语句从 "Websites" 表中选取所有网站，并按照 "country" 和 "alexa" 列排序：
mysql> SELECT * FROM Websites ORDER BY alexa,country;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)
```



### 8. SQL INSERT INTO语句

INSERT INTO语句用于向表中插入新纪录



**SQL INSERT INTO语法**

```sql
#第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：
INSET INTO table_name VALUES (value1,value2,value3,...);
#第二种形式需要指定列名及被插入的值：
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```



**示例**

![](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522000515756.png)

```sql
#假设我们要向 "Websites" 表中插入一个新行。我们可以使用下面的 SQL 语句：
---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
| NULL | 百度         | https://www.baidu.com/    |     4 | CN      |
+------+--------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)
#因为没有指定ID，所以是NULL
```



### 9. SQL UPDATE语句

UPDATE语句用于更新表中已存在的记录



**SQL UPDATE语法**

```sql
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE condition;
```



**示例**

![image-20230522131859352](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522131859352.png)

```sql
#把百度的id改为6
mysql> use mysql_runoob
Database changed
mysql> UPDATE Websites SET id=6 WHERE name='百度';
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM Websites;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|    6 | 百度         | https://www.baidu.com/    |     4 | CN      |
+------+--------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

#假设我们要把 "菜鸟教程" 的 alexa 排名更新为 5000，country 改为 USA。我们使用下面的 SQL 语句：
mysql> UPDATE Websites SET alexa=5000,country='USA' WHERE name='菜鸟教程';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM Websites;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|    6 | 百度         | https://www.baidu.com/    |     4 | CN      |
+------+--------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

#在更新记录时要十分小心，如果少了WHERE子句，将会修改表中所有数据
```



### 10. SQL DELETE语句

DELETE语句用于删除表中的行



**SQL DELETE语法**

```sql
DELETE FROM table_name WHERE condition;
```

注意WHERE子句，如果省略了，所有记录都会被删掉



**示例**

![](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230522000515756.png)

```sql
#假设我们要从 "Websites" 表中删除网站名为 "Facebook" 且国家为 USA 的网站。我们使用下面的 SQL 语句：
mysql> DELETE FROM Websites WHERE name='Facebook' AND country='USA';
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM Websites;
+------+--------------+-------------------------+-------+---------+
| id   | name         | url                     | alexa | country |
+------+--------------+-------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/  |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|    4 | 微博         | http://weibo.com/       |    20 | CN      |
+------+--------------+-------------------------+-------+---------+
4 rows in set (0.00 sec)

#在不删除标的情况下，删除表中所有的行，意味着表结构、属性、索引将保持不变
mysql> DELETE FROM Websites;
Query OK, 4 rows affected (0.01 sec)

mysql> SELECT * FROM Websites;
Empty set (0.00 sec)
```

