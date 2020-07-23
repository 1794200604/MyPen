# MySQL使用

#### 1.登录数据库服务器

​	mysql -u XiaoYu -p 1535284697

#### 2.查询数据库中所有的数据库

​	

```mysql
mysql>show databases;
```



#### 3.选中某一个数据库进行操作

```mysql
	mysql>use mysql
	mysql>select * from 数据库名字;
```



#### 4.创建数据库

```mysql
	mysql>create database 数据库名字;
```



#### 5.查看某个数据库中所有的数据表

```mysql
	mysql>show tables;
```



#### 6.创建一个数据表

```mysql
	mysql> CREATE TABLE pet(
        name VARCHAR(20),
        woner VARCHAR(20), 
        species VARCHAR(20),
        sex CHAR(1), 
        birth DATE,death DATE);
```



#### 7.查看创建好的数据表的数据

```mysql
	mysql>describe 数据表名字;
```



#### 8.查看数据表中的记录

```mysql
	mysql>select * from 数据表名字;
```



#### 9.在数据表中添加数据记录

```mysql
	mysql>INSERT INTO 数据表名字
	>VALUES('puffball', 'Diane', 'hamster', 'f', '1999-03-30', NULL);
```



#### 10.MySQL支持多种类型，大致可以分为三类：

```mysql
create table testType(
	number TINYINT
);

INSERT INTO testType VALUES(127);

(1)数据类型
(2)日期和时间类型
(3)字符串类型
```



#### 11.插入数据

```mysql
INSERT INTO pet VALUES('Fluffy', 'Harold', 'cat', 'f', '1999-02-04', NULL);
```



#### 12.删除数据

```mysql
delete from pet where name='Fluffy';
```



#### 13.修改数据

```mysql
update pet set name='可爱多' where name='Fluffy';
```



#### 14.总结

```mysql
(1)增加
insert
(2)删除
delete
(3)修改
update
(4)查询
select
```

