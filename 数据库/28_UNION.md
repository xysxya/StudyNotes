 MySQL UNION 操作符的语法和实例。

描述
MySQL UNION 操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合中。多
个 SELECT 语句会删除重复的数据。

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据
类型。同时，每个 SELECT 语句中的列的顺序必须相同。

SQL UNION 语法
----------------------------------------------------
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
----------------------------------------------------
注意：默认地，UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。

SQL UNION ALL 语法
----------------------------------------------------
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
----------------------------------------------------
注释：UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。


下面对于表apps和表websites进行查询
----------------------------------------------------
mysql> select * from websites;
+----+---------------+---------------------------+-------+---------+
| id | name          | url                       | alexa | country |
+----+---------------+---------------------------+-------+---------+
|  1 | Google        | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程      | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博          | http://weibo.com/         |    20 | CN      |
|  5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|  6 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+----+---------------+---------------------------+-------+---------+
6 rows in set (0.00 sec)

mysql> select * from apps;
+----+------------+-------------------------+---------+
| id | app_name   | url                     | country |
+----+------------+-------------------------+---------+
|  1 | QQ APP     | http://im.qq.com/       | CN      |
|  2 | 微博 APP   | http://weibo.com/       | CN      |
|  3 | 淘宝 APP   | https://www.taobao.com/ | CN      |
+----+------------+-------------------------+---------+
3 rows in set (0.00 sec)

mysql> select country from websites
    -> UNION
    -> select country from apps
    -> order by country;
+---------+
| country |
+---------+
| CN      |
| IND     |
| USA     |
+---------+
3 rows in set (0.00 sec)
----------------------------------------------------
UNION 不能用于列出两个表中所有的country。如果一些网站和APP来自
同一个国家，每个国家只会列出一次。UNION 只会选取不同的值。请使用 UNION ALL 来选取重复的值！


下面是一个UNION ALL 的例子

----------------------------------------------------
mysql> select country from websites
    -> union all
    -> select country from apps
    -> order by country;
+---------+
| country |
+---------+
| CN      |
| CN      |
| CN      |
| CN      |
| CN      |
| CN      |
| IND     |
| USA     |
| USA     |
+---------+
9 rows in set (0.00 sec)

mysql> 
----------------------------------------------------

带有where的UNION的语句

----------------------------------------------------
mysql> select country,name from websites
    -> where country='CN'
    -> UNION ALL
    -> select country, app_name from apps
    -> where country='CN'
    -> order by country;
+---------+--------------+
| country | name         |
+---------+--------------+
| CN      | 淘宝         |
| CN      | 菜鸟教程     |
| CN      | 微博         |
| CN      | QQ APP       |
| CN      | 微博 APP     |
| CN      | 淘宝 APP     |
+---------+--------------+
6 rows in set (0.00 sec)

mysql> 
----------------------------------------------------

补充：
----------------------------------------------------
select country from websites union select country from apps;

--连接两个表的查询结果集，重复的不显示

select country from websites union all select country from apps order by country;

--连接俩个个表的查询结果集，显示重复

select country,name from websites where country = 'CN' union all 

select country,app_name from apps where country='CN' order by name; 

--通过where条件查询的结果，连接连个表的结果集，并根据名字排序。
----------------------------------------------------
使用UNION命令时需要注意，只能在最后使用一个ORDER BY命令，是将两个查询结果合在一起之后，再进行排序！
绝对不能写两个ORDER BY命令。

另外，在使用ORDER BY排序时，注意两个结果的别名保持一致，使用别名排序很方便。当然也可以使用列数。
----------------------------------------------------
ORDER BY 除了可以对指定的字段进行排序，还可以使用函数进行排序:

order by abs(a);
ORDER BY 只能当前 SQL 查询结果进行排序，如要对 union all 出来的结果进行排序，需要先做集合。

select aa.* from 
(select country,name from websites where country = 'CN'
union all select country,app_name from apps where country='CN' ) aa
order by aa.name;

----------------------------------------------------



