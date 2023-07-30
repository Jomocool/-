# MySQL(小林coding)

## 一、基础篇

### 1.1 执行一条select语句，期间发生了什么？

#### 1.1.1 MySQL执行流程是怎样的？

MySQL执行一条SQL查询语句的流程：
![image-20230729174840366](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729174840366.png)

MySQL架构共分为两层：Server层和存储引擎层

- Server层负责建立连接、分析和执行SQL

  MySQL大多数的核心功能模块都在这实现，主要包括连接器、查询缓存、解析器、预处理器、优化器和执行器等。另外，所有的内置函数（如日期、时间、数学和加密函数等）和所有跨存储引擎的功能（如存储过程、触发器、视图等）都在Server层实现

- 存储引擎层负责数据的存储和提取

  支持InnoDB、MyISAM、Memory等多个存储引擎，不同的存储引擎共用一个Server层。现在最常用的存储引擎是InnoDB，从MySQL5.5版本开始，InnoDB成为了MySQL的默认存储引擎。常说的索引数组结构，解释由存储引擎层实现的，不同的存储引擎支持的索引类型也不相同，比如InnoDB支持索引类型是B+树，且是默认使用，也就是说在数据表中创建的主键索引和二级索引默认使用的是B+树索引

  

#### 1.1.2 第一步：连接器

如果在Linux操作系统里使用MySQL，第一步肯定是要先链接MySQL服务，然后才能执行SQL语句，普遍使用以下命令进行连接

```shell
#-h 指定MySQL服务的IP地址，如果是连接本地的MySQL服务，可以不同这个参数
#-u 指定用户名，管理员角色名为root
#-p 指定密码，如果命令行中不填写密码（为了密码安全，建议不要再命令行写密码），就需要在交互对话里面输入密码
mysql -h$ip -u$user -p
```

连接的过程需要先经过TCP三次握手，因为MySQL是基于TCP协议进行传输的，如果MySQL服务并没有启动，会收到如下报错：

![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/sql%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B/mysql%E8%BF%9E%E6%8E%A5%E9%94%99%E8%AF%AF.png)



如果MySQL服务正常运行，完成TCP连接的建立后，连接器就要开始验证你的用户名和密码，如果用户名和密码不对，就收到一个"Access denied for user"的错误，然后客户端程序执行结束

![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/sql%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B/%E5%AF%86%E7%A0%81%E9%94%99%E8%AF%AF.png)



如果用户密码都没有问题，连接器就会获取该用户的权限，然后保存起来，后续该用户在此连接里的任何操作，都会基于连接开始时读到的权限进行权限逻辑的判断



所以，如果一个用户已经建立了连接，即使管理员中途修改了该用户的权限，也不会影响已经存在的连接的权限。修改完成后，只有再新建的连接才会使用新的权限设置



> 如何查看MySQL服务被多少个客户单连接了？

执行`show processlist`命令查看

![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/sql%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B/%E6%9F%A5%E7%9C%8B%E8%BF%9E%E6%8E%A5.png)

上图中，两个用户名为root的用户连接了MySQL服务，其中id为6的用户的Command列的状态为Sleep，意味着该用户连接完MySQL服务就没有再执行过任何命令，也就是说这是一个空闲的连接，并且空闲的时间是736秒（Times列）



> 空闲连接会一直占着吗？

MySQL定义了空闲连接的最大空闲时长，由`wait_timeout`参数控制，默认值是8小时（28880秒），如果空闲连接超过了这个时间，连接器就会自动将它断开

```mysql
mysql> show variables like 'wait_timeout';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| wait_timeout  | 28800 |
+---------------+-------+
1 row in set (0.00 sec)
```

也可以自己手动断开连接，使用`kill connection+id`的命令

```mysql
mysql> kill connection +6;
Query OK, 0 rows affected (0.00 sec)
```

一个处于空闲状态的连接被服务端主动断开后，这个客户端并不会马上知道，等到客户端在发起下一个请求的时候，才会收到报错

“ERROR 2013 (HY000): Lost connection to MySQL server during query”



> MySQL的连接数有限制吗？

MySQL服务支持的最大连接数由`max_connections`参数控制，如果超过这个值，系统就会拒绝接下来的连接请求，并报错提示“Too many connections”

```mysql
mysql> show variables like 'max_connections';
+-----------------+-------+
| Variable_name   | Value |
+-----------------+-------+
| max_connections | 151   |
+-----------------+-------+
1 row in set (0.00 sec)
```

MySQL的连接也跟HTTP一样，有短连接和长连接的概念，它们的区别如下：

- 短连接

  连接mysql服务（TCP三次握手）

  执行sql

  断开mysql服务（TCP四次挥手）

- 长连接

  连接mysql服务（TCP三次握手）

  执行sql

  执行sql

  执行sql

  ....

  断开mysql服务（TCP四次挥手）

可以看到，使用长连接的好处就是可以减少建立连接和断开连接的过程，所以一般推荐使用长连接



但是，使用长连接之后可能占用内存增多，因为MySQL在执行查询过程中临时使用内存管理连接对象，这些连接对象资源只有在连接断开时才会释放。如果长连接累计很多，将导致MySQL服务占用内存太大，有可能会被系统强制杀掉，这样会发生MySQL服务异常重启的现象



> 怎么解决长连接占用内存的问题？

有两种解决方法：

1. 定期断开长连接

2. 客户端主动重置连接

   MySQL5.7版本实现了`mysql_reset_connection()`函数的接口，注意这是接口函数不是命令，当客户端执行了一个很大的操作后，在代码里调用mysql_reset_connection函数来重置连接，达到释放内存的效果。这个过程不需要重连和重新做权限认证，但是会将连接恢复到刚刚创建完时的状态



至此，连接器的工作做完了，简单总结：

- 与客户端进行TCP三次握手建立连接
- 校验客户端的用户名和密码，如果用户名或密码不对，则会报错
- 如果用户名和密码都对了，会读取该用户的权限，然后后面的权限逻辑判断都基于此时读取到的权限



#### 1.1.3 第二步：查询缓存

连接器的工作完成后，客户端就可以向MySQL服务发送SQL语句了，MySQL服务收到SQL语句后，就会解析出SQL语句的第一个字段，看看是什么类型的语句



如果SQL是查询语句（select语句），MySQL就会先去查询缓存（Query Cache）里查找缓存数据，看看之前有没有执行过这一条命令，这个查询缓存是以key-value形式保存在内存中的，key为SQL查询语句，value为SQL语句查询结果



如果查询的语句命中查询缓存，直接返回value给客户端。如果没有命中，就要继续往下执行，等执行完后，查询的结果就会被存入查询缓存中



查询缓存缺点：对于更新比较频繁的表，查询缓存的命中率很低，因为只要有一个表有更新操作，那么这个表的查询缓存就会被清空。如果刚缓存了一个结果很大的数据，还没被使用，刚好这个表有更新操作，查询缓存就被清空了，相当于缓存白做了



所以，MySQL8.0版本直接将查询缓存删掉了，从MySQL8.0开始，执行一条SQL查询语句，不会再走到查询缓存这个阶段了

对于MySQL8.0之前的版本，如果想关闭查询缓存，可以通过将参数`query_cache_type`设置成DEMAND

> TIP
>
> 这里说的查询缓存是 server 层的，也就是 MySQL 8.0 版本移除的是 server 层的查询缓存，并不是 Innodb 存储引擎中的 buffer pool。



#### 1.1.4 第三步：解析SQL

在正式执行SQL查询语句之前，MySQL会先对SQL语句做解析，这个工作交由解析器来完成



**解析器**

解析器会做如下两件事情：

1. 词法分析

   MySQL会根据你输入的字符串识别出关键字出来，构建出SQL语法树，方便后面模块获取SQL类型、表明、字段名、where条件等

2. 语法分析

   根据词法分析的结果，语法解析器会根据语法规则，判断你输入的SQL语句是否满足MySQL语法

如果输入的SQL语句语法不对，就会在解析器这个阶段报错，比如将from写成了form

![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/sql%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B/%E8%AF%AD%E6%B3%95%E9%94%99%E8%AF%AF.png)

但是，表不存在或者字段不存在，并不是在解析器里做的。解析器只负责构建语法树和检查语法，但是不会去查表或者字段存不存在



#### 1.1.5 第四步：执行SQL

每条`SELECT`查询语句流程主要可以分为下面这三个阶段：

- prepare阶段，也就是预处理阶段
- optimize阶段，也就是优化阶段
- execute阶段，也就是执行阶段



**预处理器**

预处理器做的事情：

- 检查SQL查询语句中的表或者字段是否存在
- 将`select *`中的`*`符号，扩展为表上的所有列



下面这条查询语句，test这张表是不存在的，这时MySQL就会在执行SQL查询语句的prepare阶段报错

```mysql
mysql> select * from test;
ERROR 1146 (42S02): Table 'mysql.test' doesn't exist
```

![image-20230729183653177](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729183653177.png)

![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/sql%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B/%E8%A1%A8%E4%B8%8D%E5%AD%98%E5%9C%A8.jpeg)

![image-20230729183701294](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729183701294.png)



**优化器**

`优化器主要负责将SQL查询语句的执行方案确定下来`，比如表里面有多个索引的时候，优化器会基于查询成本的考虑，来决定选择使用哪个索引

![image-20230729184118932](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729184118932.png)

![image-20230729184416715](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729184416715.png)

![image-20230729184541910](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729184541910.png)



> 为什么使用二级索引？

![image-20230729190112848](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729190112848.png)

可以理解为二级索引更加轻量级，查询起来更快一些，如果想要得到数据，只需将在二级索引中查询到的主键值代入到主键索引中获取数据即可



**执行器**

在执行过程中，执行器就会和存储引擎交互了，交互是以记录为单位的



**主键索引查询**

![image-20230729190535733](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729190535733.png)



**全表扫描**

![image-20230729190805844](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729190805844.png)



**索引下推**

![image-20230729190916105](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729190916105.png)

![image-20230729191048729](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729191048729.png)

每查询到一条age>20的记录，就要进行回表操作，将完整的记录返回给Server层，然后Server层再判断该记录的reward是否等于100000，成立就发送给客户端，否则跳过。然后继续从下一条记录开始重复上述操作，直到读完表中所有记录



![image-20230729191343161](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230729191343161.png)

可以理解为，不包含在联合索引(age,reward)里的条件，才执行回表操作，让Server去判断存储引擎过滤出的记录是否符合其它条件



#### 1.1.6 总结

执行一条SQL查询语句，期间发生了什么？

1. 连接器：建立连接、管理连接、校验用户身份
2. 查询缓存：查询语句如果命中查询缓存则直接返回，否则继续往下执行。MySQL8.0已删除该模块
3. 解析SQL：通过解析器对SQL查询语句进行词法分析、语法分析，然后构建语法树，方便后续模块读取表名、字段、语句类型
4. 执行SQL：执行SQL共有三个阶段：
   - 预处理阶段：检查表或字段是否存在；将`SELECT *`中的`*`符号扩展为表上的所有列
   - 优化阶段：基于查询成本考虑，选择查询成本最小的执行计划
   - 执行阶段：根据执行计划执行SQL查询语句，从存储引擎读取记录，返回给客户端



### 1.2 MySQL一行记录是怎么存储的？

#### 1.2.1 MySQL的数据存放在哪个文件？

MySQL的数据都是保存在磁盘的，具体保存在哪个文件呢？



MySQL存储的行为是由存储引擎实现的，MySQL支持多种存储引擎，不同的存储引擎保存的文件自然也不同

InnoDB是常用的存储引擎，也是MySQL默认的存储引擎。



MySQL数据库的文件存放在哪个目录？

```mysql
mysql> SHOW VARIABLES LIKE 'datadir';
+---------------+-----------------+
| Variable_name | Value           |
+---------------+-----------------+
| datadir       | /var/lib/mysql/ |
+---------------+-----------------+
1 row in set (0.00 sec)
```

每创建一个database都会在/var/lib/mysql/目录里面创建一个以database为名的目录，然后保存表结构和表数据的文件都会存放在这个目录里

![image-20230730110809188](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730110809188.png)



**表空间文件的结构是怎么样的？**

`表空间由段（segment）、区（extent）、页（page）、行（row）组成`，InnoDB存储引擎的逻辑存储结构大致如下：

![image-20230730111034703](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730111034703.png)

表空间里有多个段，每个段里面又有多个区，每个区里面又有多个页，每个页里面就是一行一行的数据了



1. 行（row）

   数据库表中的记录都是按行进行存放的，每行记录根据不同的行格式，有不同的存储结构

2. 页（page）

   记录是按照行来存储的，但是数据库的读取不以行为单位，否则一次读取（即一次I/O操作）只能处理一行数据，效率太低

   因此，InnoDB的数据是按页为单位来读写的，即当需要读一条记录的时候，并不是将这个行记录从磁盘读出来，而是以页为单位，将该行所在页整体读入内存

   默认每个页的大小为16KB，即最多能保证16KB的连续存储空间

   页是InnoDB存储引擎磁盘管理的最小单元，意味着数据库每次读写都是以16KB为单位的，一次最少从磁盘中读取16KB的内容到内存中，一次最好把内存中的16KB内容刷新到磁盘中

   页的类型有很多，常见的有数据页、undo日志页、溢出页等等。数据表中的行记录是用数据页来管理的

   总之记住表中的记录存储在数据页里面即可

3. 区（extent）

   InnoDB存储引擎是用B+树来组织数据的

   B+树中每一层都是通过双向链表连接起来的，如果是以页为单位来分配存储空间，那么链表中相邻的两个页之间的物理位置并不是连续的，可能离得非常远，那么磁盘查询时就会有大量的随机I/O，随机I/O是非常慢的

   解决方法是让链表中相邻的页的物理位置也相邻，这样就可以顺序I/O了，在范围查询（扫描叶子结点）的时候性能就会很高

   具体解决步骤：

   `在表中数据量大的时候，为某个索引分配空间的时候就不再按照页为单位分配了，而是按照区为单位分配（刚好对内存的需求量也大，干脆就直接分配一块大空间内存就好了，这样页与页之间物理位置恰好也是连续的）。每个区的大小为1MB，对于16KB的页来说，连续的64个页会被划为一个区，这样就使得链表中相邻的页的物理位置也相邻，就能使用顺序I/O了`

4. 段（segment）

   表空间是由各个段组成的，段是由多个区组成的，段一般分为数据段、索引段和回滚段等

   - 索引段：存放B+树的非叶子节点的区的集合
   - 数据段：存放B+树的叶子结点的区的结合
   - 回滚段：存放的是回滚数据的区的集合



#### 1.2.2 InnoDB行格式有哪些？

行格式（row_format），就是一条记录的存储结构

InnoDB提供了4种行格式，分别是Redundant、Compact、Dynamic和Compressed行格式

![image-20230730112757095](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730112757095.png)



#### 1.2.3 COMPACT行格式长什么样？

![image-20230730112842699](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730112842699.png)



**记录的额外信息**

记录的额外信息包含3个部分：变长字段长度列表、NULL值列表、记录头信息

- `变长字段长度列表`

  varchar(n)和char(n)的区别是char是定长的，而varchar是变长的，变长字段实际存储的数据的长度（大小）不固定的

  所以，在存储数据的时候，也要把数据占用的大小存起来，存到`变长字段长度列表`里面，读取数据的时候根据这个`变长字段长度列表`去读取对应长度的数据，其他TEXT、BLOB等变长字段也是这么实现的

  ![image-20230730113245323](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730113245323.png)

  ![image-20230730113541260](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730113541260.png)

  ![image-20230730113601779](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730113601779.png)

  > 为什么`变长字段长度列表`的信息要按照逆序存放？

  主要是因为`记录头信息`中指向下一个记录的指针，指向的是下一条记录的`记录头信息`和`真实数据`之间的位置，这样的好处就是向左读就是`记录头信息`，向右读就是`真实数据`，比较方便

  `变长字段长度列表`中的信息之所以要逆序存放，是因为这样可以`使得位置靠前的记录的真实数据和数据对应的字段长度信息可以同时在一个CPU Cache Line中（二者相距越近，就越有可能分配到同一个CPU Cache Line中），可以提高CPU Cache的命中率`

  同理，NULL值列表也需要逆序存放

  > 每个数据库表的行格式都有`变长字段长度列表`吗？

  变长字段长度列表不是必需的

  `当数据表没有变长字段的时候，比如全部都是int类型的字段，这时候表里的行格式就不会有变长字段长度列表了`，因为没有必要，比如去掉以节省空间

  所以`变长字段长度列表`只出现在数据库表有变长字段的时候

- `NULL值列表`

  表中的某些列可能会存储NULL值，如果把这些NULL值都放到记录的真实数据中会比较浪费空间，所以Compact行格式就把这些值为NULL的列存储到NULL值列表中

  如果存在允许NULL值的列，则每一个列对应一个二进制位bit，二进制位按照列的顺序逆序排列

  - 二进制位的值为1时，代表该列的值为NULL
  - 二进制位的值为0时，代表该列的值不为NULL

  另外，NULL值列表必须用整数个字节的位表示（一字节8位），如果使用的二进制位个数不足整数个字节，则在字节的高位补0

  ![image-20230730114752833](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730114752833.png)

  先看第一条记录，不存在值为NULL的列

  ![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/row_format/null%E5%80%BC%E5%88%97%E8%A1%A81.png)

  但是InnoDB是用整数字节的二进制位来表示NULL值列表的，现在不足8为，所以要在高位补0

  ![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/row_format/null%E5%80%BC%E5%88%97%E8%A1%A82.png)

  所以，对于第一条数据，NULL值列表用十六进制表示是0x00

  接下来看第二条记录，用十六进制表示是0x04

  ![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/row_format/null%E5%80%BC%E5%88%97%E8%A1%A83.png)

  最后是第三条记录，用十六进制表示是0x06

  ![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/row_format/null%E5%80%BC%E5%88%97%E8%A1%A84.png)

  把三条记录的NULL值列表填充完毕后，它们的行格式如下：

  ![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/row_format/null%E5%80%BC%E5%88%97%E8%A1%A85.png)

  > 每个数据库表的行格式都有`NULL值列表`吗？

  NULL值列表也不是必需的

  `当数据表的字段都定义成NOT NULL的时候，这时候表里的行格式就不会有NULL值列表了`

  所以在设计数据库表的时候，通常都是将字段设置为NOT NULL，这样至少可以节省1字节的空间（NULL值列表至少占用1字节空间）

  > `NULL值列表`是固定1字节空间吗？如果这样的话，一条记录有9个字段值都是NULL，这时候怎么表示？

  `NULL值列表`不是固定1字节的

  当一条记录有9个字段值都是NULL，那么就会创建2字节的空间的`NULL值列表`，高位补0

- `记录头信息`

  ![image-20230730115626521](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730115626521.png)



**记录的真实数据**

记录真实数据除了我们定义的字段，还有三个隐藏字段，分别为：row_id、trx_id、roll_pointer

![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/row_format/%E8%AE%B0%E5%BD%95%E7%9A%84%E7%9C%9F%E5%AE%9E%E6%95%B0%E6%8D%AE.png)

- `row_id`

  如果建表的时候指定了主键或者唯一约束，那么就没有row_id隐藏字段了。如果既没有指定主键，又没有唯一约束，那么InnoDB就会为记录添加row_id隐藏字段。row_id不是必需的，占用6个字节

- `trx_id`

  事物id，表示这个数据是由哪个事物生成的。trx_id是必需的，占用6个字节

- `roll_pointer`

  这条记录是上个版本的指针。roll_pointer是必须的，占用7个字节



#### 1.2.4 varchar(n)中n最大值为多少？

`MySQL 规定除了 TEXT、BLOBs 这种大对象类型之外，其他所有的列（不包括隐藏列和记录头信息）占用的字节长度加起来不能超过 65535 个字节`

注意是一行的总长度不超过65535字节，而不是一列



varchar(n)字段类型的n代表的是最多存储的字符数量，并不是字节大小

要算varchar(n)最大能允许存储的字节数，还要看数据库表的字符集，因为字符集代表着1个字符要占用多少字节。比如ASCII字符集，1个字符占用1字节，那么varchar(100)意味着最大能允许存储100字节的数据



**单字段的情况**

![image-20230730121707861](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730121707861.png)

![image-20230730121834584](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730121834584.png)

![image-20230730122254423](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730122254423.png)

255=15*16+15，1个十六进制数占用1字节，能够表示0~255，所以对于占用0~255字节的变长字段，只需1个占用1字节的十六进制数即可，所以变长字段长度列表占用字节数是1

![image-20230730122603319](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730122603319.png)



**多字段的情况**

`如果有多个字段的话，需要保证所有字段的长度+变长字段字节数列表所占用的字节数+NULL值列表所占用的字节数<=65535`

![img](https://cdn.xiaolincoding.com/gh/xiaolincoder/mysql/row_format/%E5%A4%9A%E5%AD%97%E6%AE%B5%E7%9A%84%E6%83%85%E5%86%B5.png)



#### 1.2.5 行溢出后，MySQL是怎么处理的？

![image-20230730122933026](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730122933026.png)

![image-20230730122956946](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730122956946.png)



#### 1.2.6 总结

![image-20230730123128125](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730123128125.png)

![image-20230730123145319](https://md-jomo.oss-cn-guangzhou.aliyuncs.com/IMG/image-20230730123145319.png)
