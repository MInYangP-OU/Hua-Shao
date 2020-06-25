```mysql
net start mysql
net stop mysql
mysql -u root -p
exit;

#不带FROM子句的SELECT语句有一个有用的用途，就是用来判断当前到数据库的连接是否有效。许多检测工具会执行一条SELECT 1;来测试数据库连接。
select now();
select version();
select curtime();
select curdate();
select user();
select database(); 	#查看正在使用的数据库

#show + variable
#两个重要的变量
---------------------------------
show databases;   show tables;
---------------------------------
show databases; 	#显示所有数据库

#使用数据库
use learn_mysql;
#没有使用表，我们站在整个数据库角度 创建 查看 修改 和删除表

#创建和删除
create database demo;
drop database demo;

#使用表
show tables; 	#显示所有表
desc students; 	#显示表结构

#提示符修改
prompt \U $

#创建表
show tables; 	#查看当前数据库中所有表

字段名 字段类型 字段约束
create table students (
	id int unsigned primary key auto_increment,
	name varchar(15) not null ,
	age tinyint unsigned default 18,
	high decimal(5,2) default 160.0,
	gender enum('男','女','中性','保密') default '保密',
	cls_id int unsigned not null
);

show create table students;

select * from classes; 	#显示表中所有内容
delete from classes; 	#将表中记录清空
drop table students; 	#删除表

#表结构增删改查
alter add添加字段/modify修改指定字段结构/change名称和类型
alter table students add birthday datetime default "2011-1-1 12:12:12";

alter table students modify borthday data default "2020-11-11";

alter table students change birthday birth date default "2000-1-1";

alter table students drop birth;

  

#数据增删改查
insert [into] classes values (0, '一班'), (0, '二班'), (0, '三班');

#定义外键约束
ALTER TABLE students
ADD CONSTRAINT fk_class_id
FOREIGN KEY (class_id)
REFERENCES classes (id);

#删除外键约束
ALTER TABLE students
DROP FOREIGN KEY fk_class_id;

#索引

#基本查询
* 表示所有列
#查询指定行
SELECT * FROM students WHERE (score < 80 OR score > 90) AND gender = 'M';

WHERE score BETWEEN 60 AND 90
WHERE score >= 60 AND score <= 90

#投影查询 --仅返回指定列
SELECT id, score points, name FROM students;
#排序
SELECT id, name, gender, score FROM students ORDER BY score;

#默认从低到高ASC
order by score DESC

#分页查询
SELECT id, name, gender, score
FROM students
ORDER BY score DESC
LIMIT 3 OFFSET 0;

#每页三个，从结果集第0个开始
-------------------------
0 1 2
3 4 5
6 7 8
9
-------------------------
# LIMIT总是设定为pageSize；
# OFFSET计算公式为pageSize * (pageIndex - 1)。
# 在MySQL中，LIMIT 15 OFFSET 30还可以简写成LIMIT 30, 15

#聚合查询 查询满足条件的所有行数
SELECT COUNT(*) boys FROM students WHERE gender = 'M';

# 函数
SELECT AVG(score) average FROM students WHERE gender = 'M';
sum()
max()
min()
#分组聚合查询
--------
#多表查询
SELECT * FROM students, classes;

#连接查询
SELECT s.id, s.name, s.class_id, s.gender, s.score FROM students s;
```

```mysql
#关系数据库的基本操作就是增删改查
CRUD
create retrieve update delete

select #查询

#增 insert
#删 delete
#改 update

#增加记录
INSERT INTO students (class_id, name, gender, score) VALUES (2, '帅帅', 'M', 80);

INSERT INTO students (class_id, name, gender, score) VALUES
  (1, '大宝', 'M', 87),
  (2, '二宝', 'M', 81);
  
 #更改表中的数据
UPDATE students SET name='大牛', score=66 WHERE id=1;
#更新表中字段可以使用表达式
UPDATE students SET score=score+10 WHERE score<80;

#更新注意
----------------------------
UPDATE students SET score=60;
#整个表的记录都会被更改
#最好先用 select where 测试，看看是否选择了需要更改的内容

#删除表中的记录
DELETE FROM students WHERE id=1;

```

```
MYSQL Server ---mysqld
MYSQL Client ---mysql  --> SQL-TCP   MYSQL Server
默认端口号3306
即如果发送到本机的 mysql server服务器
地址就是 127.0.0.1：3306

仅安装mysql client 可以连接到远程 MySQLserver
假设远程mysql server 的ip地址是10.0.1.99
-h 指定ip地址和域名
mysql -h 10.0.1.99 -u root -p

命令行程序mysql实际上是MySQL客户端，真正的MySQL服务器程序是mysqld，在后台运行。

```

```mysql
#实战

show databases;		#展示数据库
create database test;		#创建数据库
drop database test;		#删除数据库

use test;		#切换到当前数据库
show tables;		#展示所有的表

desc student;		#查看某个表的表结构
show create table students;		#查看创建表的sql语句

drop table students;		#删除表

#修改表

alter table students add column birth varchar(10) not null;		#新增一列birth

alter table students change column birth birthday varchar(20) not null;		#修改一列的列名和列的数据结构
alter table students drop column birthday;		#删除列


#实用sql语句
插入与替换 原有记录已存在
先删除再添加
可直接替换
replace into students (id, class_id, name, gender, score) values (1, 1, '小米', 'F', 99);

#插入或更新
无则插入，有则更新
INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99) ON DUPLICATE KEY UPDATE name='小明', gender='F', score=99;
#插入或忽略
无则插入，有则忽略
INSERT IGNORE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);

------------------
# 快照
对一个表进行快照，即复制一份表的数据到一个新表
可以结合create table 和 select
CREATE TABLE students_of_class1 SELECT * FROM students WHERE class_id=1;
新表结构和原表一样

#写入查询结果
insert select 
#创建一个统计成绩的结果表
CREATE TABLE statistics (
    id BIGINT NOT NULL AUTO_INCREMENT,
    class_id BIGINT NOT NULL,
    average DOUBLE NOT NULL,
    PRIMARY KEY (id)
);

一条语句写入全班的平均成绩
INSERT INTO statistics (class_id, average) SELECT class_id, AVG(score) FROM students GROUP BY class_id;

#强制使用指定索引
SELECT * FROM students FORCE INDEX (idx_class_id) WHERE class_id = 1 ORDER BY id DESC;

```

```mysql
#事务操作
把多条语句作为一个整体进行操作的功能，被称为数据库事务。数据库事务可以确保该事务范围内的所有操作都可以全部成功或者全部失败。如果事务失败，那么效果就和没有执行这些SQL一样，不会对数据库数据有任何改动。
ACID
原子性，一致性，隔离性，持久性
对于单条SQL语句，数据库系统自动将其作为一个事务执行，这种事务被称为隐式事务。

#显示事务
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
试图把事务内的所有SQL所做的修改永久保存。如果COMMIT语句执行失败了，整个事务也会失败
有些时候，我们希望主动让事务失败，这时，可以用ROLLBACK回滚事务，整个事务会失败：

BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
ROLLBACK;
#事务隔离

```

