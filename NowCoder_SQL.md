## 一、基础查询

### 基础查询

#### SQL1 查询所有列

```mysql
#题目：现在运营想要查看用户信息表中所有的数据，请你取出相应结果
select * from user_profile;
```

#### SQL2 查询多列

```mysql
#题目：现在运营同学想要用户的设备id对应的性别、年龄和学校的数据，请你取出相应数据
select device_id,gender,age,university from user_profile;
```

### 简单处理查询结果

#### SQL3 查询结果去重

```mysql
#题目：现在运营需要查看用户来自于哪些学校，请从用户信息表中取出学校的去重数据。
#distinct column_name:对该列去重
select distinct university from user_profile;
```

#### SQL4 查询结果限制返回行数

```mysql
#题目：现在运营只需要查看前2个用户明细设备ID数据，请你从用户信息表 user_profile 中取出相应结果。
#limit:limit子句后面跟着两个参数，第一个参数用于指定第一个返回行记录的偏移量，第二个参数指定需要几行记录
#limit 5 5:返回行6~10
#limit 5 -1:返回行6~最后一条
#limit 5:返回前5行
select device_id from user_profile order by id limit 2;
```

#### SQL5 将查询后的列重新命名

```mysql
#题目：现在你需要查看前2个用户明细设备ID数据，并将列名改为 'user_infos_example',，请你从用户信息表取出相应结果。
#as可省略
select device_id as user_infos_example from user_profile order by id limit 2;
```

