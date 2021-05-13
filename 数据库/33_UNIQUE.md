SQL UNIQUE 约束
UNIQUE 约束唯一标识数据库表中的每条记录。

UNIQUE 和 PRIMARY KEY 约束均为列或列集合提供了唯一性的保证。

PRIMARY KEY 约束拥有自动定义的 UNIQUE 约束。

请注意，每个表可以有多个 UNIQUE 约束，但是每个表只能有一个 PRIMARY KEY 约束。
CREATE TABLE 时的 SQL UNIQUE 约束
下面的 SQL 在 "Persons" 表创建时在 "P_Id" 列上创建 UNIQUE 约束：

MySQL：
****************************************************
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
UNIQUE (P_Id)
)
****************************************************

ALTER TABLE 时的 SQL UNIQUE 约束
当表已被创建时，如需在 "P_Id" 列创建 UNIQUE 约束，请使用下面的 SQL：

****************************************************
ALTER TABLE Persons
ADD UNIQUE (P_Id)
****************************************************

如需命名 UNIQUE 约束，并定义多个列的 UNIQUE 约束，请使用下面的 SQL 语法：

****************************************************
ALTER TABLE Persons
ADD CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName)
****************************************************


如需撤销 UNIQUE 约束，请使用下面的 SQL：

MySQL：
****************************************************
ALTER TABLE Persons
DROP INDEX uc_PersonID
****************************************************

实例一
#######################################################################
create table tb2(
    id int unique,
    name varchar(20),
    age int,
    unique(tb2_name)
);

mysql> insert into tb2(id,name,age) values (1,'张三',20);
Query OK, 1 row affected (0.01 sec)

下面语句违反了唯一约定
****************************************************
mysql> insert into tb2 values (2,'张三',25);
ERROR 1062 (23000): Duplicate entry '张三' for key 'tb2.name'
mysql> 
****************************************************
#######################################################################

实例二
#######################################################################
mysql> create table tb3(
    -> id int,
    -> name varchar(20),
    -> age int,
    -> constraint no_id unique(id)
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> insert into tb3 values (1,'张三',20);
Query OK, 1 row affected (0.00 sec)

mysql> insert into tb3(id,age) values(2,24);
Query OK, 1 row affected (0.01 sec)

mysql> select * from tb3;
+------+--------+------+
| id   | name   | age  |
+------+--------+------+
|    1 | 张三   |   20 |
|    2 | NULL   |   24 |
+------+--------+------+
2 rows in set (0.00 sec)

--已经有了id为1的行记录，再次插入，违反唯一约束
****************************************************
mysql> insert into tb3(id,name,age) values(1,'李四',20);
ERROR 1062 (23000): Duplicate entry '1' for key 'tb3.no_id'
mysql> 
****************************************************

--给tb3表添加主键约束，主键名为：pk_id
alter table tb3 add constraint pk_id primary key (id);

--给name添加唯一约束
alter table tb3 add constraint un_name unique (name);


#######################################################################

