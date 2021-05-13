SQL join 用于把来自两个或多个表的行结合起来,基于这些表之间的共同字段。

下图展示了 LEFT JOIN、RIGHT JOIN、INNER JOIN、OUTER JOIN 相关的 7 种用法。

SELECT <select_list>
FROM Table A 
LEFT JOIN Table B 
ON A.Key=B.Key;

SELECT <select_list>
FROM Table A 
LEFT JOIN Table B 
ON A.Key=B.Key
WHERE B.Key IS NULL 

SELECT <select_list>
FROM Table A 
FULL OUTER JOIN Table B
ON A.Key=B.Key

SELECT <select_list>
FROM Table A 
INNER JOIN Table B 
ON A.Key=B.Key

SELECT <select_list>
FROM Table A
FULL OUTER JOIN Table B 
ON A.Key=B.Key
WHERE A.Key IS NULL
OR B.Key IS NULL

SELECT <select_list>
FROM Table
RIGHT JOIN Table
ON A.KEY=B.KEY
WHERE A.KEY IS NULL

SELECT <select_list>
FROM Table
RIGHT JOIN Table
ON A.KEY=B.KEY


最常见的 JOIN 类型：SQL INNER JOIN（简单的 JOIN）。 
SQL INNER JOIN 从多个表中返回满足 JOIN 条件的所有行。

----------------------------------------------------
SELECT <select_list>
FROM Table A 
INNER JOIN Table B 
ON A.Key=B.Key
----------------------------------------------------

下面是两个表
----------------------------------------------------
mysql> select * from websites;
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+----+--------------+---------------------------+-------+---------+
mysql> select * from access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
+-----+---------+-------+------------+

----------------------------------------------------

请注意，"Websites" 表中的 "id" 列指向 "access_log" 表中的字段 "site_id"。
上面这两个表是通过 "site_id" 列联系起来的。然后，如果我们运行下面的 SQL 语句（包含 INNER JOIN）：

----------------------------------------------------
mysql> select websites.id,websites.name,access_log.count,access_log.date
    -> from websites
    -> inner join access_log
    -> on websites.id=access_log.site_id;

+----+--------------+-------+------------+
| id | name         | count | date       |
+----+--------------+-------+------------+
|  1 | Google       |    45 | 2016-05-10 |
|  3 | 菜鸟教程     |   100 | 2016-05-13 |
|  1 | Google       |   230 | 2016-05-14 |
|  2 | 淘宝         |    10 | 2016-05-14 |
|  5 | Facebook     |   205 | 2016-05-14 |
|  4 | 微博         |    13 | 2016-05-15 |
|  3 | 菜鸟教程     |   220 | 2016-05-15 |
|  5 | Facebook     |   545 | 2016-05-16 |
|  3 | 菜鸟教程     |   201 | 2016-05-17 |
+----+--------------+-------+------------+
9 rows in set (0.00 sec)

mysql> 

----------------------------------------------------


不同的 SQL JOIN
在我们继续讲解实例之前，我们先列出您可以使用的不同的 SQL JOIN 类型：

INNER JOIN：如果表中有至少一个匹配，则返回行
LEFT JOIN：即使右表中没有匹配，也从左表返回所有的行
RIGHT JOIN：即使左表中没有匹配，也从右表返回所有的行
FULL JOIN：只要其中一个表中存在匹配，则返回行