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


#### 2.4DML

##### 2.4.1介绍

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/17.png)

##### 2.4.2添加

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/18.png)

##### 2.4.3修改

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/19.png)

##### 2.4.5删除

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/20.png)

```sql
insert into employee(id, workno, name, gender, age, idcard, entrydate) values (1,'1','itcast','男',18,'123456789012345678','2000-01-01');

select * from employee;

insert into employee values(2,'2','张无忌','男',18,'123456789012345670','2005-01-01');

insert into employee values(3,'3','韦一笑','男',38,'123456789012345670','2005-01-01'),(4,'4','赵敏','女',18,'123456789012345670','2005-01-01');


-- 修改id为1的数据，将name改为itheima
update employee set name = 'itheima' where id = 1;

-- 修改id为1的数据，将name改为小昭，gender改为女
update employee set name = '小昭',gender = '女' where id=1;

-- 将所有的员工入职日期修改为2000-01-01
update employee set entrydate = '2000-01-01';


-- 删除gender为女的员工
delete from employee where gender='女';

-- 删除所有员工
delete from employee;
```

#### 2.5DQL

##### 2.5.1介绍

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/21.png)

##### 2.5.2语法

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/30.png)

##### 2.5.3基础查询

```sql
-- 数据准备
create table emp(
    id int comment'编号',
    workno varchar(10) comment '工号',
    name varchar(10) comment '姓名',
    gender char(1) comment '性别',
    age tinyint unsigned comment '年龄',
    idcard char(18) comment '身份证号',
    workaddress varchar(50) comment '工作地址',
    entrydate date comment '入职时间'
)comment '员工表';

insert into emp(id, workno, name, gender, age, idcard, workaddress, entrydate)
values (1,'1','柳岩','女',20,'123456789012345678','北京','2000-01-01'),
       (2,'2','张无忌','男',18,'123456789012345670','北京','2005-09-01'),
       (3,'3','韦一笑','男',38,'123456789712345670','上海','2005-08-01'),
       (4,'4','赵敏','女',18,'12345675712345670','北京','2009-12-01'),
       (5,'5','小昭','女',16,'123456769012345678','上海','2007-07-01'),
       (6,'6','杨逍','男',28,'12345678931234567X','北京','2006-01-01'),
       (7,'7','范瑶','女',40,'123456789212345670','北京','2005-05-01'),
       (8,'8','黛绮丝','女',38,'123456157012345670','天津','2015-05-01'),
       (9,'9','范凉凉','男',45,'123156789012345678','北京','2010-04-01'),
       (10,'10','陈友谅','男',53,'123456789012345670','上海','2011-01-01'),
       (11,'11','张士诚','男',55,'123567897123465670','江苏','2015-05-01'),
       (12,'12','常遇春','男',32,'123446757152345670','北京','2004-02-01'),
       (13,'13','张三丰','男',88,'123656789012345678','江苏','2020-11-01'),
       (14,'14','灭绝','女',65,'123456719012345670','西安','2019-05-01'),
       (15,'15','胡青牛','男',70,'12345674971234567X','西安','2018-04-01'),
       (16,'16','周芷若','女',18,null,'北京','2012-06-01');


-- 查询需求

-- 基本查询
-- 1.查询指定字段 name,workno,age 返回
select name,workno,age from emp;

-- 2.查询所有字段 返回
select id, workno, name, gender, age, idcard, workaddress, entrydate from emp;

-- 3.查询所有员工的工作地址，起别名
select workaddress '工作地址' from emp;

-- 4.查询公司员工的上班地址(不要重复）
select distinct workaddress '工作地址' from emp;
```

##### 2.5.4条件查询

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/23.png)

```sql
-- 条件查询
-- 1.查询年龄等于88的员工
select * from emp where age = 88;

-- 2.查询年龄小于20的员工
select * from emp where age < 20;

-- 3.查询年龄小于等于20的员工
select * from emp where age <= 20;

-- 4.查询没有身份证号的员工
select * from emp where idcard is null;

-- 5.查询有身份证号的员工
select * from emp where idcard is not null;

-- 6.查询年龄不等于88的员工
select * from emp where age != 88;
select * from emp where age <> 88;

-- 7.查询年龄在15岁(包含) 到 20岁(包含)之间的员工信息
select * from emp where age>=15 && age<=20;
select * from emp where age>=15 and age<=20;
select * from emp where age between 15 and 20;

-- 8.查询性别为女，且年龄小于25岁的员工
select * from emp where gender='女' and age<25;

-- 9.查询年龄等于18或20或40的员工
select * from emp where age=18 or age=20 or age=40;
select * from emp where age in(18,20,40);

-- 10.查询姓名为两个字的员工信息
select * from emp where name like '__';

-- 11.查询身份证号最后一位是X的员工
select * from emp where idcard like '%X';
select * from emp where idcard like '_________________X';
```

##### 2.5.5聚合函数

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/24.png)

```sql
-- 聚合函数
-- 1.统计该企业员工数量
select count(*) from emp;-- 16
select count(id) from emp;-- 16
select count(idcard) from emp;-- 15 null值不参与count函数计算

-- 2.统计该企业员工的平均年龄
select avg(age) from emp;

-- 3.统计该企业员工的最大年龄
select max(age) from emp;

-- 4.统计该企业员工的最小年龄
select min(age) from emp;

-- 5.统计西安地区员工的年龄之和
select sum(age) from emp where workaddress = '西安';
```

##### 2.5.6分组查询

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/25.png)

```sql
-- 分组查询
-- 1.根据性别分组，统计男性员工 和 女性员工的数量
select gender,count(*) from emp group by gender;

-- 2.根据性别分组，统计男性员工 和 女性员工的平均年龄
select gender,avg(age) from emp group by gender;

-- 3.查询年龄小于45的员工，并根据工作地址分组，获取员工数量大于等于3的工作地址
-- 3.1选出年龄小于45的员工，并根据工作地址分别显示人数
select workaddress,count(*) from emp where age<45 group by workaddress;
-- 3.2多加一个条件：员工数量大于等于3
select workaddress,count(*) address_count from emp where age<45 group by workaddress having address_count>=3;

根据什么分组，select后面就加上什么，方便辨别
count(*)是从所有row里面选
where->聚合函数(group by)->having：层层筛选，不断缩小范围
```

##### 2.5.7排序查询

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/26.png)

```sql
-- 排序查询
-- 1.根据年龄对公司的员工进行升序排序
select * from emp order by age asc;
select * from emp order by age;-- 默认升序

-- 2.根据入职时间对公司的员工进行降序排序
select * from emp order by entrydate desc;

-- 3.根据年龄对公司的员工进行升序排序，年龄相同，再按照入职时间进行降序排序
select * from emp order by age asc , entrydate desc;
```

##### 2.5.8分页查询

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/27.png)

```sql
-- 分页查询
-- 1.查询第1页员工数据，每页展示10条记录
select * from emp limit 0,10;
select * from emp limit 10;

-- 2.查询第2页员工数据，每页展示10条数据------->起始索引：(页码-1)*页展示记录数
select * from emp limit 10,10;
```

##### 2.5.9案例

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/28.png)

```sql
-- DQL语句练习
-- 1.查询年龄为20,21,22,23岁的女性员工信息
select * from emp where gender='女' and age in(20,21,22,23);

-- 2.查询性别为男，并且年龄在20~40岁(含)的姓名为三个字的员工
select * from emp where gender='男' and (age between 20 and 40) and name like '___';

-- 3.统计员工表中，年龄小于60岁的，男性员工和女性员工的人数
select gender,count(*) from emp where age<60 group by gender;

-- 4.查询所有年龄小于等于35岁员工的姓名和年龄，并对查询结果按年龄升序排序，如果年龄相同按入职时间降序排序
select name,age from emp where age<=35 order by age asc,entrydate desc;

-- 5.查询性别为男，且年龄在20~40岁(含)的前五个员工信息，对查询的结果按年龄升序排序，年龄相同按入职时间升序排序
select * from emp where gender='男' and age between 20 and 40 order by age asc,entrydate asc limit 5;
```

##### 2.5.10执行顺序

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/29.png)

```sql
-- 查询年龄大于15岁的员工的姓名、年龄、并根据年龄进行升序排序
select e.name ename,e.age eage from emp e where e.age>15 order by eage asc;
-- from：创建emp别名e
-- where：能够识别e，无法识别select创建的别名，说明在select之前执行
-- select：能够识别e，且创建name别名ename，age别名eage
-- order by：能够识别eage
-- limit
```

#### 2.6DCL

##### 2.6.1介绍

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/42.png)

##### 2.6.2管理用户

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/31.png)

```sql
-- 创建用户itcast，只能够在当前主机localhost访问，密码123456
create user 'itcast'@'localhost' identified by '123456';

-- 创建用户heima，可以在任意主机访问该数据库，密码123456
create user 'heima'@'%' identified by '123456';

-- 修改用户heima的访问密码为1234
alter user 'heima'@'%' identified with mysql_native_password by '1234';

-- 删除itcast@localhost用户
drop user 'itcast'@'localhost';
```

##### 2.6.3权限控制

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/32.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/33.png)

```sql
-- 管理用户对root某个数据库库的权限
-- 查询权限
show grants for 'heima'@'%';-- GRANT USAGE ON *.* TO `heima`@`%`，仅仅只是可以登录

-- 授予权限
grant all on itcast.* to 'heima'@'%';

-- 撤销权限
revoke all on itcast.* from 'heima'@'%';
```

### 3.函数

**函数：**一段可以被另一段程序调用的程序或代码

#### 3.1字符串函数

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/34.png)

```sql
-- concat
select contact('Hello','MySQL');-- 拼接字符串

-- lower
select lower('Hello');-- 小写Hello

-- upper
select upper('Hello');-- 大写Hello

-- lpad
select lpad('01',5,'-');-- 从01左边用-补充到长度5

-- rpad
select rpad('01',5,'-');-- 从01右边用-填充到长度5

-- trim
select trim(' Hello  MySQL  ');-- 去除头部和尾部空格

-- substring
select substring('Hello MySQL',1,5);-- 索引从1开始而不是0，Hello

-- 1.由于业务需求变更，企业员工的工号，统一为5位数，目前不足5位数的全部在前面补0,。比如：1号员工的工号为00001
update emp set workno = lpad(workno,5,'0');-- update更新表，set设置工号
```

#### 3.2数值函数

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/35.png)

```sql
-- ceil
select ceil(1.5);-- 向上取整

-- floor
select floor(1.1)-- 向下取整

-- mod
select mod(3,4);-- 3%4

-- rand
select rand();-- 0~1之间的随机数(小数)

-- round
select round(2.345,2);-- 对2.345四舍五入，保留2位小数

-- 2.通过数据库的函数，生成一个六位数的随机验证码
select rand();-- 随机
select rand()*1000000;-- 六位，但是会出现0.0...的情况，所以需要补位
select lpad(round(rand()*1000000,0),6,'0');
```

#### 3.3日期函数

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/36.png)

```sql
-- curdate()
select curdate();-- 当前日期

-- curtime()
select curtime();-- 当前时间

-- now()
select now();-- 当前日期时间

-- YEAR(),MONTH(),DAY()
select YEAR(now());
select MONTH(now());
select DAY(now());

-- date_add
select date_add(now(),INTERVAL 70 DAY);-- 当前往后推70天的日期

-- datediff
select datediff('2021-12-01','2021-10-01');-- 两日期间的差值天数

-- 3.查询所有员工的入职天数，并根据入职天数倒序排序
select name,datediff(curdate(),entrydate) as 'entrydays' from emp order by entrydays desc;
```

#### 3.4流程函数

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/37.png)

```sql
-- if
select if(true,'Ok','Error');-- true就返回Ok，否则就返回Error

-- ifnull
select ifnull('Ok','Default');-- Ok不为null，返回Ok
select ifnull('','Default');-- ‘’空串不为null，返回空串
select ifnull(null,'Default');-- 返回Default

-- case when then else end
-- 需求：查询emp表的员工姓名和工作地址(北京/上海 ----> 一线城市，其他 ----> 二线城市)
select
    name,
    (case workaddress when '北京' then '一线城市' when '上海' then '一线城市' else '二线城市' end) as '工作地址'
from emp;

-- 4.统计班级各个学员的成绩，展示的规则如下：
-- >=85，展示优秀
-- >=60，展示及格
-- 否则，不及格
create table score(
    id int comment'ID',
    name varchar(10) comment'姓名',
    math int comment'数学',
    english int comment'英语',
    chinese int comment'语文'
)comment '学员成绩表';
insert into score(id,name,math,english,chinese)VALUES(1,'Tom',67,88,95),(2,'Rose',23,66,90),(3,'Jack',56,98,76);

select
    id,
    name,
    (case when math>=85 then '优秀' when math>=60 then '及格' else '不及格' end)'数学',
    (case when english>=85 then '优秀' when english>=60 then '及格' else '不及格' end)'英语',
    (case when chinese>=85 then '优秀' when chinese>=60 then '及格' else '不及格' end)'语文'
from score;
```

### 4.约束

#### 4.1概述

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/38.png)

#### 4.2示例

```sql
create table user(
    id int primary key auto_increment comment '主键',
    name varchar(10) not null unique comment '姓名',
    age int check(age>0 && age<=120) comment '年龄',
    status char(1) default '1' comment '状态',
    gender char(1) comment '性别'
)comment '用户表';

-- 插入数据
-- id是主键，自动维护，不用手动插入。分别为1/2/3
insert into user(name,age,status,gender) values ('Tom1',19,'1','男'),('Tom2',25,'0','男');
insert into user(name,age,status,gender) values ('Tom3',19,'1','男');

insert into user(name,age,status,gender) values (null,19,'1','男');-- 无效，name不能为null
insert into user(name,age,status,gender) values ('Tom3',19,'1','男');-- 无效，name重复，不唯一

-- 虽然上面没有成功插入，但是提交了申请，所以id4被占用了，因此下面的是id5
insert into user(name,age,status,gender) values ('Tom4',80,'1','男');
insert into user(name,age,status,gender) values ('Tom5',-1,'1','男');-- 无效，年龄小于0了
insert into user(name,age,status,gender) values ('Tom5',121,'1','男');-- 无效，年龄大于120

insert into user(name,age,gender) values ('Tom5',120,'男');-- status默认值是1
```

#### 4.3外键约束

让两张表建立连接，从而保证数据的一致性和完整性

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/39.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/40.png)

![](https://github.com/Jomocool/MySQL/blob/main/MySQL-img/41.png)

```sql
-- 前面已经创建好了一张表emp
-- 添加外键
alter table emp add constraint fk_emp_dept_id foreign key(dept_id) refrences dept(id);
-- 创建外键约束后，不能随意删除父表的内容，因为关联到子表，从而保证了数据的一致性和完整性

-- 删除外键
alter table emp drop foreign key fk_emp_dept_id;

-- 删除/更新行为
alter table emp add constraint fk_emp_dept_id foreign key(dept_id) refrences dept(id) on update on delete cascade;
```

