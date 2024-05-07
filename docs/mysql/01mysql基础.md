# 一、MySQL数据库启动

> ## 1、启动MySQL服务
```mysql
service  mysqld start
```

> ## 2、开启MySQL服务开机自启
```mysql
sudo systemctl enable mysql
```

> ## 3、停止MySQL服务
```mysql
service mysqld stop
```

> ## 4、重启MySQL服务
```mysql
service mysqld restart
```
> ## 5、查看MySQL是否启动命令
```mysql
ps -aux | grep mysqld
```

<!--  -->


# 二、MySQL数据库表操作

## 1、数据库操作

> <h3>1-1 查看当前所有数据库</h3>
```mysql
SHOW DATABASES
```

> <h3>1-2 进入数据库</h3>
```mysql
USE 数据库名;
```
```mysql语法案例
USE Student; -- 选择使用那个数据库
```

> <h3>1-3 创建数据库</h3>
```mysql
CREATE DATABASE  数据库名;
```
```mysql语法案例
CREATE DATABASE Student;
```

> <h3>1-4 删除数据库</h3>
```mysql
DROP DATABASE  数据库名;
```
```mysql语法案例
DROP DATABASE Student;
```

## 2、数据库表操作

> <h3>2-1 创建数据库表</h3>
```mysql
CREATE TABLE <表名>
(
列名1  数据类型 [列级别约束条件]  [默认值],

列名2  数据类型 [约束条件]  [默认值]
);
```
```mysql语法案例
CREATE TABLE reader(
	id     INT,
	card_id char(18), 
	gender VARCHAR(10),
	age    INT,
	birth  DATE,
	score   DOUBLE
);
```

> <h3>2-2 删除表</h3>
```mysql
drop table 表名;
```
```mysql语法案例
drop table reader;	
```

> <h3>2-3 查看指定某个表的创建语句</h3>
```mysql
SHOW  CREATE TABLE 表名;
```
```mysql语法案例
SHOW  CREATE TABLE reader;
```




## 3、修改表结构格式

> <h3>3-1 修改列名和类名</h3>
```mysql
ALTER TABLE 表名 change  旧列名 新列名 类型(长度)  [约束] ;
```
```mysql语法案例
ALTER TABLE reader CHANGE  name names  varchar(20);
```

> <h3>3-2 修改表添加列</h3>
```mysql
ALTER TABLE 表名 add 列名 类型(长度)  [约束] ;
```
```mysql语法案例
ALTER TABLE reader ADD name varchar(20); 
```


> <h3>3-3 删除列</h3>
```mysql
ALTER TABLE 表名 drop  列名;
```
```mysql语法案例
ALTER TABLE reader DROP  names;
```



> <h3>3-4 修改表名</h3>
```mysql
RENAME TABLE 表名 TO 新表名;
```
```mysql语法案例
RENAME TABLE reader  TO 学生表;
```


# 三、MySQL数据增删改操作

## 1、数据插入

```mysql
方法一
insert into 表 values(值1,值2,值3....);

方法二
insert into 表(列名1,列名2,列名3...) values(值1,值2,值3....);
```
```mysql语法案例
-- 方法一
INSERT INTO 学生表 VALUES(101,'18',14,'52','2001-12-23',87.5),(102,'19',12,'52','2001-12-23',87.5);

-- 方法二
INSERT INTO 学生表(id,card_id,gender,age,birth,score)
VALUES(101,'2',18,'25','2001-12-23',87.5),(102,'3',12,'34','2001-12-23',87.5);
```

## 2、数据修改

```mysql
 --字段名就是列名
update 表名 set 字段名=值,字段名=值...;  
 --------------------------------------------
update 表名 set 字段名=值,字段名=值...  where 条件;
```
```mysql语法案例
 --会修改所有数据
update 学生表 set gender='张三';
 --------------------------------------------
 -- 修改单个数据 把id是102的改成张
update 学生表 set gender='张' where  id = 102;
```


## 3、数据删除

```mysql
delete from 表名 [where 条件];
 --------------------------------------------
truncate table 表名 或者 truncate 表名
```
```mysql语法案例
-- 删除单个数据
delete from 学生表   where  id = 102;
 --------------------------------------------
-- 清空数据
delete from 学生表;
```

# 四、MySQL数据查找

## 1、简单查询

> <h3>1-1 修改表名</h3>
```mysql
-- ---查询所有的内容
select * from 表名;

-- 查询指定列的内容
select 列名 ,列名 from 表名;

-- ---别名查询.使用的关键字是as (as可以省略的）.
select * from 表名 as 表别名自定义;

-- --- 列别名:
select 列名 ,列名  as 列别名自定义  from 学生表;

-- ---去掉重复值.
select distinct 列名 from 表名;

-- ---查询结果是表达式（运算查询）:将所有商品的价格+10元进行显示.
select 列名+10 别名 from 表名;

-- ---模糊查询  %用来匹配任意字符  下划线匹配单个字符
select * from 列名 where like '要查询的内容';
select * from 列名 where like '_要查询的内容%';
```
```mysql语法案例
-- ---查询所有的内容
select * from 学生表;

-- ---查询指定列的内容
select id ,birth from 学生表;

-- ----- 别名查询.使用的关键字是as (as可以省略的）.
select * from 学生表 as p;

-- --- 列别名:
select id  as 序号id  from  学生表;

-- --- 去掉重复值 可以把if换成* 
select distinct id from 学生表;

-- ---查询结果是表达式（运算查询）:将所有商品的价格+10元进行显示.
select id+10 别名 from 学生表;
```

## 2、排序查询



> <p>asc代表升序，desc代表降序，如果不写默认升序</p>
> <p> order by用于子句中可以支持单个字段，多个字段，表达式，函数，别名</p>
> <p>order by子句，放在查询语句的最后面。LIMIT子句除外</p>

```mysql
select * from  表名 order by 列名 asc;
select * from  表名 order by 列名 desc;
```
```mysql语法案例
select * from  学生表 order by id;
select * from  学生表 order by id asc;
select * from  学生表 order by id desc;
```
## 3、聚合查询


| 聚合函数 | 作用                                                         |
| -------- | ------------------------------------------------------------ |
| cont()   | 统计指定列不为NULL的记录行数|
| sum()    | 计算指定列的数值和|
| max()    | 计算指定列的最大值|
| min()    | 计算指定列的最小值|
| avg()    | 计算指定列的平均值 |


> <h3>3-1 聚合查询</h3>
```mysql
select  count(列名) from 表名;

-----查询大于200的总个数
select  count(列名) from 表名 where 列名>200 ;
```
```mysql语法案例
select  count(id) from 学生表;

--------查询大于200的总个数
select  count(id) from 表名 where id>200 ;
```

## 4、分组查询
> <p> 分组查询是指使用group by字句对查询信息进行分组</p>
> <p>分组之后对统计结果进行筛选的话必须使用having,不能使用where</p>
> <p>where子句用来筛选 FROM子句中指定的操作所产生的行</p>
> <p>group by子句用来分组WHERE子句的输出</p>
> <p>having子句用来从分组的结果中筛选行</p>


> <h3>4-1 分组查询</h3>
```mysql
select   count(列名)  from 表名  group by 列名;

--只显示大于4的内容
select   count(列名) 列名  from 表名  group by 列名 having 列名>4;
```
```mysql语法案例
select  count(id)  from 学生表  group by id;

--只显示大于4的内容
select  count(id) id from 学生表  group by id having id>2;
```


## 5、分页查询
> limit分页查询在项目开发中常见，由于数据量很大，显示屏长度有限，因此对数据需要采取分页显示方式。例如数据共有30条，每页显示5条，第一页显示1-5条，第二页显示6-10条。

> <h3>5-1 分页查询</h3>
```mysql
-- m:整数，表示从第几条索引开始，计算方式（当前页-1) *每页显示条数
-- n:整数，表示查询多少条数据
select  *  from 表名 limit m,n
```
```mysql语法案例
-- 分页查询 查询前3条数据
select  *  from 学生表 limit 3;
-- 分页查询 查询3到5条数据
select  *  from 学生表 limit 3,5;
```

## 6、INSERT INTQ  SELECT语句

> <h3>6-1 表2插到表1</h3>
```mysql
inser into 表1  select * from 表2
```
```mysql语法案例
-- 把表2插入到表1
inser into 表1  select * from 表2;
```

## 7、正侧表达式

```mysql
select  'abc' regexp 'a$';
```
```mysql语法案例
select  * from 表名 where regexp '^小明';
```


> ## 8、逻辑运算符

| 逻辑运算符   | 说明     |
| ------------ | -------- |
| NOT 或者 !   | 逻辑非   |
| AND 或者 &&  | 逻辑与   |
| OR 或者 \|\| | 逻辑或   |
| XOR          | 逻辑异或 |








# 五、MySQL的多表操作




# 、约束
--------------------------------------

> <h3>2-1 修改表名</h3>
```mysql
RENAME TABLE 表名 TO 新表名;
```
```mysql语法案例
RENAME TABLE reader  TO 学生表;
```



> <h3>2-1 修改表名</h3>
```mysql
RENAME TABLE 表名 TO 新表名;
```
```mysql语法案例
RENAME TABLE reader  TO 学生表;
```

> <h3>2-1 修改表名</h3>
```mysql
RENAME TABLE 表名 TO 新表名;
```
```mysql语法案例
RENAME TABLE reader  TO 学生表;
```


<h1></h1>

<h2></h2>

<p></p>

```mysql

```

`
ss
`

