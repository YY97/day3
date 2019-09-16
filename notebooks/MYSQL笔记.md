# 数据库

# 一、数据库的定义以及他的发展史

 数据库（Database）是按照数据结构来组织、存储和管理数据的仓库。

 每个数据库都有一个或多个不同的 API 用于创建，访问，管理，搜索和复制所保存的数据。

 我们也可以将数据存储在文件中，但是在文件中读写数据速度相对较慢。

  所以，现在我们使用关系型数据库管理系统（RDBMS）来存储和管理的大数据量。所谓的关系型数据库，是建立在关系模型基础上的数据库，借助于集合代数等数学概念和方法来处理数据库中的数据。 

 RDBMS 即关系数据库管理系统(Relational Database Management System)的特点：

- 1.数据以表格的形式出现
- 2.每行为各种记录名称
- 3.每列为记录名称所对应的数据域
- 4.许多的行和列组成一张表单
- 5.若干的表单组成database

## １、开始阶段

所有数据都是储存在文件中的，安全性低，操作性繁琐

## ２、层次模型

- 优点：

  ​	查询分类的效率比较高

- 缺点:

  ​	没有导航结构，导致分类困难

  ​	数据不完整

- 注意：数据的不完整，如果不能准确的分辨两条数据有什么不同，称之为失去了‘数据的完整性’

## ３、网状模型

网状模型:没有解决导航问题，解决了数据完整性问题

## ４、关系模型

特点：

- 每张表都是独立的，没有导航结构

- 表与表之间会建立公共字段，也就是将两张表之间建立了关系

  **注意:** 公共的字段名可以不一样, 但是数据类型必须相同(数据类型相同的不一定是公共字段), 两个字段的含义必须也要一致.
  关系型数据库, 解决了了数据的完整性, 也解决导航问题, 但是带来的是低效率.
  NOSQL(非关系型数据库): MongoDB, Redis

## ５、ＭｙＳＱＬ数据库

 MySQL 是一个关系型数据库管理系统，由瑞典 MySQL AB 公司开发，目前属于 Oracle 公司。MySQL 是一种关联数据库管理系统，关联数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。 

- MySQL 是开源的，所以你不需要支付额外的费用。
- MySQL 支持大型的数据库。可以处理拥有上千万条记录的大型数据库。
- MySQL 使用标准的 SQL 数据语言形式。
- MySQL 可以运行于多个系统上，并且支持多种语言。这些编程语言包括 C、C++、Python、Java、Perl、PHP、Eiffel、Ruby 和 Tcl 等。
- MySQL 对PHP有很好的支持，PHP 是目前最流行的 Web 开发语言。
- MySQL 支持大型数据库，支持 5000 万条记录的数据仓库，32 位系统表文件最大可支持 4GB，64 位系统支持最大的表文件为8TB。
- MySQL 是可以定制的，采用了 GPL 协议，你可以修改源码来开发自己的 MySQL 系统。

# 二、数据库的相关术语和概念

- **数据库:** 数据库是一些关联表的集合。
- **数据表:** 表是数据的矩阵。在一个数据库中的表看起来像一个简单的电子表格。
- **列:** 一列(数据元素) 包含了相同类型的数据, 例如邮政编码的数据。
- **行：**一行（=元组，或记录）是一组相关的数据，例如一条用户订阅的数据。
- **冗余**：存储两倍数据，冗余降低了性能，但提高了数据的安全性。
- **主键**：主键是唯一的。一个数据表中只能包含一个主键。你可以使用主键来查询数据。
- **外键：**外键用于关联两个表。
- **复合键**：复合键（组合键）将多个列作为一个索引键，一般用于复合索引。
- **索引：**使用索引可快速访问数据库表中的特定信息。索引是对数据库表中一列或多列的值进行排序的一种结构。类似于书籍的目录。
- **参照完整性:** 参照的完整性要求关系中不允许引用不存在的实体。与实体完整性是关系模型必须满足的完整性约束条件，目的是保证数据的一致性。

# 三、Ｌｉｎｕｘ数据库的开启和链接

### １、安装数据库

```
sudo apt install -y mysql-server mysql-client
```

### ２、开启数据库服务

1. Ubuntu : service mysql start|stop|restart|status
2. Deepin : systemctl start|stop|restart|status mysqld
3. CentOS7 : systemctl start|stop|restart|status mysqld
4. CentOS6 : service mysqld start|stop|restart|status

### ３、连接数据库

各个Ｌｉｎｕｘ系统链接数据库都一样

**语法：sudo mysql -h localhost -p3306 -u root**

1. -h : host(ip地址) localhost = 127.0.0.1
2. -u : username(用用户账户)
3. -p : password(密码)
4. -P : port(端口口, 默认端口口3306)

**备注：**第一次使用 root 连接后最好添加一个新的用户来操作。出于安全考虑,日常开发中最好不不要使用 root

```
-- 创建新用用户,并设置密码
-- *.* 代表该用用户可以操作任何库、任何表
-- 主机名可以使用用 '%', 代表允许该用户从任何机器器登陆
GRANT ALL PRIVILEGES on *.* to '用户名'@'主机'　IDENTIFIED BY "密码" WITH GRANTOPTION;
-- 刷新使权限生生效
flush privileges;
```

### ４、退出数据库

四种方式效果一样:

1. exit
2. quit
3. \q
4. 快捷键: ctrl + d

### ５、密码忘记该怎么办？

1. 打开配置: vim    /etc/mysql/my.cnf

2. 添加一段:

  ```
  [mysqld]
  
  skip-grant-tables
  ```

  如果文件中已存在 [mysqld] , 则直接将 skip-grant-tables 写到其下方即可。

3. 修改完成后,保存退出,重启服务: sudo systemctl restart mysqld

# 四、ＳＱＬ语言概览

SQL 全拼为 Structured Query Language, 即 “结构化查询语言”。

SQL 是一种特殊目的的编程语言,是一种数据库查询和程序设计语言,用于存取数据以及查询、更新和管理关系数据库系统;同时也是数据库脚本文件的扩展名。

**关系型数据**

数据库						ＳＱＬ类型			公司

Ａｃｃｅｓｓ					ＳＱＬ				微软

ＳＱＬ－Ｓｅｒｖｅｒ			Ｔ－ＳＱＬ			微软

Ｏｒａｃｌｅ					ＰＬ/ＳＱＬ			甲骨文

MyＳＱＬ					ＭｙＳＱＬ			甲骨文

ＳＱＬite				内嵌小型数据库		移动端用的多

# 五、数据库的操作

## １、创建数据库　

```
create database [if not exists] `数据库名` charset=字符编码(utf8mb4);
```

**注意：**

1. 如果多次创建会报错
2. 字符编码不指定默认 utf8mb4
3. 给数据库命名一定要习惯性加上反引号, 防止和关键字冲突

## ２、查看数据库

```
show databases;
```

## ３、选择数据库

```
use `数据库的名字`;
```

## ４、修改数据库

```
-- 只能修改字符集
alter database `数据库名` charset=字符集;
```

## ５、删除数据库

```
drop database [if exists] `数据库的名字`;
```

# 六、表的操作

表是建立在数据库中的数据结构,是一类数据的存储集

## １、表的创建

```
create table <表名> ([表定义选项]) engine=myisam charaset=utf8mb4
```

其中，`[表定义选项]`的格式为：

```
<列名1> <类型1> [,…] <列名n> <类型n>
```

create table 命令语法比较多，其主要是由表创建定义（create-definition）、表选项（table-options）和分区选项（partition-options）所组成的。

-  create table：用于创建给定名称的表，必须拥有表CREATE的权限。
-  <表名>：指定要创建表的名称，在 CREATE TABLE 之后给出，必须符合标识符命名规则。表名称被指定为  db_name.tbl_name，以便在特定的数据库中创建表。无论是否有当前数据库，都可以通过这种方式创建。在当前数据库中创建表时，可以省略  db-name。如果使用加引号的识别名，则应对数据库和表名称分别加引号。例如，'mydb'.'mytbl' 是合法的，但  'mydb.mytbl' 不合法。
-  <表定义选项>：表创建定义，由列名（col_name）、列的定义（column_definition）以及可能的空值说明、完整性约束或表索引组成。
-  默认的情况是，表被创建到当前的数据库中。若表已存在、没有当前数据库或者数据库不存在，则会出现错误

```
提示：使用 CREATE TABLE 创建表时，必须指定以下信息：
1、要创建的表的名称不区分大小写，不能使用SQL语言中的关键字，如DROP、ALTER、INSERT等。
２、数据表中每个列（字段）的名称和数据类型，如果创建多个列，要用逗号隔开。
```



## ２、查看所有的表

选择数据库后，才可以查看表

```
show tables;
```

## ３、删除表

删除表必须在数据库中删除

```
drop table [if exists] `表名`
```

## ４、显示建表结构

```
desc `表名`;
describe `表名`;
```

## ５、修改表

```
-- 修改表的名称
alter table `old_name` rename `new_name`;
-- 修改表的引擎
alter table `表名` engine = innodb|myisam;
-- 移动表 到指定的数据库
alter table `表名` rename to 数据库名.表名;
```

## ６、修改字段

```
-- 增加一个新的字段
alter table `表名` add `字段名` 数据类型 属性;
-- 增加一个新的字段, 并放在首位
alter table `表名` add `字段名` 数据类型 属性 first;
-- 增加一个新的字段, 并放在某一个字段之后
alter table `表名` add `字段名` 数据类型 属性 after 指定字段;
-- 修改字段的属性
alter table `表名` modify `字段名` 数据类型 属性;
-- 修改字段的名称
alter table `表名` change `原字段名` `新的字段名` 数据类型 属性;
-- 修改字段的位置
alter table `表名` change `原字段名` `新的字段名` 数据类型 after `指定字段`;
-- 删除字段
alter table `表名` drop `字段名`;
```

## ７、复制表

### (1)先创建一个表，并且在表中插入一些数据

```
/* 创建 abc 表*/
create table abc(
    id int primary key auto_increment comment '主键',
    username char(32) not null comment '账户',
    password char(32) not null comment '密码'
) engine=myisam;

/* 插入入两条数据 */
insert into abc values(null, 'tom', md5(123456)), (null, 'bob',md5(123456));
```

### (2)复制表，并且复制数据

- 执行：

```
create table `复制表的名称` select * from `原表名`;
```

- 特点：完整的复制一个表，既有原来表的结构，又有原来表的数据

### (3)仅复制原来表的结构，不复制数据

- 执行

```
create table `复制表的名称` like `原表名`;
```

- 特点;复制后的表结构与原来的表相同，但是里面没有数据，是一张空的表
- 可以单独复制

```
insert into `复制表的名称` select * from `原表名`;
```

# 数据库和表的操作总结

```
增
    数据库: create database `库名`;
    表: create table `表名`;
    字段: alter table `表名` add `字段名` 类型 [属性];
    数据: insert into `表名`;

删
    数据库: drop database `库名`;
    表: drop  table `表名`;
    字段: alter table `表名` drop `字段名`;
    数据: delete from `表名` where ...;

改
    数据库: alter database `库名` ...;
    表: alter table `表名` ...;
    字段: alter table `表名` modify | change ...;
    数据: update `表名` set ...;

查
    数据库: show database [like ...];
    表: show tables [like ...];
    字段: desc `表名`;
    数据: select * from `表名` where ...;
```

# 七、字符集

## １、字符集在什么时候可以发挥作用？

- 保存数据的时候需要使用字符集
- 数据传输的时候也需要使用字符集
- 在存续的时候使用字符集
  - 在ＭｙＳＱＬ的服务器上，ｚａｉ数据库中，在表的使用上，在字段的位置上
  - 在服务器安装的是时候，可以指定默认的字符集

## ２、常见字符集

- ASCLL:基于罗马字母表的一套字符集，它采用１个字节的低７位表示字符，高位始终为０
- LATIN1:相对于ASCLL字符集做了扩展，仍然使用一个字节表示字符，但是启用了高位，扩展了字符集的展示范围
- GB2312:简体中文字符，一个汉子最多占用２个字节
- GB:只是所有的中文字符，一个汉子最多占用个字节
- UTF8:国际通用编码，一个汉子最多占用３个字节
- UTF8MB4:国际通用编码，在utf8的基础上加强了对新文字识别，一个汉字最多占用４个字节

```
/* gbk字符集最大大字符串串⻓长度: 65535/2 -1 */
create table test(
	text varchar(32766)
) charset=gbk;

/* utf8字符集最大大字符串串⻓长度: 65535/3 -1 */
create table test1(
	text varchar(21844)
) charset=utf8;

/* utf8mb4字符集最大大字符串串⻓长度: 65535/4 -1 */
create table test4(
	text varchar(16382)
) charset=utf8mb4;
```

## ３、查看当前MYSQL系统支持的字符集

```
mysql> show variables like 'character_%';

/* 输出:
+--------------------------+------------+
| Variable_name				| Value		|
+--------------------------+------------+
| character_set_client| utf8mb4 | 客户端来源数据使用用的字符集
| character_set_connection | utf8mb4 | 连接层字符集
| character_set_database| utf8mb4| 当前选中的数据库的默认字符集
| character_set_filesystem | binary | 文文件系统字符集
| character_set_results | utf8mb4 | 查询结果使用用的字符集
| character_set_server | utf8mb4 | 默认的内部操作字符集
| character_set_system | utf8 | 系统元数据(字段名、表名等)的字符集
| character_sets_dir | /usr/lo... |
+--------------------------+------------+
*/
```

## ４、修改当前的mysql系统的字符集编码

- 全部修改

```
set names gbk;
```

- 指定修改

```
set character_set_client = gbk;
set character_set_results = gbk;
```

- 它是临时性的命令，mysql链接断开以后，再次链接时会恢复原状

## ５、校对集

在某一种字符集下, 为了使字符之间可以互相比较, 让字符和字符形成一种关系的集合, 称之为校对集。
比如说 ASCII 中的 a 和 B, 如果区分大小写 a > B, 如果不区分 a < B;
不同字符集有不同的校对规则, 命名约定:以其相关的字符集名开始, 通常包括一个语言名, 并且以
_ci 、 _cs 或 _bin 结束。

- _ci：大小写不敏感
- _cs:大小写敏感
- _bin: binary  collation 二元法，直接比较字符的编码，可以认为是区分大小写的，因为在字符集中‘Ａ’和‘ａ’的编码是显然不同的

```
/* 数据库默认的排序方式,是升序 */
create table t1(
	str char(1)
) charset=utf8mb4 collate=utf8mb4_general_ci;
-- _general_ci 后缀的都是不区分大小写的
create table t2(
	str char(1)
) charset=utf8mb4 collate=utf8mb4_bin;
-- 看到后缀边是_bin的都是区分大小的
```

```
/*
Linux中Mysql是区分大小的
需要自己去配置
vim /etc/my.cnf
找到[mysqld]
1是不区分大小写,0是区分大小写
*/
lower_case_table_names=1
```

```
show character set; -- 查看字符集 和 校对集
show collation; -- 显示所有的校对集
```

# 八、Ｍysql的数据类型

## １、整形

![](/home/shenyang/Pictures/1.png)

- **一个无符号数一定是非负数**

```
create table t3(
	age tinyint unsigned
);
```

- **显示宽度(zerofill)**

整形显示宽度，位数不足时用０填充

```
create table t4(
    id int(10) zerofill primary key auto_increment,
    name char(32)
);
insert into t4 values(12345, '5个');
insert into t4 values(1234567890, '10个');
insert into t4 values(123456789012, '12个');
select * from t4;
```

## ２、浮点型

![](/home/shenyang/Pictures/7.png)

定位数的位数更加长

使用的方法：

- float(M,D)
- double(M,D)
- decimal(M,D)
- M是支持多少个长度，Ｄ是小数点后面的位数

```
create table t5 (
    a float(10, 2),
    b double(10, 2),
    c decimal(10, 2)
);
```

## ３、字符串类型

![](/home/shenyang/Pictures/2.png)

**char varchar的区别**：

------

| Type       | iNPUT     | saved in DB | Size       | Desc                                   |
| ---------- | --------- | ----------- | ---------- | -------------------------------------- |
| CHAR(5)    | "a"       | "a  "       | 5   bytes  | 固定占５个字节，不足的用空格补齐       |
| VARCHAR(5) | "a"       | "a"         | 2    bytes | 字符占１字节，额外用１字节记录位长     |
| CHAR(5)    | "abc  "   | "abc   "    | 5  bytes   | 保留结尾空格，仍然占５个字节           |
| VARCHAR(5) | "abc   "  | "abc"       | 4    bytes | 删除结尾空格，再加位长记录，共占４字节 |
| CHAR(5)    | "abcdefg" | "abcde"     | 5   bytes  | 截掉超出的字符，依然占用５字节         |
| VACHAR(5)  | "abcdefg" | "abcde"     | 6   bytes  | 截掉超出的字符，在加位长记录，共６字节 |

**思考:**
字符串、浮点型等都可以随意指定大小, 那么是不是平时操作的时候随意指定一个就可以呢?
答:不是, 数据类型并不是越大越好, 越大的类型会造成数据臃肿, 存储空间占用过大, 数据检索也会变慢

## ４、枚举(enum)

多选一的时候使用的一种数据类型，子前段使用单选框的时候，枚举类型可以发挥作用

枚举类型的优点:

- 限制值
- 节省空间
- 运行效率高

```
create table t6(
    name varchar(32),
    sex enum('男','女','保密') default 3
);
-- 枚举类型的计数默认从1开始
insert into t6 set name='张三',sex=1;
```

## ５、集合(set)

SET最多可以有64个不同的成员。类似于复选框, 有多少可以选多少。

```
create table t7 (
    name varchar(32),
    hobby set('吃','睡','玩','喝喝','抽')
);

insert into t7 values('张三','睡,抽,玩,吃,喝喝');
insert into t7 values('李李四','睡,抽');
```

- 为什么不是用set类型？

  在现在网站开发中，多选框的值有上千个，值存储的空没有索引用的多

- 那么复选框的问题怎么解决？

  将复选框单独设计成一张表

## ６、时间类型

![](/home/shenyang/Pictures/3.png)

### (1)datetime

```
create table datetime_test (
	create_at datetime
);
insert into datetime_test values('2019-4-2 16:54:00');
insert into datetime_test values('2019/4/2 16:54:00');
insert into datetime_test values(now());
-- 年份最大支持4个⻓度
insert into datetime_test values('10000/4/2 16:54:00');　－－错误
insert into datetime_test values('9999/4/2 16:54:00');
```

### (2)time

```
create table time_test (
	create_at time
);
insert into time_test values('12:12:12');
insert into time_test values('100:12:12');
insert into time_test values('-100:12:12');
insert into time_test values('10 10:12:12');
-- -838:59:59 - 838:59:59
insert into time_test values('839:12:12'); -- 错误的
```

### (3)timestamp时间戳类型

- 时间戳类型在显示方面和datetime是一样的，在储存上不一样
- 范围从　1970-1-1 0:0:0 到 2038-1-19 11:14:07
- 时间戳使用 4 个字节表示
- 该值大小与存储的位长有关: 2 ** (4 * 8 - 1)

```
create table timestamp_test (
	create_time timestamp
);

insert into timestamp_test values(now());
insert into timestamp_test values('2038-1-19 11:14:07');
insert into timestamp_test values('2038-1-19 11:14:08'); --错误
```

### (4)year

```
create table `year`(
create_at year
);

-- 从1900年年开始 - 1900+255

insert into `year` values(now());
insert into `year` values('2155');
insert into `year` values('2156'); -- 错误
```

## ７、布尔型

mysql中的bool类型也是1和0

```
create table `bool`(
cond boolean
);

insert into `bool` set cond=True; -- 成功
insert into `bool` set cond=False; -- 成功
insert into `bool` set cond=1; -- 成功
insert into `bool` set cond=10; -- 成功
insert into `bool` set cond=-1; -- 成功
insert into `bool` set cond=0; -- 成功
insert into `bool` set cond=0.1; -- 成功
insert into `bool` set cond='True'; -- 失败
```

## ８、列的属性

- 插入的值是否可以为空

  - null:是可以为空，默认不写
  - not null: 不可以为空，如果插入的时候某个字段的值为空，则会报错

  ```
  create table null_test (
  	id int primary key auto_increment,
  	username varchar(32) not null,
  	pwd varchar(16) null
  );
  insert into null_test values(null,null,null);	
  ```

- default

  默认值一般是和ｎｕｌｌ做搭配的

  ```
  create table default_test (
      id int primary key auto_increment,
      username varchar(32) default 'admin' not null,
      pwd varchar(16) default 123456
  );
  insert into default_test (username) values ('admin');
  ```

- auto_increment

  - 自动增长的列
  - 默认从１开始
  - 常配合主键使用

  ```
  create table auto_inc (
      id int primary key auto_increment,
      name varchar(32)
  );
  insert into auto_inc (name) values ('aaa'), ('bbb'), ('ccc');
  select * from auto_inc;
  
  /* 输出:
  +----+------+
  | id | name |
  +----+------+
  | 1 | aaa |
  | 2 | bbb |
  | 3 | ccc |
  +----+
  ×/
  ```

- primary key

  - 主键一般是唯一的标识
  - 特性：不能为空，也不能重复，一张表当中只可以拥有一个主键

  ```
  -- 这里只有一个主键,这种主键叫做联合主键, 在项目目中使用用较少
  create table double_pri_test (
      id int,
      sid int,
      primary key(id,sid)
  );
  insert into double_pri_test values (1, 1);
  insert into double_pri_test values (1, 2); -- 成功
  insert into double_pri_test values (2, 1); -- 成功
  insert into double_pri_test values (1, 1); -- 失败
  ```

- unique

  - 唯一键，保证列当中的每一个数据都不重复
  - 邮箱不可以重复，手机号不可以重复

  ```
  create table test_uniq (
      id int auto_increment primary key,
      mobile char(11) unique
  );
  insert into test_uniq set mobile=13999999999;
  ```

- comment

  - 注释：给开发者看的，一般用来对相应字段进行说明

  ```
  create table test_cmt (
  	ctime datetime comment '这个字段代表创建日日期'
  );
  ```

## ９、ＳＱＬ注释

- 单行注释: -- 你好
- 多行注释: /* 巴拉巴拉 */
- MySQL 独有的单行注释: # 哈哈哈哈

# 九、Mysql的运算符

## 算数运算符

```
select 123 + 543, 321 * 5, -456 / 2, 10 % 3, 2 / 0, 3 % 0;
/*输出:
+-----------+---------+-----------+--------+-------+-------+
| 123 + 543 | 321 * 5 | -456 / 2| 10 % 3 | 2 / 0 | 3 % 0 |
+-----------+---------+-----------+--------+-------+-------+
|		666 |	1605  | -228.0000 |		 1 |  NULL |NULL |
+-----------+---------+-----------+--------+-------+-------+
1 row in set, 2 warnings (0.00 sec)
*/
```

## 比较运算符

![](/home/shenyang/Pictures/4.png)

- 常规比较

```
select 1=2, 2<3, 3<=4, 4>5, 5>=3, 8!=9, 8<>9, 'abc' = 'Abc', 'z' > 'a';
/* 输出:
+-----+-----+------+-----+------+------+------+---------------+-----------
+
| 1=2 | 2<3 | 3<=4 | 4>5 | 5>=3 | 8!=9 | 8<>9 | 'abc' = 'Abc' | 'z' > 'a'
|
+-----+-----+------+-----+------+------+------+---------------+-----------
+
|	0 |	  1 |    1 |   0 |   1  |    1 |    1 |             1 |     1
|
+-----+-----+------+-----+------+------+------+---------------+-----------
+
1 row in set (0.00 sec)
*/
```

- 范围比较

```
select 123 between 100 and 200, 'b' in ('a', 'b', 'c');
/* 输出
+-------------------------+------------------------+
| 123 between 100 and 200 | 'b' in ('a', 'b', 'c') |
+-------------------------+------------------------+
|			1			  |				1 			|
+-------------------------+------------------------+
1 row in set (0.04 sec)
*/
```

- Null比较

```
select 12 is null, 23 = null, null = null, null <=> null, null is null, 32 is not null;
```

- 模糊比较: like

```
select 'HelloWorld' like 'hello%';
```

## 逻辑运算符

![](/home/shenyang/Pictures/5.png)

# 十、数据库的查询

## １、构造数据

学生表

```
create table student (
`id` int unsigned primary key auto_increment,
`name` char(32) not null unique,
`sex` enum('男', '女') not null,
`city` char(32) not null,
`description` text,
`birthday` date not null default '1995-1-1',
`only_child` boolean
) charset=utf8;

insert into student
(`name`, `sex`, `city`, `description`, `birthday`, `only_child`)
values
('郭德纲', '男', '北京', '班长', '1997/10/1', True),
('陈乔恩', '女', '上海', NULL, '1995/3/2', True),
('赵丽颖', '女', '北京', '班花, 不不骄傲', '1995/4/4', False),
('王宝强', '男', '重庆', '阳光大男孩, 超爱吃火火锅', '1998/10/5', False),
('赵雅芝', '女', '重庆', '全宇宙三好学生', '1996/7/9', True),
('张学友', '男', '上海', '全国数学奥林匹克竞赛冠军! 还有谁!', '1993/5/2', False),
('陈意涵', '女', '上海', NULL, '1994/8/30', True),
('赵本山', '男', '南京', '副班长', '1995/6/1', True),
('张柏芝', '女', '上海', '这家伙很勤勤奋, 但还是什么都没留留下。。。', '1997/2/28', False),
('吴亦凡', '男', '南京', '大碗宽面要不要?', '1995/6/1', True),
('鹿晗', '男', '北京', NULL, '1993/5/28', True),
('关晓彤', '女', '北京', NULL, '1995/7/12', True),
('周杰伦', '男', '台北', '小伙人才啊', '1998/3/28', False),
('⻢云', '男', '南京', '一个字:真丑,两个字:贼有钱', '1990/4/1', False),
('⻢化腾', '男', '上海', '深圳小马哥,马云死对头', '1990/11/28', False);
```

成绩表

```
create table score (
    `id` int unsigned primary key auto_increment,
    `math` float not null default 0,
    `english` float not null default 0
) charset=utf8;

insert into score (`math`, `english`)
values
(49, 71), (62, 66.7), (44, 86), (77.5, 74), (41, 75),(82, 59.5), (64.5, 85), (62, 98), (44, 36), (67, 56),(81, 90), (78, 70), (83, 66), (40, 90), (90, 90);
```

## ２、常用的查询语句

### (1)SELECT:字段表达式

- SELECT既可以查询。也可以做输出

- 例子

  ```
  select random();-- 随机数
  select unix_timestamp(); -- 显示Unix时间戳
  select id, name from student;
  ```

### (2)FROM字句

- 语句：select　字段 　from　表名　

- FROM后面的是数据源，数据源可以写多个，数据源一般是表明，也可以是其他查询的结果///////////////////////////////////

- 实例

  ```
  SELECT student.name, score.math FROM student,
  score;
  ```

### (3)WHERE子句：按照指定条件过滤

- 语法：select 字段　from 表名　where 条件；

- WHERE是做条件查询，只返回结果为Ｔrue的数据

- 实例

  ```
  select name from student where city = '上海';
  ```

- 空值判断：is null | is not null

  ```
  select `name` from `student` where `description` is null;
  select `name` from `student` where `description` is not null;
  ```

  

- 范围判断：between ...and ...| not between

  ```
  select id, math from score where math between 60 and 70;
  select id, math from score where math not between 60 and 70;
  select * from score where math>=80 and english<=60;
  -- 直接做比较判断
  ```

  

### (4)GROUP BY:分组查询

- 按照某一字段进行分组，会把该字段中相同的值归为一组，将查询的结果分类显示，方便统计

- GROUP BY要放在WHERE的后面

- 语法：select 字段　from 表名　group by 分组字段

- 实例

  ```
  select sex, count(id) from student group by sex;
  -- 在group将需要的结果通过 “聚合函数” 拼接
  select sex, group_concat(name) from student group by sex;
  -- 添加where语句
  -- 按性别分组, 将上海地区的男生女生姓名连接起来
  select sex, group_concat(name) from student where city='上海' group by sex;
  ```

### (5)HAVING

- HAVING与WHERE在SQL中增加HAVING子句原因是，WHERE关键字无法与聚合函数一起使用

- 语法：SELECT　字段　FROM　表名　HAVING　条件

- WHERE: 后面不能加上聚合函数，只能写在数据源的后面

- HAVING:条件字段必须要在结果中集中出现，HAVING可以写在GROUP BY的后面

- 实例：

  ```
  select `name`, `birthday` from `student` where `birthday` > '1995-1-1';
  select `name`, `birthday` from `student` having `birthday` > '1995-1-1';
  select `name` from `student` where `id` >= 5;
  select `name` from `student` having `id` >= 5;
  -- 错误
  select * from student where id>=3 and city='北京';
  select * from student having id>=3 and city='北京';
  select * from student where id>=3 having city='北北京';
  -- 混用
  -- 取出每个城市中满足足最小出生年份大于1995的
  select city, group_concat(birthday) from student group by city having
  min(birthday) > '1995-1-1';
  ```

### (6)ORDER BY:按字段排序

- ORDER BY主要作用是排序

- ORDER BY写在 GROUP BY后面，如果有 HAVING 也要写在HAVING后面

- 语法：select 字段 from 表名 order by 排序字段 asc | desc

- 分为升序 asc 降序 desc ,默认 asc (可以不写)

- 实例

  ```
  select * from student order by age;
  select * from student order by age desc;
  ```

### (7)LIMIT：限制取出数量

- 语法：

  ```
  select 字段 from 表名 limit m;
  -- 从第 1 行到第 m 行
  select 字段 from 表名 limit m, n;
  -- 从第 m 行开始,往下取 n 行
  select 字段 from 表名 limit m offset n;
  -- 跳过前 n 行, 取后面的 m 行
  ```

### (8)DISTINCT：去重

- 实例

  ```
  select distinct city from student;
  ```

### (9)dual表

dual 是一个虚拟表, 仅仅为了保证 select ... from ... 语句的完整性

```
select now() from dual;
```

## 3、函数

### (1)聚合函数

| Name             | Description                  |
| ---------------- | ---------------------------- |
| AVG()            | 返回参数的平均值             |
| BIT_AND()        | 按位返回AND                  |
| BIT_OR()         | 按位返回OR                   |
| BIT_XOR()        | 按位返回异或                 |
| COUNT()          | 返回返回的行数.              |
| COUNT(DISTINCT)  | 返回许多不同值的计数         |
| GROUP_CONCAT()   | 返回连接的字符串             |
| JSON_ARRAYAGG()  | 讲结果集作为单个JSON数组返回 |
| JSON_OBJECTAGG() | 讲结果集作为单个JSON对象返回 |
| MAX()            | 返回最大值                   |
| MIN()            | 返回最小值                   |
| STD()            | 返回样本的标准差             |
| STDDEV()         | 返回样本的标准差             |
| STDDEV-POP()     | 返回样本的标准差             |
| STDDEV_SAMP()    | 返回样本的标准差             |
| SUM()            | 归还总和                     |
| VAR_POP()        | 返回样本的标准差异           |
| VAR_SAMP()       | 返回样本方差                 |
| VARIAN()         | 返回样本的标准差异           |

### (2)数值计算类函数

![](/home/shenyang/Pictures/8.png)

### (3)日期计算类函数

![](/home/shenyang/Pictures/9.png)

### (4)字符串相关函数

![m](/home/shenyang/Pictures/10.png)

### (5)其他函数

![](/home/shenyang/Pictures/11.png)

## 4、多表查询

### **UNION联合查询**

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。
union要求:

1. 两边 select 语句句的字段数必须一样

2. 两边可以具有不同数据类型的字段

3. 字段名默认按照左边的表来设置

4. 用法：

   ```
   SELECT column_name(s) FROM table1
   UNION
   SELECT column_name(s) FROM table2;
   ```

### INNER JOIN : 内连接 (交集)

![](/home/shenyang/Pictures/12.png)

- INNER JOIN 关键字在在表中存在至少一个匹配时返回行

- 语法：

  ```
  SELECT 字段
  FROM 表1 INNER JOIN 表2
  ON 表1.字段=表2.字段;
  
  
  -- 或:
  SELECT column_name(s)
  FROM table1 JOIN table2
  ON table1.column_name=table2.column_name;
  ```

### LEFT JOIN：左链接

![](/home/shenyang/Pictures/13.png)

- LEFT JOIN 关键字从左表(table1)返回所有的行,即使右表(table2)中没有匹配。如果右表中没有匹配,则结果为 NULL。

- 语法：

  ```
  SELECT column_name(s)
  FROM table1
  LEFT JOIN table2
  ON table1.column_name=table2.column_name;
  
  -- 或:
  SELECT column_name(s)
  FROM table1
  LEFT OUTER JOIN table2
  ON table1.column_name=table2.column_name;
  ```

### RIGHT JOIN：右链接

![](/home/shenyang/Pictures/14.png)

- RIGHT JOIN 关键字从右表(table2)返回所有的行,即使左表(table1)中没有匹配。如果左表中没有匹配,则结果为 NULL。

- 语法：

  ```
  SELECT column_name(s)
  FROM table1
  RIGHT JOIN table2
  ON table1.column_name=table2.column_name;
  
  
  -- 或:
  SELECT column_name(s)
  FROM table1
  RIGHT OUTER JOIN table2
  ON table1.column_name=table2.column_name;
  ```

### 子查询

查询的语句中还有一个查询

```
select name from student where id in (select id from score where math > 10);
```

# 十一、数据库的高级特性

## 1、权限管理

### (1)**MYSQL的权限的两个阶段：**

- 第一阶段为连接验证,主要限制用户连接 mysql-server 时使用的 ip 及 密码
- 第二阶段为操作检查,主要检查用户执行的指令是否被允许,一般非管理员账户不被允许执行drop、delete 等危险操作

### (2)**权限控制安全准则：**

- 只授予能满足需要的最小权限,防止用户执行危险操作
- 限制用户的登录主机,防止不速之客登录数据库。
- 禁止或删除没有密码的用用户。
- 禁止用户使用弱密码。
- 定期清理无效的用户,回收权限或者删除用户。

### (3)**常用操作：**

- 创建用户、权限授予

  - 8.0之前的版本

    ```
    GRANT ALL PRIVILEGES on *.* to '用用户名'@'主机' IDENTIFIED BY "密码" WITH
    GRANT OPTION;
    flush privileges; -- 刷新使权限生效
    ```

    - ALL PRIVILEGES : 授予全部权限, 也可以指定 select 、 insert 等
    - *.*:允许操作的数据库和表

  - WITH GRANT OPTION : 带有该子句说明允许用户将自己拥有的权限授予别人

  - 8.0 之后的版本

    ```
    CREATE USER `用用户名`@`主机` IDENTIFIED BY '密码';-- 创建账户
    GRANT ALL ON *.* TO `用用户名`@`主机` WITH GRANT OPTION;-- 授权
    ```

- 修改密码

  ```
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';
  ```

- 查看权限

  ```
  show grants;    -- 查看当前用户的权限
  show grants for 'abc'@'localhost';   
  -- 查看用户 abc 的权限
  ```

- 回收权限

  ```
  revoke delete on *.* from 'abc'@'localhost';
  ```

- 删除用户

  ```
  use mysql;
  select host, user from user;
  drop user 用用户名@'%';
  ```

## 2、视图

- 视图是数据的特定子集,是从其他表里提取出数据而形成的虚拟表,或者说临时表。
- 创建视图表依赖一个查询。
- 视图是永远不会自己消失的除非手动删除它。
- 视图有时会对提高效率有帮助。临时表不会对性能有帮助,是资源消耗者。
- 视图一般随该数据库存放在一起,临时表永远都是在 tempdb 里里里的。
- 视图适合于多表连接浏览时使用;不适合增、删、改,这样可以提高执行效率。
- 一般视图表的名称以 v_ 为前缀,用来与正常表进行区分。
- 对原表的修改会影响到视图中的数据。

### 创建视图

- 语法:create view 视图名 as 查询语句

- 实例：

  ```
  -- 以上节课的关联查询为例
  create view v_user_score as
  select a.id, a.name, b.math, b.english
  from student a inner join score b on a.id=b order by id;
  
  -- 查询
  select * from v_user_score;
  
  -- 删除
  drop view v_user_score;
  ```


## 3、储存引擎

存储引擎就是如何存储数据、如何为数据建立索引和如何更新、查询数据等技术的实现方法。
MySQL 默认支持多种存储引擎,以适用于不同领域 的数据库应用需要,用户可以通过选择使用不同的存储引擎提高应用的效率,提供灵活的存储。

### (1)查看当前的储存引擎

```
show variables like '%storage_engine';
show engines;
```

### (2)MySQL常用的储存引擎

![](/home/shenyang/Pictures/17.png)

<!-- ### 3. 表的引擎
InnoDB 和 MyISAM
CURD操作:增删改查
C create insert 插入
U update 修改
R read select 查询
D delete 删除
less /etc/my.cnf
默认的存储路路径
datadir = /data/mysql
innodb 在 写的操作上非常的有优势(事务) CUD全是写的操作
myisam 在 读的操作上非常的有优势(健全的索引) R操作

### (3)引擎的储存方式

myisam将一张表存储为三个文件
demo.frm -> 表的结构
demo.MYD -> 存储的是数据
demo.MYI -> 存储的是表的索引

### (4)myisam的文件可以任意的移动

innodb将一张表存储为两个文件
demo.frm -> 表的结构+表的索引
demo.ibd -> 存储的是数据
ibd存储是有限的, 存储不足自动创建ibd1, ibd2

## ４、innodb的文件创建在哪个数据库中，不任意的的移动

- innoDB

  事务型数据库的首选引擎，支持事务安全表（ACID），支持行锁定和外键，innoDB是默认的MySQL引擎

  innoDB的主要特征：InnoDB 给 MySQL 提供了具有提交、回滚、崩溃恢复能力的事物安全存储引擎。

1. InnoDB 是为处理巨大数据量的最大性能设计。它的 CPU 效率比比其他基于磁盘的关系型数据
    库引擎高高。
2. InnoDB 存储引擎自带缓冲池,可以将数据和索引缓存在内存中。
3. InnoDB 支持外键完整性约束。
4. InnoDB 被用在众多需要高性能的大型数据库站点上
5. InnoDB 支持行级锁

- MyISAM

  MYISAM基于ISAM储存引擎，并对其进行拓展。他是在ｗｅｂ，数据仓储和其他应用环境下最常使用的存储引擎之一。MYISAM拥有较高的插入，查询速度，但是不支持事务

  MyISAM主要特性有:

  1. 大文件支持更好
  2. 当删除、更新、插入混用时,产生更少碎片。
  3. 每个 MyISAM 表最大索引数是64,这可以通过重新编译来改变。每个索引最大的列列数是16
  4. 最大的键⻓度是1000字节。
  5. BLOB和TEXT列可以被索引
  6. NULL 被允许在索引的列中,这个值占每个键的0~1个字节
  7. 所有数字键值以高字节优先被存储以允许一个更高的索引压缩
  8. MyISAM 类型表的 AUTO_INCREMENT 列更新比 InnoDB 类型的 AUTO_INCREMENT 更快
  9. 可以把数据文件和索引文件放在不同目录
  10. 每个字符列可以有不同的字符集
  11. 有 VARCHAR 的表可以固定或动态记录长度
  12. VARCHAR 和 CHAR 列可以多达 64KB
  13. 只支持表锁

- MEMORY

  MEMORY储存引擎将表中数据存储到内存中，为查询引用其他表数据提供快速访问

### (1)存储引擎的选择

一般来说，对插入和并发性要求较高的，或者需要外键及事务支持的选择innoDB,查询较少的场景，优先考虑MyISAM

### (2)使用引擎

一般在建表是添加

```
create table abc (
    name char(10)
) engine=MyISAM charset=utf8;

create table xyz (
    name char(10)
) engine=InnoDB charset=utf8;
```

## ５、索引

索引就是为特定的 mysql 字段进行一些特定的算法排序,比如二叉树的算法和哈希算法,哈希算法是通过建立特征值,然后根据特征值来快速查找。
MySQL 索引的建立对于 MySQL 的高高效运行是很重要的,索引可以大大提高MySQL的检索速度。

![](/home/shenyang/Pictures/18.png)

用的最多,并且是 mysql 默认的索引数据结构 btree。
通过 BTREE 算法建立索引的字段,比如扫描 20 行就能得到未使用 BTREE 前扫描了2^20 行的结果

![](/home/shenyang/Pictures/19.png)

哈希索引比较特殊,时间复杂度为 O(1), 但只适合等值比较方式的查询,不适合范围或大小比较进行查询

**索引的优点:**
一个字:快!使用索引能极大提升查询速度。
索引的缺点:

1. 额外的使用了一些存储的空间
2. 索引会让写的操作变慢

### (1)索引的创建原则

1. 适合用于频繁查找的列
2. 适合经常用于条件判断的列
3. 适合经常由于排序的列
4. 不适合数据不多的列
5. 不适合很少查询的列

### (2)创建索引

1. 建表时添加索引

   ```
   create table 表(
       id int not null,
       username varchar(16) not null,
       index 索引名(字段名(长度))
   );
   ```

2. 后期添加索引

   ```
   create index `索引名` on 表名(字段名(⻓度));
   ```

### (3)删除索引

```
drop index [索引名] on 表;
```

### (4)唯一索引

它与前面的普通索引类似,不同的就是:索引列的值必须唯一,但允许有空值。如果是组合索引,则列值的组合必须唯一

```
create unique index 索引名 on 表(字段名(长度));

-- 或
create table 表(
    id int not null,
    username varchar(16) not null,
    unique 索引名 (字段名(⻓度))
);
```

### (5)查看索引

```
show index from table_name 
```

## ６、关系与外键

### (1)关系

- 一对一
  - 在Ａ表中有一条记录，在B表中有唯一一条记录相匹配
  - 比如：学生表和成绩表
- 一对多
  - 在A 表中有一条记录,在 B 表中有多条记录一直对应
  - 比如：微博中用户表和文章表
- 多对多
  - A 表中的一条记录有多条 B 表数据对应, 同样 B 表中一条数据在 A 表中也有多条与之对应
  - 比如: 用户与权限关系

### (2)外键

外键是一种约束，他只是保证数据的一致性，并不能给系统带来任何好处

# 十二、数据库的事务及其他

## １、事务

### (1)事务简介

事务主要用于处理操作量大，并且关联性强的数据

比如说, 在人员管理理系统中, 你删除一个人员, 你即需要删除人人员的基本资料料, 也要删除和该人员相关的信息, 如信箱, 文章等, 这样, 这些数据库操作语句就构成一个事务!
在 MySQL 中只有 Innodb 存储引擎支持事务。
事务处理可以用来维护数据库的完整性, 保证成批的 SQL 语句要么全部执行, 要么全部不执行。主要针对insert, update, delete 语句而设置

### (2)事务的四大特性

在写入或更新资料的过程中, 为保证事务 (transaction) 是正确可靠的, 所必须具备的四个特性 (ACID):

**原子性** (Atomicity) :

事务中的所有操作, 要么全部完成, 要么全部不完成, 不会结束在中间某个环节。

事务在执行过程中发生错误, 会被回滚 (Rollback) 到事务开始前的状态, 就像这个事务从来没有执行过一样。

**一致性** (Consistency):

在事务开始之前和事务结束以后, 数据库的完整性没有被破坏。

这表示写入的资料必须完全符合所有的预设规则, 这包含资料的精确度、串联性以及后续数据库可以自发性地完成预定的工作。

**隔离性**（lsolation）

数据库允许多个并发事务同时对其数据进行读写和修改的能力, 隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。

事务隔离分为不同级别, 包括:

- 读取未提交（read uncommitted）

  - 所有事务都可以看到其他未提交事务的执行结果
  - 本隔离级别很少用于实际应用,因为它的性能也不比其他级别好多少
  - 该级别引发的问题是——脏读(Dirty Read):读取到了未提交的数据

- 读提交 (read committed)

  - 这是大多数数据库系统的默认隔离级别(但不是MySQL默认的)

  - 它满足了隔离的简单定义:一个事务只能看见已经提交事务做的改变

  - 这种隔离级别出现的问题是: 不可重复读(Nonrepeatable Read):

    不可重复读意味着我们在同一个事务中执行完全相同的 select 语句时可能看到不一样的结果

    

    导致这种情况的原因可能有

    - 有一个交叉的事务有新的commit,导致了数据的改变
    - 一个数据库被多个实例操作时，同一个事务的其他实例在该实例处理期间可能会有新的commit

**可重复性读**（repeatable read）

- 这是ＭｙＳＱＬ默认的隔离级别
- 它确保同一事物的多个实例在并发读取数据时，会看到同样的数据行
- 此级别可能出现的问题: 幻读(Phantom Read):当用户读取某一一范围的数据行时,另一个事务又在该范围内插入了新行,当用户再读取该范围的数据行时,会发现有新的“幻影” 行
- InnoDB通过多版本并发控制(MVCC,Multiversion Concurrency Control) 机制解决幻读问题

**串行化**(Serializable)

- 这是最高的隔离级别
- 他通过强制事务排序，使之不可能相互冲突，从而解决幻读问题，简而言之，他是在每个读的数据行上加上共享锁。MYSQL锁总结
- 在这个级别，可能导致大量的超时现象和锁竞争

**持久性** (Durability):

事务处理结束后，对数据的修改就是永久性的，即使系统故障也不会丢失

### (3)语法与使用

- **开启事务：**ＢＥＧＩＮ或者ＳＴＡＲＴ　ＴＲＡＮＳＡＣＴＩＯＮ

- **提交事务：**COMMIT,提交会让所有修改生效

- **回滚：**ROLLBACK，撤销正在进行的所有未提交的修改

- **创建保存点：**SAVEPOINT  identifier

- **删除保存点：**RELEASE  SAVEPOINT  identifier 

- **把事务回滚到保存点**：ROLLBACK  TO  identifier

- **设置事务的隔离级别：**SET  TRANSACTION

  **innoDB提供的级别有**

  - READ
  - UNCOMMITTED
  - READ  COMMITTED
  - REPEATABLE  READ
  - SERIALIZABLE

  **示例**

  ```
  create table `abc` (
      id int unsigned primary key auto_increment,
      name varchar(32) unique,
      age int unsigned
  ) charset=utf8;
  
  begin;
  insert into abc (name, age) values ('aa', 11);
  insert into abc (name, age) values ('bb', 22);
  -- 在事务中查看一一下数据
  -- 同时另开一个窗口,连接到 MySQL 查看一下数据是否一样
  select * from abc;
  commit;
  
  begin;
  insert into abc (name, age) values ('cc', 33);
  insert into abc (name, age) values ('dd', 44);
  update abc set age=77 where name='aa';
  -- 在事务中查看一下数据
  select * from abc;
  rollback;
  
  select * from abc;
  -- 事务结束后在查看一下数据
  ```

## ２、锁

锁是计算机协调多个进程或线程并发访问某一资源的机制

锁保证数据并发访问的一致性、有效性

锁冲突也是影响数据库并发访问性能的一个重要因素

锁是Mysql在服务器器层和存储引擎层的的并发控制

### 分类

- **行级锁**
  - 行级锁是Mysql中锁定粒度最细的一种锁,表示只针对当前操作的行进行加锁。
  - 行级锁只有 InnoDB 引擎支支持。
  - 行级锁能大大减少数据库操作的冲突。其加锁粒度最小,但加锁的开销也最大。
  - 特点:开销大,加锁慢;会出现死锁;锁定粒度最小,发生锁冲突的概率最低,并发度也最高。
- **表级锁**
  - 表级锁是MySQL中锁定粒度最大的一种锁
  - 对当前操作的整张表加锁,它实现简单,资源消耗较少,被大部分MySQL引擎支支持。
  - 特点:开销小,加锁快;不会出现死锁;锁定粒度大,发出锁冲突的概率最高,并发度最低。
- **共享锁**（读锁）
  - 其他用户可以并发读取数据,但任何事务不能对数据进行修改,直到已释放所有共享锁。
- **排他锁**（写锁）
  - 如果事务 T 对数据 A 加上排他锁后,则其他事务不能再对 A 加任何类型的封锁。
  - 持有排他锁的事务既能读数据,又能修改数据。
- **乐观锁**（Optimistic Lock）
  - 假设不会发生并发冲突,只在提交操作时检查是否违反数据完整性。 乐观锁不能解决脏读的问题
  - 乐观锁, 顾名思义,就是很乐观,每次去拿数据的时候都认为别人不会修改,所以不会上锁,但是在更新的时候会判断一下在此期间别人有没有去更新这个数据,可以使用版本号等机制。乐观锁适用于多读的应用类型,这样可以提高吞吐量,像数据库如果提供类似于write_condition机制的其实都是提供的乐观锁。
- **悲观锁**（Ｐessimistic lock）
  - 假定会发生并发冲突,屏蔽一切可能违反数据完整性的操作
  - 悲观锁,顾名思义,就是很悲观,每次去拿数据的时候都认为别人会修改,所以每次在拿数据的时候都会上锁,这样别人想拿这个数据就会block直到它拿到锁。传统的关系型数据库里边就用到了很多这种锁机制,比如行锁,表锁等,读锁,写锁等,都是在做操作之前先上锁。

## ３、存储过程

存储过程(Stored Procedure)是一种在数据库中存储复杂程序,以便外部程序调用的一种数据库对象。

存储过程是为了完成特定功能的SQL语句集,经编译创建并保存在数据库中,用户可通过指定存储过程的名字并给定参数(需要时)来调用执行

存储过程思想上很简单,就是数据库 SQL 语言层面的代码封装与重用。

### 优点:

- 存储过程可封装,并隐藏复杂的商业逻辑。
- 存储过程可以回传值,并可以接受参数。
- 存储过程无法使用 SELECT 指令来运行,因为它是子程序,与查看表,数据表或用户定义函数不同。
- 存储过程可以用在数据检验,强制实行商业逻辑等。

### 缺点：

- 存储过程,往定制化于特定的数据库上,因为支持的编程语言不同。当切换到其他厂商的数据库系统时,需要重写原有的存储过程。
- 存储过程的性能调校与撰写,受限于各种数据库系统。

### (1)语法：

**声明语句结束符,可以自定义**:
存储过程中有很多的SQL语句句,SQL语句的后面为了保证语法结构必须要有分号(;),  但是默认情况下分号表示客户端代码发送到服务器器执行。必须更改结束符

```
DELIMITER $$
-- 或者
DELIMITER //
```

**声明存储过程:**

```
CREATE PROCEDURE demo_in_parameter(IN p_in int)
```

**存储过程开始和结束符号:**

```
BEGIN .... END
```

**变量赋值:**

```
SET @p_in=1
```

**变量定义:**

```
DECLARE l_int int unsigned default 4000000;
```

**创建mysql存储过程、存储函数:**

```
create procedure 存储过程名(参数)
```

**存储过程体**

```
create function 存储函数名(参数)
```

### (2)使用

**简单用法**

```
-- 定义
-- 如果存储过程中就一条SQL语句句,begin...end两个关键字可以省略
create procedure get_info()
select * from student;

-- 调用
call get_info();
```

**复杂一点的 (备注:只能在标准 mysql 客户端中执行行行,mycli 无无法识别)**

```
delimiter // -- 定义前,将分隔符改成 //
create procedure foo(in uid int)
begin
select * from student where `id`=uid;
update student set `city`='北北京' where `id`=uid;
end//
delimiter ;--定义完以后可以讲分隔符改回分号

call foo(3);
```

**延伸阅读**

https://www.zhihu.com/question/19749126
https://segmentfault.com/q/1010000004907411

## ４、Ｐｙｔｈｏｎ操作

安装：pip install pymysql

使用：

```
import pymysql

db = pymysql.connect(host='localhost',
                    user='user',
                    password='passwd',
                    db='db',
                    charset='utf8')
try:
	with db.cursor() as cursor:
		# 插入
        sql = "INSERT INTO `users` (`email`, `password`) VALUES (%s, %s)"
        cursor.execute(sql, ('webmaster@python.org', 'very-secret'))
    # 需要手动提交才会执行
    db.commit()
    
    with db.cursor() as cursor:
        # 读取记录
        sql = "SELECT `id`, `password` FROM `users` WHERE `email`=%s"
        cursor.execute(sql, ('webmaster@python.org',))
        result = cursor.fetchone()
        print(result)
finally:
    db.close()
```

## (5)数据备份与恢复

**备份**

```
mysqldump -h localhost -u root -p123456 dbname > dbname.sql
```

**恢复**

```
mysql -h localhost -u root -p123456 dbname < ./dbname.sql
```







​				