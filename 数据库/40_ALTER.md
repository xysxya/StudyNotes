ALTER TABLE 语句用于在已有的表中添加、删除或修改列。

SQL ALTER TABLE 语法
如需在表中添加列，请使用下面的语法:
****************************************************
ALTER TABLE table_name
ADD column_name datatype
****************************************************

如需删除表中的列，请使用下面的语法（请注意，某些数据库系统不允许这种在数据库表中删除列的方式）：
****************************************************
ALTER TABLE table_name
DROP COLUMN column_name
****************************************************

要改变表中列的数据类型，请使用下面的语法：
适用于My SQL
****************************************************
ALTER TABLE table_name
MODIFY COLUMN column_name datatype
****************************************************

对于表person添加一个新的列DateOfBirth数据类型是Date用来存放日期

****************************************************
mysql> select * from person;
+----+-----------+-----------+--------------+-----------+
| id | lastname  | firstname | address      | city      |
+----+-----------+-----------+--------------+-----------+
|  1 | Hansen    | Ola       | Timoteivn 10 | Sandnes   |
|  2 | Svendson  | Tove      | Borgvn 23    | Sandnes   |
|  3 | Pettersen | Kari      | Storgt 20    | Stavanger |
+----+-----------+-----------+--------------+-----------+
3 rows in set (0.00 sec)

mysql> alter table person add DateOfBirth date;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0
mysql> select * from person;
+----+-----------+-----------+--------------+-----------+-------------+
| id | lastname  | firstname | address      | city      | DateOfBirth |
+----+-----------+-----------+--------------+-----------+-------------+
|  1 | Hansen    | Ola       | Timoteivn 10 | Sandnes   | NULL        |
|  2 | Svendson  | Tove      | Borgvn 23    | Sandnes   | NULL        |
|  3 | Pettersen | Kari      | Storgt 20    | Stavanger | NULL        |
+----+-----------+-----------+--------------+-----------+-------------+
3 rows in set (0.00 sec)

mysql> 

****************************************************

改变数据类型实例
现在，我们想要改变 "Persons" 表中 "DateOfBirth" 列的数据类型。

我们使用下面的 SQL 语句：
****************************************************
ALTER TABLE Persons
ALTER COLUMN DateOfBirth year
****************************************************
请注意，现在 "DateOfBirth" 列的类型是 year，可以存放 2 位或 4 位格式的年份。

DROP COLUMN 实例
接下来，我们想要删除 "Person" 表中的 "DateOfBirth" 列。

我们使用下面的 SQL 语句：
****************************************************
ALTER TABLE Persons
DROP COLUMN DateOfBirth
****************************************************

