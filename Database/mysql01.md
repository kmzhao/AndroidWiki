## MySql入门01 

### 一，数据库
#### 1.1 概述
数据库DB，database:按数据结构存储和管理数据的计算机软件系统
#### 1.2 启动登陆
    启动：
    cmd> net start mySql
    cmd> net stop mySql
    登录：
    cmd> mysql -u账号 -p密码
#### 1.3 常用命令
- 查询所有的数据库：mysql> show databases;
- 使用数据库：mysql> use 数据库名称;
- 查询当前数据库所有的表：mysql> show tables;
- 查询当前使用的数据库：mysql> select database();
- 查看表结构：mysql> desc 表名;
- 查看状态：mysql> status;


### 二，SQL语句
#### 2.1 概述
SQL称为结构化查询语言(structured query language),是操作和检索关系型数据库的标准语言(CURD)

#### 2.2语法要求如下：
* 所有内容都需要使用英文符号
* 每一个语句必须使用;结尾
* sql命令不区分大小写，建议：关键字大写

#### 2.3 sql分类
- DDL： 数据定义语言，定义的是结构； 关键字：create  drop   alter
- DML:  数据操作语言，操作的是数据； 关键字：insert  update  delete
- DQL:  数据查询语言，检索的是数据； 关键字：select
- DTL:  事务处理语言                关键字：开启事务start transaction，提交事务commit，回滚事务rollback
- DCL:  数据控制语言                关键字：授权grant、回收revoke


### 三，DDL(Data Definition Language)  结构
#### 3.1 创建数据库

    mysql> create database [IF NOT EXISTS] 数据库名称 [character set 字符集];
    mysql> drop database 数据库名称;
    mysql> alter database 数据库名称 character set 字符集;

#### 3.2 表
##### 3.2.1 创建表
- 格式： create table users(字段描述1,字段描述2,字段描述3);
- 举个例子： create table users(id varchar(32),name varchar(50),age int);
> 其中字段描述的定义： 字段名称 字段类型
> 常用字段类型：
varchar(n)  可变字符串;
int			  --> int【】
double(m,d)	--> double【】  例如：double(5,2) , M表示数字的个数，D表示小数位的个数。最大值：999.99

##### 3.2.3 删除表
drop table [IF EXISTS] 表名
##### 3.2.4 修改表
* 重命名：mysql> alter table 表名 rename to 新表名
* 添加字段：mysql> alter table 表名 add column 字段描述;
* 删除字段：mysql> alter table 表名 drop [column] 字段名称;
* 修改字段：mysql> alter table 表名 change old字段名称 new字段描述;

### 四，DML 数据操纵语言
#### 4.1 插入
- insert into 表(字段名称1,字段名称2,...) values(值1,值2,...);
#### 4.2 更新：
- update 表名 set 字段 = 值,字段2=值2,...where 条件;
#### 4.3 删除
- delete from 表名 where 条件；

### 五， DQL 数据查询语言(查询，检索)
#### 5.1 聚合函数的使用

  1. 有多少条记录：select count(*) from 表名；
  2. 平均成绩：select avg(fenshu) from users; //不含null
  3. 平均成绩：select sum(fenshu)/count(*) from 表名;

#### 5.2 分组【】
- 分组：select ... where .. group by 分组字段 having 分组条件
- select ...只能是聚合函数或者分组字段

#### 5.3 总结【】

		select distinct *|字段|聚合函数 from 表名
		where 查询条件
		group by 分组字段
			having 分组条件
		order by 排序字段 asc|desc


### 六，about 约束：规定数据库中的表中的数据应该如何存在
#### 6.1 主键约束
- 关键字： primary key
- 主 键：被约束的字段，内容不能重复，不能为null

##### 6.1.1 声明方式
- 声明字段时 直接添加

          create table info(id varchar(32) primary key,content varchar(512));

- 声明字段后 在约束区域添加

          create table info(id varchar(32),content varchar(50),constraint primary key(id));

- 创建表之后 修改表结构 添加主键

          create table info(id varchar(32),content varchar(512));
          alter table info add constraint primary key(id);


#### 6.2 唯一约束
- 关 键 字： unique
- 唯一约束： 别约束的字段不能重复
##### 6.2.1 声明方式：
- 声明字段时， 添加约束

          create table info(id varchar(32) unique);

- 声明字段后，在约束区域添加主键：

          create table info(id varchar(32) unique,content varchar(32),constraint unique (id));

- 创建表之后， 修改表结构添加主键

          create table info(id varchar(32),content varchar(512));
          alter table info add constraint unique (id);


#### 6.3 非空约束
* 关键字：not null
* 非空：被约束的字段内容不能为null
* 声明方式

            create table info(id int not null,content varchar(512));


#### 6.4 mysql特有的字段： 自动增长列
* 关键字： auto_increment
* 自动增长： 被修饰的字段，每添加一条数据+1；
- 要求：  1) 必须是整形  2) 必须是主键

        create table auto(id int primary key auto_increment,content varchar(32));

#### 6.5 外键：
— 关键字： foreign key
