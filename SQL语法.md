# SQL语法

[SQL 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/sql/sql-tutorial.html)

## 1.SQL简介

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

## 2.SQL语法

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