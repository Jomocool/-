# MySQL

## 一、基础篇

### 1.MySQL概述

#### 1.1数据库相关概念

- **数据库(DataBase)：**存储数据的仓库，数据是有组织地进行存储
- **数据库管理系统：**操纵和管理数据库的大型软件
- **SQL：**操作关系型数据库的编程语言，定义了一套操作关系型数据库统一标准

#### 1.2连接MySQL

cmd：mysql -u root -p

#### 1.3数据库模型

- **关系型数据库：**建立在关系型基础上，由多张相互连接的二维表组成的数据库

  使用表存储结构，格式统一，便于维护

  使用SQL语言操作，标准统一，使用方便

#### 1.4数据模型

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/1.png)

### 2.SQL

#### 2.1通用语法

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/2.png)

#### 2.2SQL分类

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/3.png)

#### 2.3DDL

##### 2.3.1查询

- **数据库操作：**

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/4.png)

- **表操作：**

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/5.png)

##### 2.3.2创建

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/6.png)

```sql
1.创建表
mysql> create table tb_user(
    -> id int comment '编号',//comment是注释
    -> name varchar(50) comment'姓名',//不是string，是varchar并要指定长度大小
    -> age int comment'年龄',
    -> gender varchar(1) comment'性别'
    -> )comment'用户表';
    
2.查询表结构
mysql> desc tb_user;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int         | YES  |     | NULL    |       |
| name   | varchar(50) | YES  |     | NULL    |       |
| age    | int         | YES  |     | NULL    |       |
| gender | varchar(1)  | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+

3.创建表的详细信息
mysql> show create table tb_user;
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table   | Create Table                                                                                                                                                                                                                                                                                      |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| tb_user | CREATE TABLE `tb_user` (
  `id` int DEFAULT NULL COMMENT '编号',
  `name` varchar(50) DEFAULT NULL COMMENT '姓名',
  `age` int DEFAULT NULL COMMENT '年龄',
  `gender` varchar(1) DEFAULT NULL COMMENT '性别'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='用户表' |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

**数据类型：**

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/7.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/8.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/9.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/10.png)

**案例：**

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/11.png)

```sql
mysql> create table emp(
    -> id int comment'编号',
    -> workno varchar(10) comment'工号',
    -> name varchar(10) comment'姓名',
    -> gender char(1) comment'性别',
    -> age tinyint unsigned comment'年龄',
    -> idcard char(18) comment'身份证号',
    -> entrydate date comment'入职时间'
    -> )comment'员工表';

mysql> desc emp;
+-----------+------------------+------+-----+---------+-------+
| Field     | Type             | Null | Key | Default | Extra |
+-----------+------------------+------+-----+---------+-------+
| id        | int              | YES  |     | NULL    |       |
| workno    | varchar(10)      | YES  |     | NULL    |       |
| name      | varchar(10)      | YES  |     | NULL    |       |
| gender    | char(1)          | YES  |     | NULL    |       |
| age       | tinyint unsigned | YES  |     | NULL    |       |
| idcard    | char(18)         | YES  |     | NULL    |       |
| entrydate | date             | YES  |     | NULL    |       |
+-----------+------------------+------+-----+---------+-------+
```

##### 2.3.3修改

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/12.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/13.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/14.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/15.png)

```sql
1.添加字段
mysql> alter table emp add nickname varchar(20) comment'昵称';
mysql> desc emp;
+-----------+------------------+------+-----+---------+-------+
| Field     | Type             | Null | Key | Default | Extra |
+-----------+------------------+------+-----+---------+-------+
| id        | int              | YES  |     | NULL    |       |
| workno    | varchar(10)      | YES  |     | NULL    |       |
| name      | varchar(10)      | YES  |     | NULL    |       |
| gender    | char(1)          | YES  |     | NULL    |       |
| age       | tinyint unsigned | YES  |     | NULL    |       |
| idcard    | char(18)         | YES  |     | NULL    |       |
| entrydate | date             | YES  |     | NULL    |       |
| nickname  | varchar(20)      | YES  |     | NULL    |       |
+-----------+------------------+------+-----+---------+-------+

2.修改字段名和字段类型
mysql> alter table emp change nickname username varchar(30);
mysql> desc emp;
+-----------+------------------+------+-----+---------+-------+
| Field     | Type             | Null | Key | Default | Extra |
+-----------+------------------+------+-----+---------+-------+
| id        | int              | YES  |     | NULL    |       |
| workno    | varchar(10)      | YES  |     | NULL    |       |
| name      | varchar(10)      | YES  |     | NULL    |       |
| gender    | char(1)          | YES  |     | NULL    |       |
| age       | tinyint unsigned | YES  |     | NULL    |       |
| idcard    | char(18)         | YES  |     | NULL    |       |
| entrydate | date             | YES  |     | NULL    |       |
| username  | varchar(30)      | YES  |     | NULL    |       |
+-----------+------------------+------+-----+---------+-------+

3.删除字段
mysql> alter table emp drop username;
mysql> desc emp;
+-----------+------------------+------+-----+---------+-------+
| Field     | Type             | Null | Key | Default | Extra |
+-----------+------------------+------+-----+---------+-------+
| id        | int              | YES  |     | NULL    |       |
| workno    | varchar(10)      | YES  |     | NULL    |       |
| name      | varchar(10)      | YES  |     | NULL    |       |
| gender    | char(1)          | YES  |     | NULL    |       |
| age       | tinyint unsigned | YES  |     | NULL    |       |
| idcard    | char(18)         | YES  |     | NULL    |       |
| entrydate | date             | YES  |     | NULL    |       |
+-----------+------------------+------+-----+---------+-------+

4.修改表名
mysql> alter table emp rename to employee;
mysql> show tables;
+------------------+
| Tables_in_itcast |
+------------------+
| employee         |
| tb_user          |
+------------------+
```

##### 2.3.4删除

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/16.png)

```sql
1.删除表
mysql> drop table if exists tb_user;
mysql> show tables;
+------------------+
| Tables_in_itcast |
+------------------+
| employee         |
+------------------+

2.删除指定表，并重新创建该表
mysql> truncate table employee;
mysql> show tables;
+------------------+
| Tables_in_itcast |
+------------------+
| employee         |
+------------------+
```


