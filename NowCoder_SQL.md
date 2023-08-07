## 一、基础查询

### 基础查询

#### SQL1 查询所有列

```mysql
#题目：现在运营想要查看用户信息表中所有的数据，请你取出相应结果
select *
from user_profile;
```

#### SQL2 查询多列

```mysql
#题目：现在运营同学想要用户的设备id对应的性别、年龄和学校的数据，请你取出相应数据
select device_id,gender,age,university
from user_profile;
```

### 简单处理查询结果

#### SQL3 查询结果去重

```mysql
#题目：现在运营需要查看用户来自于哪些学校，请从用户信息表中取出学校的去重数据。
#distinct column_name:对该列去重
select distinct university
from user_profile;
```

#### SQL4 查询结果限制返回行数

```mysql
#题目：现在运营只需要查看前2个用户明细设备ID数据，请你从用户信息表 user_profile 中取出相应结果。
#limit:limit子句后面跟着两个参数，第一个参数用于指定第一个返回行记录的偏移量，第二个参数指定需要几行记录
#limit 5 5:返回行6~10
#limit 5 -1:返回行6~最后一条
#limit 5:返回前5行
select device_id
from user_profile
order by id
limit 2;
```

#### SQL5 将查询后的列重新命名

```mysql
#题目：现在你需要查看前2个用户明细设备ID数据，并将列名改为 'user_infos_example',，请你从用户信息表取出相应结果。
#as可省略
select device_id as user_infos_example
from user_profile
order by id
limit 2;
```

## 二、条件查询

### 基础排序

#### SQL36 查找后排序

```mysql
#题目：现在运营想要取出用户信息表中的用户年龄，请取出相应数据，并按照年龄升序排序。
select device_id,age
from user_profile
order by age asc;
```

#### SQL37 查找后多列排序

```mysql
#题目：现在运营想要取出用户信息表中的年龄和gpa数据，并先按照gpa升序排序，再按照年龄升序排序输出，请取出相应数据。
#不需要两个order by，一个order by即可，然后两个需要排序的字段用逗号隔开，顺序是从左到右
select device_id,gpa,age
from user_profile
order by gpa asc,age asc;
```

#### SQL38 查找后降序排列

```mysql
#题目：现在运营想要取出用户信息表中对应的数据，并先按照gpa、年龄降序排序输出，请取出相应数据。
select device_id,gpa,age
from user_profile
order by gpa desc,age desc;
```

### 基础操作符

#### SQL6 查找学校是北大的学生信息

```mysql
#题目：现在运营想要筛选出所有北京大学的学生进行用户调研，请你从用户信息表中取出满足条件的数据，结果返回设备id和学校。
select device_id,university
from user_profile
where university='北京大学';
```

#### SQL7 查找年龄大于24岁的用户信息

```mysql
#题目：现在运营想要针对24岁以上的用户开展分析，请你取出满足条件的设备ID、性别、年龄、学校。
select device_id,gender,age,university
from user_profile
where age>24;
```

#### SQL8 查找某个年龄段的用户信息

```mysql
#题目：现在运营想要针对20岁及以上且23岁及以下的用户开展分析，请你取出满足条件的设备ID、性别、年龄。
select device_id,gender,age
from user_profile
where age between 20 and 23;
```

#### SQL9 查找除复旦大学的用户信息

```mysql
#题目：现在运营想要查看除复旦大学以外的所有用户明细，请你取出相应数据
select device_id,gender,age,university
from user_profile
where university != '复旦大学';
```

#### SQL10 用where过滤空值练习

```mysql
#题目：现在运营想要对用户的年龄分布开展分析，在分析时想要剔除没有获取到年龄的用户，请你取出所有年龄值不为空的用户的设备ID，性别，年龄，学校的信息。

#解法1
select device_id,gender,age,university
from user_profile
where age;
#解法2
select device_id,gender,age,university
from user_profile
where age is not NULL;
#解法3
select device_id,gender,age,university
from user_profile
where age!='';
```

### 高级操作符

#### SQL11 高级操作符练习（1）

```mysql
#题目：现在运营想要找到男性且GPA在3.5以上(不包括3.5)的用户进行调研，请你取出相关数据。
select device_id,gender,age,university,gpa
from user_profile
where gender='male' and gpa>3.5;
```

#### SQL11 高级操作符练习（1）

```mysql
#题目：现在运营想要找到学校为北大或GPA在3.7以上(不包括3.7)的用户进行调研，请你取出相关数据（使用OR实现）
select device_id,gender,age,university,gpa
from user_profile
where university='北京大学' or gpa>3.7;
```

#### SQL13 Where in和Not in

```mysql
#题目：现在运营想要找到学校为北大、复旦和山大的同学进行调研，请你取出相关数据。
select device_id,gender,age,university,gpa
from user_profile
where university in ('北京大学','复旦大学','山东大学');
```

#### SQL14 操作符混合运用

```mysql
#题目：现在运营想要找到gpa在3.5以上(不包括3.5)的山东大学用户 或 gpa在3.8以上(不包括3.8)的复旦大学同学进行用户调研，请你取出相应数据
select device_id,gender,age,university,gpa
from user_profile
where (university='山东大学' and gpa>3.5)
or (university='复旦大学' and gpa>3.8);
```

#### SQL15 查看学校名称中含北京的用户

```mysql
#题目：现在运营想查看所有大学中带有北京的用户的信息，请你取出相应数据。
select device_id,age,university
from user_profile
where university like '%北京%';
```

## 三、高级查询

### 计算函数

#### SQL16 查找GPA最高值

```mysql
#题目：运营想要知道复旦大学学生gpa最高值是多少，请你取出相应数据

#方法一：order by,limit
select gpa
from user_profile
where university='复旦大学'
order by gpa desc
limit 1;
#方法二：max()
select max(gpa) as gpa
from user_profile
where university='复旦大学';
```

#### SQL17 计算男生人数以及平均GPA

```mysql
#题目：现在运营想要看一下男性用户有多少人以及他们的平均gpa是多少，用以辅助设计相关活动，请你取出相应数据。
select count(gender) as male_num,avg(gpa) as avg_gpa
from user_profile
where gender='male';
```

### 分组查询

#### SQL18 分组计算练习题

```mysql
#题目：现在运营想要对每个学校不同性别的用户活跃情况和发帖数量进行分析，请分别计算出每个学校每种性别的用户数、30天内平均活跃天数和平均发帖数量。
问题分解：
1. 限定条件：无
2. 每个学校每种性别：按性别和学校分组(group by gender,university)
3. 用户数(count(device_id))
4. 30天内平均活跃天数(保留1位小数)(round(avg(active_days_within_30),1) as avg_active_day)
5. 平均发帖数量(保留一位小数)(round(avg(question_cnt),1) as avg_question_cnt)

select 
    gender,university,
    count(device_id) as user_num,
    round(avg(active_days_within_30),1) as avg_active_day,
    round(avg(question_cnt),1) as avg_question_cnt
from user_profile
group by gender,university;
```

#### SQL19 分组过滤练习题

```mysql
#题目：现在运营想查看每个学校用户的平均发贴和回帖情况，寻找低活跃度学校进行重点运营，请取出平均发贴数低于5的学校或平均回帖数小于20的学校。
#由于本题是按学校来统计的，所以需要先分组再过滤，因此应该用group by,having组合，而不是where,group by组合了，以上二者的顺序是不可逆的

select 
    university,
    round(avg(question_cnt),3) as avg_question_cnt,
    round(avg(answer_cnt),3) as avg_answer_cnt
from user_profile
group by university
having avg_question_cnt<5 or avg_answer_cnt<20;#可以直接利用上面已经计算过的值
```

#### SQL20 分组排序练习题

```mysql
#题目：现在运营想要查看不同大学的用户平均发帖情况，并期望结果按照平均发帖情况进行升序排列，请你取出相应数据。
select
    university,
    round(avg(question_cnt),4) as avg_question_cnt
from user_profile
group by university
order by avg_question_cnt;
```

