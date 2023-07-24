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
INSERT INTO Websites VALUES(NULL,'百度','https://www.baidu.com/',4,'CN');
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



## 二、SQL高级教程

### 1. SQL SELECT TOP, LIMIT, ROWNUM 子句

**SQL SELECT TOP 子句**

SELECT TOP子句用于规定要返回的记录的数目

SELECT TOP子句对于拥有数千条记录的大型表来说，是非常有用的

> **注意:**并非所有的数据库系统都支持 SELECT TOP 语句。 MySQL 支持 LIMIT 语句来选取指定的条数数据， Oracle 可以使用 ROWNUM 来选取。

**SQL Server / MS Access 语法**

```sql
SELECT TOP number|percent column_name(s)
FROM table_name;
```

**MySQL 语法**

```sql
SELECT column_name(s)
FROM table_name
LIMIT number;
```

**Oracle 语法**

```sql
SELECT column_name(s)
FROM table_name
WHERE ROWNUM<=number;
```

**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)
```

**MySQL SELECT LIMIT实例**

```sql
#展示Websites表的前两行
mysql> SELECT * FROM Websites LIMIT 2;
+------+--------+-------------------------+-------+---------+
| id   | name   | url                     | alexa | country |
+------+--------+-------------------------+-------+---------+
|    1 | Google | https://www.google.cm/  |     1 | USA     |
|    2 | 淘宝   | https://www.taobao.com/ |    13 | CN      |
+------+--------+-------------------------+-------+---------+
2 rows in set (0.00 sec)
```



### 2. SQL LIKE 操作符

LIKE操作符用于在WHERE子句中搜索列中的指定模式

**SQL LIKE 操作符**

```sql
SELECT column1,column2,...
FROM table_name
WHERE column LIKE pattern;

#参数说明：
#column1,column2,...：选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段
#table_name：要查询的表名称
#column：要搜索的字段名称
#pattern：搜索模式
```

**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)
```

**SQL LIKE 操作符实例**

```sql
#选取name以'G'开始的所有客户
mysql> SELECT * FROM Websites WHERE name LIKE 'G%';
+------+--------+------------------------+-------+---------+
| id   | name   | url                    | alexa | country |
+------+--------+------------------------+-------+---------+
|    1 | Google | https://www.google.cm/ |     1 | USA     |
+------+--------+------------------------+-------+---------+
1 row in set (0.00 sec)

#选取name以字母'k'结尾的所有客户
mysql> SELECT * FROM Websites WHERE name LIKE '%k';
+------+----------+---------------------------+-------+---------+
| id   | name     | url                       | alexa | country |
+------+----------+---------------------------+-------+---------+
|    5 | Facebook | https://www.facebook.com/ |     3 | USA     |
+------+----------+---------------------------+-------+---------+
1 row in set (0.00 sec)

#选取name包含模式'oo'的所有客户
mysql> SELECT * FROM Websites WHERE name LIKE '%oo%';
+------+----------+---------------------------+-------+---------+
| id   | name     | url                       | alexa | country |
+------+----------+---------------------------+-------+---------+
|    1 | Google   | https://www.google.cm/    |     1 | USA     |
|    5 | Facebook | https://www.facebook.com/ |     3 | USA     |
+------+----------+---------------------------+-------+---------+
2 rows in set (0.00 sec)

#选取name不包含模式'oo'的所有客户
mysql> SELECT * FROM Websites WHERE name NOT LIKE '%oo%';
+------+--------------+-------------------------+-------+---------+
| id   | name         | url                     | alexa | country |
+------+--------------+-------------------------+-------+---------+
|    2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|    4 | 微博         | http://weibo.com/       |    20 | CN      |
+------+--------------+-------------------------+-------+---------+
3 rows in set (0.00 sec)
```

> **提示：**'%'符号用于在模式的前后定义通配符（默认字母）



### 3. SQL 通配符

通配符可用于替代字符串中的任何其他字符



**SQL 通配符**

在SQL中，通配符与SQL LIKE操作符一起使用

SQL通配符用于搜索表中的数据

在SQL中，可以使用以下通配符：

| **通配符**               | **描述**                   |
| :----------------------- | -------------------------- |
| %                        | 替代0个或多个字符          |
| _                        | 替代一个字符               |
| [charlist]               | 字符列中的任何单一字符     |
| [^charlist]或[!charlist] | 不在字符列中的任何单一字符 |



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)
```



**使用 SQL % 通配符**

```sql
#选取url以'https'开始的所有网站
mysql> SELECT * FROM Websites WHERE url LIKE 'https%';
+------+----------+---------------------------+-------+---------+
| id   | name     | url                       | alexa | country |
+------+----------+---------------------------+-------+---------+
|    1 | Google   | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝     | https://www.taobao.com/   |    13 | CN      |
|    5 | Facebook | https://www.facebook.com/ |     3 | USA     |
+------+----------+---------------------------+-------+---------+
3 rows in set (0.04 sec)

#选取url包含模式'oo'的所有网站
mysql> SELECT * FROM Websites WHERE url LIKE '%oo%';
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
3 rows in set (0.00 sec)


```



**使用 SQL _ 通配符**

```sql
#选取name以一个任意字符开始，然后是'oogle'的所有客户
mysql> SELECT * FROM Websites WHERE name LIKE '_oogle';
+------+--------+------------------------+-------+---------+
| id   | name   | url                    | alexa | country |
+------+--------+------------------------+-------+---------+
|    1 | Google | https://www.google.cm/ |     1 | USA     |
+------+--------+------------------------+-------+---------+
1 row in set (0.00 sec)

#选取name以'G'开始，然后是一个任意字符，然后是'o'，然后是一个任意字符，然后是'le'的所有网站
mysql> SELECT * FROM Websites WHERE name LIKE 'G_o_le';
+------+--------+------------------------+-------+---------+
| id   | name   | url                    | alexa | country |
+------+--------+------------------------+-------+---------+
|    1 | Google | https://www.google.cm/ |     1 | USA     |
+------+--------+------------------------+-------+---------+
1 row in set (0.00 sec)
```



**使用 SQL [charlist] 通配符**

MySQL中使用REGEXP或NOT REGEXP运算符（或RLIKE 和 NOT RLIKE）来操作正则表达式

```sql
#选取name以'G'、‘F'或's'开始的所有网站
mysql> SELECT * FROM Websites WHERE name REGEXP '[GFs]';
+------+----------+---------------------------+-------+---------+
| id   | name     | url                       | alexa | country |
+------+----------+---------------------------+-------+---------+
|    1 | Google   | https://www.google.cm/    |     1 | USA     |
|    5 | Facebook | https://www.facebook.com/ |     3 | USA     |
+------+----------+---------------------------+-------+---------+
2 rows in set (0.01 sec)

#选取name以A到H字母开头的网站
mysql> SELECT * FROM Websites WHERE name REGEXP '[A-Z]';
+------+----------+---------------------------+-------+---------+
| id   | name     | url                       | alexa | country |
+------+----------+---------------------------+-------+---------+
|    1 | Google   | https://www.google.cm/    |     1 | USA     |
|    5 | Facebook | https://www.facebook.com/ |     3 | USA     |
+------+----------+---------------------------+-------+---------+
2 rows in set (0.00 sec)

#选取name不以A到H字母开头的网站
mysql> SELECT * FROM Websites WHERE name REGEXP '[^A-Z]';
+------+--------------+-------------------------+-------+---------+
| id   | name         | url                     | alexa | country |
+------+--------------+-------------------------+-------+---------+
|    2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|    4 | 微博         | http://weibo.com/       |    20 | CN      |
+------+--------------+-------------------------+-------+---------+
3 rows in set (0.00 sec)
```



### 4. SQL IN 操作符

**IN 操作符**

IN操作符允许在WHERE子句中规定多个值



**SQL IN 语法**

```sql
SELECT column1,column2,...
FROM table_name
WHERE column IN(value1,value2,...);
```

参数说明：

- **column1, column2, ...**：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- **table_name**：要查询的表名称。
- **column**：要查询的字段名称。
- **value1, value2, ...**：要查询的值，可以为多个值。



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)
```



**IN 操作符实例**

```sql
#选取name为'Google'或'菜鸟教程'的所有网站
mysql> SELECT * FROM Websites WHERE name IN('Google','菜鸟教程');
+------+--------------+------------------------+-------+---------+
| id   | name         | url                    | alexa | country |
+------+--------------+------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/ |     1 | USA     |
|    3 | 菜鸟教程     | http://www.runoob.com/ |  5000 | USA     |
+------+--------------+------------------------+-------+---------+
2 rows in set (0.03 sec)
```



### 5. SQL BETWEEN 操作符

BETWEEN操作符用于选取介于两个值之间的数据范围内的值



**SQL BETWEEN 操作符**

BETWEEN操作符选取介于两个值之间的数据范围内的值，这些值可以是数值、文本或者日期



**SQL BETWEEN 语法**

```sql
SELECT column1,column2,...
FROM table_name
WHERE column BETWEEN value1 AND value2;
```

参数说明：

- column1, column2, ...：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- table_name：要查询的表名称。
- column：要查询的字段名称。
- value1：范围的起始值。
- value2：范围的结束值。



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)
```



**BETWEEN 操作符实例**

```sql
#选择alexa介于1和20之间的所有网站
mysql> SELECT * FROM Websites WHERE alexa BETWEEN 1 AND 20;
+------+----------+---------------------------+-------+---------+
| id   | name     | url                       | alexa | country |
+------+----------+---------------------------+-------+---------+
|    1 | Google   | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝     | https://www.taobao.com/   |    13 | CN      |
|    4 | 微博     | http://weibo.com/         |    20 | CN      |
|    5 | Facebook | https://www.facebook.com/ |     3 | USA     |
+------+----------+---------------------------+-------+---------+
4 rows in set (0.00 sec)
```



**NOT BETWEEN 操作符实例**

```sql
#选取alexa不在1和20之间的所有网站
mysql> SELECT * FROM Websites WHERE alexa NOT BETWEEN 1 AND 20;
+------+--------------+------------------------+-------+---------+
| id   | name         | url                    | alexa | country |
+------+--------------+------------------------+-------+---------+
|    3 | 菜鸟教程     | http://www.runoob.com/ |  5000 | USA     |
+------+--------------+------------------------+-------+---------+
1 row in set (0.00 sec)
```



**带有 IN 的 BETWEEN 操作符实例**

```sql
#选取alexa介于1和20之间但country不为USA和IND的所有网站
mysql> SELECT * FROM Websites WHERE (alexa BETWEEN 1 AND 20) AND (country NOT IN ('USA','IND'));
+------+--------+-------------------------+-------+---------+
| id   | name   | url                     | alexa | country |
+------+--------+-------------------------+-------+---------+
|    2 | 淘宝   | https://www.taobao.com/ |    13 | CN      |
|    4 | 微博   | http://weibo.com/       |    20 | CN      |
+------+--------+-------------------------+-------+---------+
2 rows in set (0.00 sec)
```

**带有文本值的 BETWEEN 操作符实例**

```sql
#选取name以介于'A'和'H'之间字母开始的所有网站
mysql> SELECT * FROM Websites WHERE name BETWEEN 'A' AND 'H';
+------+----------+---------------------------+-------+---------+
| id   | name     | url                       | alexa | country |
+------+----------+---------------------------+-------+---------+
|    1 | Google   | https://www.google.cm/    |     1 | USA     |
|    5 | Facebook | https://www.facebook.com/ |     3 | USA     |
+------+----------+---------------------------+-------+---------+
2 rows in set (0.00 sec)
```



**带有文本值的 NOT BETWEEN 操作符实例**

```sql
#选取name不介于'A'和'H'之间字母开始的所有网站
mysql> SELECT * FROM Websites WHERE name NOT BETWEEN 'A' AND 'H';
+------+--------------+-------------------------+-------+---------+
| id   | name         | url                     | alexa | country |
+------+--------------+-------------------------+-------+---------+
|    2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|    4 | 微博         | http://weibo.com/       |    20 | CN      |
+------+--------------+-------------------------+-------+---------+
3 rows in set (0.00 sec)
```

![image-20230713152244851](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230713152244851.png)





### 6. SQL 别名

通过使用SQL，可以为表名称或列名称指定别名



**SQL 别名**

创建别名是为了让列名称的可读性更强



**列的 SQL 别名语法**

```sql
SELECT column_name AS alias_name
FROM table_name;
```



**表的 SQL 别名语法**

```sql
SELECT column_name(s)
FROM table_name AS alias_name;
```



**演示数据库**

**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+--------------+---------------------------+-------+---------+
| id   | name         | url                       | alexa | country |
+------+--------------+---------------------------+-------+---------+
|    1 | Google       | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博         | http://weibo.com/         |    20 | CN      |
|    5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+------+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)
```



**列的别名实例**

```sql
#指定两个别名，一个是name列的别名，一个是country列的别名
#提示：如果列名称包含空格，要求使用双引号或方括号
mysql> SELECT name AS n,country AS c FROM Websites;
+--------------+------+
| n            | c    |
+--------------+------+
| Google       | USA  |
| 淘宝         | CN   |
| 菜鸟教程     | USA  |
| 微博         | CN   |
| Facebook     | USA  |
+--------------+------+
5 rows in set (0.00 sec)

#把三个列（url、alexa和country）结合在一起，并创建一个名为'site_info‘的别名，列之间用','隔开
mysql> SELECT name, CONCAT(url,',',alexa,',',country) AS site_info FROM Websites;
+--------------+---------------------------------+
| name         | site_info                       |
+--------------+---------------------------------+
| Google       | https://www.google.cm/,1,USA    |
| 淘宝         | https://www.taobao.com/,13,CN   |
| 菜鸟教程     | http://www.runoob.com/,5000,USA |
| 微博         | http://weibo.com/,20,CN         |
| Facebook     | https://www.facebook.com/,3,USA |
+--------------+---------------------------------+
5 rows in set (0.00 sec)
```



**表的别名实例**

```sql
#指定Websites为w，并显示name和url列，同时指定这两列的别名
mysql> SELECT w.name AS n,w.url AS u FROM Websites AS w;
+--------------+---------------------------+
| n            | u                         |
+--------------+---------------------------+
| Google       | https://www.google.cm/    |
| 淘宝         | https://www.taobao.com/   |
| 菜鸟教程     | http://www.runoob.com/    |
| 微博         | http://weibo.com/         |
| Facebook     | https://www.facebook.com/ |
+--------------+---------------------------+
5 rows in set (0.00 sec)
```

在下面的情况下，使用别名很有用：

- 在查询中涉及超过一个表
- 在查询中使用了函数
- 列名称很长或者可读性差
- 需要把两个列或者多个列结合在一起



### 7. SQL 连接(JOIN)

SQL join用于把来自两个或多个表的行结合起来

![image-20230713182433021](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230713182433021.png)



**SQL JOIN**

SQL JOIN子句用于把来自两个或多个表的行结合起来，基于这些表之间的共同字段

最常见的JOIN类型：SQL INNER JOIN（简单的JOIN）。SQL INNER JOIN从多个表中返回满足JOIN条件的所有行

**语法：**

```sql
SELECT column1,column2,...
FROM table1
JOIN table2 ON condition;
```

**参数说明：**

- **column1, column2, ...**：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- **table1**：要连接的第一个表。
- **table2**：要连接的第二个表。
- **condition**：连接条件，用于指定连接方式。



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+------+---------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM access_log;
+------+---------+-------+------------+
| aid  | site_id | count | date       |
+------+---------+-------+------------+
|    1 |       1 |    45 | 2016-05-10 |
|    2 |       3 |   100 | 2016-05-13 |
|    3 |       1 |   230 | 2016-05-14 |
|    4 |       2 |    10 | 2016-05-14 |
|    5 |       5 |   205 | 2016-05-14 |
|    6 |       4 |    13 | 2016-05-15 |
|    7 |       3 |   220 | 2016-05-15 |
|    8 |       5 |   545 | 2016-05-16 |
|    9 |       3 |   201 | 2016-05-17 |
+------+---------+-------+------------+
9 rows in set (0.00 sec)

注意：Websites表中的id列指向access_log表中的site_id字段。上面两个表是通过site_id列联系起来的
```



**实例**

```sql
#查找到Websites中所有网站的访问记录，并以id排序
mysql> SELECT Websites.id,Websites.name,access_log.count,access_log.date FROM Websites INNER JOIN access_log ON Websites.id=access_log.site_id ORDER BY Websites.id;
+------+--------------+-------+------------+
| id   | name         | count | date       |
+------+--------------+-------+------------+
|    1 | Google       |    45 | 2016-05-10 |
|    1 | Google       |   230 | 2016-05-14 |
|    2 | 淘宝         |    10 | 2016-05-14 |
|    3 | 菜鸟教程     |   100 | 2016-05-13 |
|    3 | 菜鸟教程     |   220 | 2016-05-15 |
|    3 | 菜鸟教程     |   201 | 2016-05-17 |
|    4 | 微博         |    13 | 2016-05-15 |
|    5 | Facebook     |   205 | 2016-05-14 |
|    5 | Facebook     |   545 | 2016-05-16 |
+------+--------------+-------+------------+
9 rows in set (0.00 sec)
```

**不同的 SQL JOIN：**

- **INNER JOIN**：如果表中有至少一个匹配，则返回行
- **LEFT JOIN**：即使右表中没有匹配，也从左表返回所有的行
- **RIGHT JOIN**：即使左表中没有匹配，也从右表返回所有的行
- **FULL JOIN**：只要其中一个表中存在匹配，则返回行



### 8. SQL INNER JOIN 关键字

**SQL INNER JOIN 关键字**

INNER JOIN关键字在表中存在至少一个匹配时返回行



**SQL INNER JOIN 语法**

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name=table2.column_name;

或

SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name=table2.column_name;
```

**参数说明：**

- columns：要显示的列名。
- table1：表1的名称。
- table2：表2的名称。
- column_name：表中用于连接的列名。

**注释：**INNER JOIN 与 JOIN 是相同的。

![SQL INNER JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_innerjoin.gif)



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+------+---------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM access_log;
+------+---------+-------+------------+
| aid  | site_id | count | date       |
+------+---------+-------+------------+
|    1 |       1 |    45 | 2016-05-10 |
|    2 |       3 |   100 | 2016-05-13 |
|    3 |       1 |   230 | 2016-05-14 |
|    4 |       2 |    10 | 2016-05-14 |
|    5 |       5 |   205 | 2016-05-14 |
|    6 |       4 |    13 | 2016-05-15 |
|    7 |       3 |   220 | 2016-05-15 |
|    8 |       5 |   545 | 2016-05-16 |
|    9 |       3 |   201 | 2016-05-17 |
+------+---------+-------+------------+
9 rows in set (0.00 sec)
```



**SQL INNER JOIN 实例**

```sql
#返回所有网站的访问记录
mysql> SELECT Websites.name,access_log.count,access_log.date FROM Websites INNER JOIN access_log ON Websites.id=access_log.site_id ORDER BY access_log.count;
+--------------+-------+------------+
| name         | count | date       |
+--------------+-------+------------+
| 淘宝         |    10 | 2016-05-14 |
| 微博         |    13 | 2016-05-15 |
| Google       |    45 | 2016-05-10 |
| 菜鸟教程     |   100 | 2016-05-13 |
| 菜鸟教程     |   201 | 2016-05-17 |
| Facebook     |   205 | 2016-05-14 |
| 菜鸟教程     |   220 | 2016-05-15 |
| Google       |   230 | 2016-05-14 |
| Facebook     |   545 | 2016-05-16 |
+--------------+-------+------------+
9 rows in set (0.03 sec)
```

**注释：**INNER JOIN 关键字在表中存在至少一个匹配时返回行（返回选中列组成的行）。如果 "Websites" 表中的行在 "access_log" 中没有匹配，则不会列出这些行。



### 9. SQL LEFT JOIN 关键字

**SQL LEFT JOIN 关键字**

LEFT JOIN关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为NULL



**SQL LEFT JOIN 语法**

```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name=table2.column_name;

或

SELECT column_name(s)
FROM table1
LEFT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```

**注释：**在某些数据库中，LEFT JOIN 称为 LEFT OUTER JOIN。

![SQL LEFT JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_leftjoin.gif)



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+------+---------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM access_log;
+------+---------+-------+------------+
| aid  | site_id | count | date       |
+------+---------+-------+------------+
|    1 |       1 |    45 | 2016-05-10 |
|    2 |       3 |   100 | 2016-05-13 |
|    3 |       1 |   230 | 2016-05-14 |
|    4 |       2 |    10 | 2016-05-14 |
|    5 |       5 |   205 | 2016-05-14 |
|    6 |       4 |    13 | 2016-05-15 |
|    7 |       3 |   220 | 2016-05-15 |
|    8 |       5 |   545 | 2016-05-16 |
|    9 |       3 |   201 | 2016-05-17 |
+------+---------+-------+------------+
9 rows in set (0.00 sec)
```



**SQL LEFT JOIN 实例**

```sql
#返回所有网站以及它们的访问量（如果有的话）
#把Websites作为左表，access_log作为右表
mysql> SELECT Websites.name,access_log.count,access_log.date FROM Websites LEFT JOIN access_log ON Websites.id=access_log.site_id ORDER BY access_log.count DESC;
+---------------+-------+------------+
| name          | count | date       |
+---------------+-------+------------+
| Facebook      |   545 | 2016-05-16 |
| Google        |   230 | 2016-05-14 |
| 菜鸟教程      |   220 | 2016-05-15 |
| Facebook      |   205 | 2016-05-14 |
| 菜鸟教程      |   201 | 2016-05-17 |
| 菜鸟教程      |   100 | 2016-05-13 |
| Google        |    45 | 2016-05-10 |
| 微博          |    13 | 2016-05-15 |
| 淘宝          |    10 | 2016-05-14 |
| stackoverflow |  NULL | NULL       |
+---------------+-------+------------+
10 rows in set (0.00 sec)
#右表没匹配记录也会显示，只不过数据是NULL
```

**注释：**LEFT JOIN 关键字从左表（Websites）返回所有的行，即使右表（access_log）中没有匹配。



### 10. SQL RIGHT JOIN 关键字

**SQL RIGHT JOIN 关键字**

RIGHT JOIN 关键字从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为 NULL。



**SQL RIGHT JOIN 语法**

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name=table2.column_name;

或

SELECT column_name(s)
FROM table1
RIGHT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```

**注释：**在某些数据库中，RIGHT JOIN 称为 RIGHT OUTER JOIN。

![SQL RIGHT JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_rightjoin.gif)



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+------+---------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM access_log;
+------+---------+-------+------------+
| aid  | site_id | count | date       |
+------+---------+-------+------------+
|    1 |       1 |    45 | 2016-05-10 |
|    2 |       3 |   100 | 2016-05-13 |
|    3 |       1 |   230 | 2016-05-14 |
|    4 |       2 |    10 | 2016-05-14 |
|    5 |       5 |   205 | 2016-05-14 |
|    6 |       4 |    13 | 2016-05-15 |
|    7 |       3 |   220 | 2016-05-15 |
|    8 |       5 |   545 | 2016-05-16 |
|    9 |       3 |   201 | 2016-05-17 |
|   10 |       6 |   111 | 2016-03-19 |
+------+---------+-------+------------+
10 rows in set (0.00 sec)
```



**SQL RIGHT JOIN 实例**

```sql
#返回网站的访问记录
#把Websites作左表，access_log作右表
mysql> SELECT Websites.name,access_log.count,access_log.date FROM Websites RIGHT JOIN access_log ON Websites.id=access_log.site_id ORDER BY access_log.count DESC;
+--------------+-------+------------+
| name         | count | date       |
+--------------+-------+------------+
| Facebook     |   545 | 2016-05-16 |
| Google       |   230 | 2016-05-14 |
| 菜鸟教程     |   220 | 2016-05-15 |
| Facebook     |   205 | 2016-05-14 |
| 菜鸟教程     |   201 | 2016-05-17 |
| NULL         |   111 | 2016-03-19 |
| 菜鸟教程     |   100 | 2016-05-13 |
| Google       |    45 | 2016-05-10 |
| 微博         |    13 | 2016-05-15 |
| 淘宝         |    10 | 2016-05-14 |
+--------------+-------+------------+
10 rows in set (0.00 sec)
#左边没有对应的记录也会显示，只不过是NULL
```

**注释：**RIGHT JOIN 关键字从右表（access_log）返回所有的行，即使左表（Websites）中没有匹配。



### 11. SQL FULL OUTER JOIN 关键字

**SQL FULL OUTER JOIN 关键字**

FULL OUTER JOIN关键字只要左表（table1）和右表（table2）其中一个表中存在匹配，则返回行

FULL OUTER JOIN关键字结合了LEFT JOIN和RIGHT JOIN的结果



**SQL FULL OUTER JOIN 语法**

```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name=table2.column_name;
```

![SQL FULL OUTER JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_fulljoin.gif)



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+------+---------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM access_log;
+------+---------+-------+------------+
| aid  | site_id | count | date       |
+------+---------+-------+------------+
|    1 |       1 |    45 | 2016-05-10 |
|    2 |       3 |   100 | 2016-05-13 |
|    3 |       1 |   230 | 2016-05-14 |
|    4 |       2 |    10 | 2016-05-14 |
|    5 |       5 |   205 | 2016-05-14 |
|    6 |       4 |    13 | 2016-05-15 |
|    7 |       3 |   220 | 2016-05-15 |
|    8 |       5 |   545 | 2016-05-16 |
|    9 |       3 |   201 | 2016-05-17 |
+------+---------+-------+------------+
9 rows in set (0.00 sec)
```



**SQL FULL OUTER JOIN 实例**

```sql
#选取所有网站访问记录
#MySQL中不支持FULL OUTER JOIN
```

**注释：**FULL OUTER JOIN 关键字返回左表（Websites）和右表（access_log）中所有的行。如果 "Websites" 表中的行在 "access_log" 中没有匹配或者 "access_log" 表中的行在 "Websites" 表中没有匹配，也会列出这些行。



### 12. SQL UNION 操作符

SQL UNION操作符合并两个或多个SELECT语句的结果



**SQL UNION 操作符**

UNION内部的每个SELECT语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个SELECT语句中的列的顺序必须相同



**SQL UNION 语法**

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

**注释：**UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+------+---------------+---------------------------+-------+---------+
6 rows in set (0.04 sec)

mysql> SELECT * FROM apps;
+------+------------+-------------------------+---------+
| id   | app_name   | url                     | country |
+------+------------+-------------------------+---------+
|    1 | QQ APP     | http://im.qq.com/       | CN      |
|    2 | 微博 APP   | http://weibo.com/       | CN      |
|    3 | 淘宝 APP   | https://www.taobao.com/ | CN      |
+------+------------+-------------------------+---------+
3 rows in set (0.00 sec)
```



**SQL UNION 实例**

```sql
#从"Websites"和"apps"表中选取所有不同的country（只有不同的值）
mysql> SELECT country FROM Websites UNION SELECT country FROM apps ORDER BY country;
+---------+
| country |
+---------+
| CN      |
| IND     |
| USA     |
+---------+
3 rows in set (0.00 sec)
```

**注释：**UNION 不能用于列出两个表中所有的country。如果一些网站和APP来自同一个国家，每个国家只会列出一次。UNION 只会选取不同的值。请使用 UNION ALL 来选取重复的值！



**SQL UNION ALL 实例**

```sql
#使用UNION ALL从"Websites"和"apps"表中选取所有的country（也有重复的值）
mysql> SELECT country FROM Websites UNION ALL SELECT country FROM apps ORDER BY country;
+---------+
| country |
+---------+
| CN      |
| CN      |
| CN      |
| CN      |
| CN      |
| IND     |
| USA     |
| USA     |
| USA     |
+---------+
9 rows in set (0.00 sec)
```



**带有 WHERE 的 SQL UNION ALL**

```sql
#使用UNION ALL从"Websites"和"apps"表中选取所有的中国（CN）的数据（也有重复的值）
mysql> SELECT country,name FROM Websites WHERE country='CN' UNION ALL SELECT country,app_name FROM apps WHERE country='CN';
+---------+------------+
| country | name       |
+---------+------------+
| CN      | 淘宝       |
| CN      | 微博       |
| CN      | QQ APP     |
| CN      | 微博 APP   |
| CN      | 淘宝 APP   |
+---------+------------+
5 rows in set (0.00 sec)
```

### 13. SQL SELECT INTO 语句

通过SQL，可以从一个表复制信息到另一个表

SELECT INTO语句从一个表复制数据，然后把数据插入到另一个新表中



**SQL SELECT INTO 语句**

**注意：**

MySQL 数据库不支持 SELECT ... INTO 语句，但支持INSERT INTO ... SELECT 。

当然你可以使用以下语句来拷贝表结构及数据：

```sql
CREATE TABLE new_table
AS
SELECT * FROM old_table;
```



**SQL SELECT INTO 语法**

```sql
#复制所有的列插入到新表中
SELECT *
INTO newtable [IN externaldb]
FROM table1;

#只复制希望的列插入到新表中
SELECT column_name(s)
INTO newtable [IN externaldb]
FROM table1;
```

**提示：**新表将会使用 SELECT 语句中定义的列名称和类型进行创建。您可以使用 AS 子句来应用新名称。



**SQL SELECT INTO 实例**

```sql
#创建Websites的备份复件
mysql> CREATE TABLE WebsitesBackup2023 AS SELECT * FROM Websites;
Query OK, 6 rows affected (0.03 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM WebsitesBackup2023;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+------+---------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

#只复制一些列插入到新表中
mysql> CREATE TABLE WebsitesBackupColumn AS SELECT name,url FROM Websites;
Query OK, 6 rows affected (0.05 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM WebsitesBackupColumn;
+---------------+---------------------------+
| name          | url                       |
+---------------+---------------------------+
| Google        | https://www.google.cm/    |
| 淘宝          | https://www.taobao.com/   |
| 菜鸟教程      | http://www.runoob.com/    |
| 微博          | http://weibo.com/         |
| Facebook      | https://www.facebook.com/ |
| stackoverflow | http://stackoverflow.com/ |
+---------------+---------------------------+
6 rows in set (0.00 sec)

#只复制中国的网站插入到新表中
mysql> CREATE TABLE WebsitesCN AS SELECT * FROM Websites WHERE country='CN';
Query OK, 2 rows affected (0.05 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM WebsitesCN;
+------+--------+-------------------------+-------+---------+
| id   | name   | url                     | alexa | country |
+------+--------+-------------------------+-------+---------+
|    2 | 淘宝   | https://www.taobao.com/ |    13 | CN      |
|    4 | 微博   | http://weibo.com/       |    20 | CN      |
+------+--------+-------------------------+-------+---------+
2 rows in set (0.00 sec)

#复制多个表中的数据插入到新表中
mysql> CREATE TABLE WebsitesMultiTable AS SELECT Websites.name,access_log.count,access_log.date FROM Websites LEFT JOIN access_log ON Websites.id=access_log.site_id;#只要有id匹配的，就把这些数据筛选出来
Query OK, 10 rows affected (0.03 sec)
Records: 10  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM WebsitesMultiTable;
+---------------+-------+------------+
| name          | count | date       |
+---------------+-------+------------+
| Google        |   230 | 2016-05-14 |
| Google        |    45 | 2016-05-10 |
| 淘宝          |    10 | 2016-05-14 |
| 菜鸟教程      |   201 | 2016-05-17 |
| 菜鸟教程      |   220 | 2016-05-15 |
| 菜鸟教程      |   100 | 2016-05-13 |
| 微博          |    13 | 2016-05-15 |
| Facebook      |   545 | 2016-05-16 |
| Facebook      |   205 | 2016-05-14 |
| stackoverflow |  NULL | NULL       |
+---------------+-------+------------+
10 rows in set (0.00 sec)

#创建空表，只要添加促使查询没有数据返回的WHERE子句即可
mysql> CREATE TABLE emptyTable AS SELECT * FROM Websites WHERE 1=0;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM emptyTable;
Empty set (0.00 sec)
```



### 14. SQL INSERT INTO SELECT 语句

**SQL INSERT INTO SELECT 语句**

INSERT INTO SELECT语句从一个表复制数据，然后把数据插入到一个已存在的表中。目标表中任何已存在的行都不会受影响



**SQL INSERT INTO SELECT 语法**

```sql
#我们可以从一个表中复制所有的列插入到另一个已存在的表中
INSERT INTO table2
SELECT * FROM table1;

#可以只复制指定的列插入到另一个已存在的表中
INSERT INTO table2
(column_name(s)))
SELECT column_name(s)
FROM table1;
```



**演示数据库**

```sql
mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+------+---------------+---------------------------+-------+---------+
6 rows in set (0.04 sec)

mysql> SELECT * FROM apps;
+------+------------+-------------------------+---------+
| id   | app_name   | url                     | country |
+------+------------+-------------------------+---------+
|    1 | QQ APP     | http://im.qq.com/       | CN      |
|    2 | 微博 APP   | http://weibo.com/       | CN      |
|    3 | 淘宝 APP   | https://www.taobao.com/ | CN      |
+------+------------+-------------------------+---------+
3 rows in set (0.00 sec)
```



**SQL INSERT INTO SELECT 实例**

```sql
#复制"apps"中的数据插入到"Websites"中，app_name和name匹配，country和country匹配
mysql> INSERT INTO Websites(name,country) SELECT app_name,country FROM apps;
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
| NULL | QQ APP        | NULL                      |  NULL | CN      |
| NULL | 微博 APP      | NULL                      |  NULL | CN      |
| NULL | 淘宝 APP      | NULL                      |  NULL | CN      |
| NULL | QQ APP        | NULL                      |  NULL | CN      |
+------+---------------+---------------------------+-------+---------+
10 rows in set (0.00 sec)
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
| NULL | QQ APP        | NULL                      |  NULL | CN      |
| NULL | 微博 APP      | NULL                      |  NULL | CN      |
| NULL | 淘宝 APP      | NULL                      |  NULL | CN      |
+------+---------------+---------------------------+-------+---------+
9 rows in set (0.00 sec)

#只复制id=1的数据到"Websites"中
mysql> SELECT * FROM Websites;
+------+---------------+---------------------------+-------+---------+
| id   | name          | url                       | alexa | country |
+------+---------------+---------------------------+-------+---------+
|    1 | Google        | https://www.google.cm/    |     1 | USA     |
|    2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|    3 | 菜鸟教程      | http://www.runoob.com/    |  5000 | USA     |
|    4 | 微博          | http://weibo.com/         |    20 | CN      |
|    5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|    7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
| NULL | QQ APP        | NULL                      |  NULL | CN      |
| NULL | 微博 APP      | NULL                      |  NULL | CN      |
| NULL | 淘宝 APP      | NULL                      |  NULL | CN      |
| NULL | QQ APP        | NULL                      |  NULL | CN      |
+------+---------------+---------------------------+-------+---------+
10 rows in set (0.00 sec)
```



### 15. SQL CREATE DATABASE 语句

**SQL CREATE DATABASE 语句**

CREATE DATABASE语句用于创建数据库



**SQL CREATE DATABASE 语法**

```sql
CREATE DATABASE dbname;
```



**SQL CREATE DATABASE 实例**

```sql
#创建一个名为"my_db"的数据库
mysql> CREATE DATABASE my_db;
Query OK, 1 row affected (0.02 sec)
```



### 16. SQL CREATE TABLE 语句

**SQL CREATE TABLE 语句**

CREATE TABLE语句用于创建数据库中的表

表由行和列组成，每个表都必须有个表名



**SQL CREATE TABLE 语法**

```sql
CREATE TABLE table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
);
```

column_name 参数规定表中列的名称。

data_type 参数规定列的数据类型（例如 varchar、integer、decimal、date 等等）。

size 参数规定表中列的最大长度。





**SQL CREATE TABLE 实例**

```sql
#创建一个名为"Persons"的表，包含5列：PersonID。LastName、FirstName、Address和City
mysql> CREATE TABLE Persons (PersonID int,LastName varchar(255),FirstName varchar(255),Address varchar(255),City varchar(255));
Query OK, 0 rows affected (0.02 sec)
```

**提示：**可使用 INSERT INTO 语句向空表写入数据。



### 17. SQL 约束（Constraints）

**SQL 约束（Constraints）**

SQL约束用于规定表中的数据规则

如果存在违反约束的数据行为，行为会被约束终止

约束可以在创建表时规定（通过CREATE TABLE语句），或者在表创建之后规定（通过ALTER TABLE语句）



**SQL CREATE TABLE + CONSTRAINT 语法**

```sql
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name.
....
);
```

在SQL中，有如下约束：

- NOT NULL：指示某列不能存储NULL值
- UNIQUE：保证某列的每行必须有唯一的值
- PRIMARY KEY：NOT NULL和UNIQUE的结合。确保某列（或者两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录
- FOREIGN KEY：保证一个表中的数据匹配另一表中的值的参照完整性
- CHECK：保证列中的值符合指定的条件
- DEFAULT：规定没有给列赋值时的默认值



### 18. SQL NOT NULL 约束

在默认的情况下，表的列接收NULL值



**SQL NOT NULL 约束**

NOT NULL约束强制列不接受NULL值

NOT NULL约束强制字段始终包含值。这意味着，如果不向字段添加值，就无法插入新纪录或者更新记录

```sql
#强制'ID'列、'LastName'列以及'FirstName'列不接受NULL值
CREATE TABLE Person
(
ID int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255) NOT NULL,
Age int
);
```



**添加 NOT NULL 约束**

```sql
#在一个已创建的表的'Age'字段中添加NOT NULL约束
mysql> ALTER TABLE Person MODIFY Age int NOT NULL;
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0
```



**删除 NOT NULL 约束**

```sql
#在一个已创建的表的'Age'字段中删除NOT NULL约束
mysql> ALTER TABLE Person MODIFY Age int NULL;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0
```



### 19. SQL UNIQUE 约束

**SQL UNIQUE 约束**

UNIQUE约束唯一标识数据库表中的每条记录

UNIQUE和PRIMARY KEY约束均为列或列集合提供了唯一性的保证

PRIMARY KEY约束拥有自动定义的UNIQUE约束

注意，每个表可以有多个UNIQUE约束，但是每个表只能有一个PRIMARY约束


**CREATE TABLE 时的 SQL UNIQUE 约束**

```sql
#在"Persons"表创建时在'P_Id'列上创建UNIQUE约束
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
UNIQUE(P_Id)
);

#命名UNIQUE约束，并定义多个列的UNIQUE约束
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
CONSTRAINT uc_PersonID UNIQUE(P_Id,LastName)
);
```



**ALTER TABLE 时的 SQL UNIQUE 约束**

```sql
#当表已被创建时，如需在'P_Id'列创建UNIQUE约束
ALTER TABLE Persons ADD UNIQUE(P_Id);

#当表已被创建，需命名UNIQUE约束，并定义多个列的UNIQUE约束
ALTER TABLE Persons
ADD CONSTRAINT uc_PersonID UNIQUE(P_Id,LastName);
```



**撤销 UNIQUE 约束**

```sql
#撤销UNIQUE约束
ALTER TABLE DROP INDEX uc_PersonID;
```



### 20. SQL PRIMARY KEY 约束

**SQL PRIMARY KEY 约束**

PRIMARY KEY约束唯一标识数据库表中的每条记录

主键必须包含唯一的值

主键列不能包含NULL值

每个表都应该有一个主键，并且每个表只能有一个主键



**CREATE TABLE 时的 SQL PRIMARY KEY 约束**

```sql
#在"Persons"表创建时再"P_Id"列上创建PRIMARY KEY约束
CREATE TABLE Persons
(
P_Id int NOT NULL,
....
PRIMARY KEY(P_Id)
);

#如需命名PRIMARY KEY约束，并定义多个列的PRIMARY KEY约束
#添加主键的列必须在首次创建时声明为NOT NULL
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
#命名PRIMARY KEY约束为pk_PersonID，并定义P_Id和LastName两个列的约束
CONSTRAINT pk_PersonID PRIMARY KEY (P_Id,LastName)
);

```

**注释：**在上面的实例中，只有一个主键 PRIMARY KEY（pk_PersonID）。然而，pk_PersonID 的值是由两个列（P_Id 和 LastName）组成的。



**ALTER TABLE 时的 SQL PRIMARY KEY 约束**

```sql
#当表已被创建时，如需在'P_Id'列创建PRIMARY KEY约束
ALTER TABLE Persons
ADD PRIMARY KEY (P_Id)

#如需命名PRIMARY KEY约束，并定义多个列的PRIMARY KEY约束
ALTER TABLE Persons
ADD CONSTRAINT pk_PersonID PRIMARY KEY(P_Id,LastName);
```

**注释：**如果您使用 ALTER TABLE 语句添加主键，必须把主键列声明为不包含 NULL 值（在表首次创建时）。





**撤销 PRIMARY KEY 约束**

```sql
#撤销PRIMARY KEY约束
#撤销PRIMARY KEY约束时，不论约束条件为一列还是多列，对于MySQL，撤销都是如下
ALTER TABLE Persons
DROP PRIMARY KEY;
```



### 21. SQL FOREIGN KEY 约束

**SQL FOREIGN KEY 约束**

一个表中的FOREIGN KEY指向另一个表中的UNIQUE KEY（唯一约束的键）

![image-20230724235144110](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230724235144110.png)



**CREATE TABLE 时的 SQL FOREIGN KEY 约束**

```sql
#在"Orders"表中创建时在"P_Id"列上创建FOREIGN KEY约束
CREATE TABLE Orders
(
O_Id int NOT NULL,
OrderNo int NOT NULL,
P_Id int,
PRIMARY KEY (O_Id),
FOREIGN KEY (P_Id) REFERENCES Persons(P_Id)#Orders的P_Id连接到Persons的P_Id
);

#命名FOREIGN KEY，并定义多个列的FOREIGN KEY约束
CREATE TABLE Orders
(
O_Id int NOT NULL,
OrderNo int NOT NULL,
P_Id int,
PRIMARY KEY(O_Id),
CONSTRAINT fk_PerOrders FOREIGN KEY(P_Id)
REFERENCES Persons(P_Id)
);
```



**ALTER TABLE 时的 SQL FOREIGN KEY 约束**

```sql
#"Orders"表已被创建，在'P_Id'列创建FOREIGN KEY约束
ALTER TABLE Orders
ADD FOREIGN KEY(P_Id)
REFERENCES Persons(P_Id);

#"Orders"表已被创建，命名FOREIGN KEY，并定义多个列的FOREIGN KEY约束
ALTER TABLE Orders
ADD CONSTRAINT fk_PerOrders
FOREIGN KEY(P_Id)
REFERENCES Persons(P_Id);
```



**撤销 FOREIGN KEY 约束**

```sql
#撤销FOREIGN KEY约束
ALTER TABLE Orders
DROP FOREIGN KEY fk_PerOrders;
```

**总结：**创建外键时，FOREIGN KEY后总是跟着REFERENCES，因为要和另一个表的列关联，那必然需要一个参照



### 22. SQL CHECK 约束

**SQL CHECK 约束**

CHECK约束用于限制列中的值的范围

如果对单个列定义CHECK约束，那么该列只允许特定的值
如果对于一个表定义CHECK约束，那么此约束会基于行中其他列的值在特定的列中对值进行限制



**CREATE TABLE 时的 SQL CHECK 约束**

```sql
#在"Persons"表创建时在'P_Id'列上创建CHECK约束。CHECK约束规定'P_Id'列必须只包含大于0的整数
CREATE TABLE Persons
(
P_Id int NOT NULL,
....
CHECK(P_Id>0)
);

#命名CHECK约束，并定义多个列的CHECK约束
CREATE TABLE Persons
(
P_Id int NOT NULL,
City varchar(255),
....
CONSTRAINT chk_Person CHECK(P_Id>0 AND City='Sandnes')
);
```



**ALTER TABLE 时的 SQL CHECK 约束**

```sql
#当表已被创建时，在'P_Id'列创建CHECK约束
ALTER TABLE Persons
ADD CHECK(P_Id>0);

#当表已被创建时，命名CHECK约束，并定义多个列的CHECK约束
ALTER TABLE Persons
ADD CONSTRAINT chk_Person CHECK(P_id>0 AND City='Sandnes');
```



**撤销 CHECK 约束**

```sql
#撤销CHECK约束
ALTER TABLE Persons
DROP CONSTRAINT chk_Person;
```



### 23. SQL DEFAULT 约束

**SQL DEFAULT 约束**

DEFAULT约束用于向列中插入默认值

如果没有规定其他的值，那么会将默认值添加到所有的新纪录



**CREATE TABLE 时的 SQL DEFAULT 约束**

```sql
#在"Persons"表创建时在'City'列上创建DEFAULT约束
CREATE TABLE Persons
(
    P_Id int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) DEFAULT('Sandnes')
);

#通过使用类似GETDATE()这样的函数，DEFAULT约束也可以用于插入系统值
CREATE TABLE Orders
(
    O_Id int NOT NULL,
    OrderNo int NOT NULL,
    P_Id int,
    OrderDate date DEFAULT(GETDATE())
);
```



**ALTER TABLE 时的 SQL DEFAULT 约束**

```sql
#当表已被创建时，在'City'列创建DEFAULT约束
ALTER TABLE Persons
ALTER City SET DEFAULT 'SANDNES';
```



**撤销 DEFAULT 约束**

```sql
#撤销DEFAULT约束
ALTER TABLE Persons
ALTER City DROP DEFAULT;
```



### 24. SQL CREATE INDEX 语句

CREATE INDEX语句用于在表中创建索引
在不读取整个表的情况下，索引使数据库应用程序可以更快地查询数据



**索引**

在表中创建索引，以便更加快速高效地查询数据

用户无法看到索引，它们只能被用来加速搜索/查询

**注释：**更新一个包含索引的表需要比更新一个没有索引的表花费更多的时间，这是由于索引本身也需要更新。因此，理想的做法是仅仅在常常被搜索的列（以及表）上面创建索引。



**SQL CREATE INDEX 语法**

```sql
#在表上创建一个简单的索引，允许使用重复的值
CREATE INDEX index_name
ON table_name (column_name);
```



**SQL CREATE UNIQUE INDEX 语法**

```sql
#在表上创建一个唯一的索引。不允许使用重复的值：唯一的索引意味着两个行不能拥有相同的索引值
CREATE UNIQUE INDEX index_name
ON table_name (column_name);
```

**注释：**用于创建索引的语法在不同的数据库中不一样。因此，检查您的数据库中创建索引的语法。



**CREATE INDEX 实例**

```sql
#在"Persons"表的'LastName'列上创建一个名为'PIndex'的索引
CREATE INDEX PIndex
ON Persons (LastNmae);

#多个列
CREATE INDEX PIndex
ON Persons (LastName,FirstName);
```

