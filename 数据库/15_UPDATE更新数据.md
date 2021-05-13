如果我们需要修改或更新 MySQL 中的数据，我们可以使用
 SQL UPDATE 命令来操作。

语法
以下是 UPDATE 命令修改 MySQL 数据表数据的通用 SQL 语法：

UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]

对于表"websites"，我们更改alexa=13这一行数据

--------------操作过程---------------

mysql> update websites set name="TAOBAO" where alexa=13;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from websites;
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
|  2 | TAOBAO       | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+----+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)

mysql> 

--------------操作过程---------------
