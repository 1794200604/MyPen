## MySQL建表约束

#### 1.主键约束(primary key)

##### 	它能够唯一确定一张表中的一条记录，也就是我们通过某个字段添加约束，就可以使得
改字段不重复且不为空

```mysql
create table user(
	id int primary key,
	name varchar(20)
);

insert into user values(1, '张三');

insert into user values(2, '张三');
当列表里有张三的时候报错：
ERROR 1062 (23000): Duplicate entry '1' for key 'user.PRIMARY'

-- 联合主键
-- 只要联合的主键值加起来不重复就可以（只要有一个或以上的值不同就可以了）
(从id和name两个条件去约束)：
create table user2(
	id int,
	name varchar(20),
	password varchar(20),
	primary key(id, name)
);

insert into user2 values(1, '张三', '123');
insert into user2 values(2, '张三', '123');
```

#### 2.自增约束(auto_increment)

```mysql
create table user3(
	id int primary key auto_increment,
	name varchar(20)
);

insert into user3 (name) values('张三');
```

#### 3.如果创建表的时候，忘记创建主键约束

```mysql
create table user4(
	id int,
	name varchar(20)
);

-- 添加主键约束
alter table user4 add primary key(id);
```

#### 4.删除主键约束

```mysql

```



#### 5.用modify修改字段，添加约束

```mysql

```



#### 6.唯一约束(unique)

```mysql

```



#### 7.删除唯一约束

#### 8.非空约束(not null)

#### 9.默认约束(default)

#### 10.外键约束(foreign key)