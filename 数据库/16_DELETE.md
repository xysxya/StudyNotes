
你可以使用SQL的 DELETE FROM 命令来删除表中的记录，比如某些行。

以下是 SQL DELETE 语句从 MySQL 数据表中删除数据的通用语法：

DELETE FROM table_name [WHERE Clause]

如果没有指定 WHERE 子句，MySQL 表中的所有记录将被删除，表的结构
会被保留。
你可以在 WHERE 子句中指定任何条件，您可以在单个表中一次性删除记录。
当你想删除数据表中指定的记录时 WHERE 子句是非常有用的


--------------操作过程---------------

mysql> delete from websites where name='Facebook' and country='USA'; 
Query OK, 1 row affected (0.00 sec)

mysql> select * from websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | TAOBAO       | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  4689 | CN      |
|  4 | 微博         | http://weibo.com/       |    20 | CN      |
+----+--------------+-------------------------+-------+---------+
4 rows in set (0.01 sec)

mysql> 

--------------操作过程---------------

delete，drop，truncate 都有删除表的作用，区别在于：

 1、delete 和 truncate 仅仅删除表数据，drop 连表数据和表结构一起删除，
 打个比方，delete 是单杀，truncate 是团灭，drop 是把电脑摔了。
 2、delete 是 DML 语句，操作完以后如果没有不想提交事务还可以回滚，truncate 和
  drop 是 DDL 语句，操作完马上生效，不能回滚，打个比方，delete 是发微信说分手，后
  悔还可以撤回，truncate 和 drop 是直接扇耳光说滚，不能反悔。
 3、执行的速度上，drop>truncate>delete，打个比方，drop 是神舟火箭，truncate 是和
 谐号动车，delete 是自行车。

