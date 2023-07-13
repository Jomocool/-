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
