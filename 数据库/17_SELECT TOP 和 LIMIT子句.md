SQL SELECT TOP 子句

SELECT TOP 子句用于规定要返回的记录的数目。

SELECT TOP 子句对于拥有数千条记录的大型表来说，是非常有用的。

注意:并非所有的数据库系统都支持 SELECT TOP 语句。MySQL
 支持 LIMIT 语句来选取指定的条数数据， Oracle 可以使用 ROWNUM 来选取。

以下我们只列出MYSQL的语法，SQL Sever 和 Oracle我们不列出来。
MySQL 语法
----------------------------------------------------
SELECT column_name(s)
FROM table_name
LIMIT number;
----------------------------------------------------

----------------------------------------------------
实例
SELECT *
FROM Persons
LIMIT 5;
----------------------------------------------------

以表websites为例
----------------------------------------------------
mysql> select * from websites limit 2;
+----+--------+-------------------------+-------+---------+
| id | name   | url                     | alexa | country |
+----+--------+-------------------------+-------+---------+
|  1 | Google | https://www.google.cm/  |     1 | USA     |
|  2 | TAOBAO | https://www.taobao.com/ |    13 | CN      |
+----+--------+-------------------------+-------+---------+
2 rows in set (0.01 sec)

mysql> 
----------------------------------------------------

补充说明：
select top 5 * from table

--后5行
select top 5 * from table order by id desc  --desc 
表示降序排列 asc 表示升序