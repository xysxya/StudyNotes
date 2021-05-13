
ORDER BY 关键字用于对结果进行排序。

ORDER BY 关键字默认按照升序对记录进行排序。如果需要按照降序
对记录进行排序，您可以使用 DESC 关键字。

--------------表格-------------------
表名：webisites
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+----+--------------+---------------------------+-------+---------+

--------------表格-------------------
对于表格"websites"我们对列alexa按升序查看数据，使用以下语句

SELECT * FROM Websites
ORDER BY alexa;

--------------操作过程---------------
mysql> select * from websites order by alexa;
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|  2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
+----+--------------+---------------------------+-------+---------+
5 rows in set (0.01 sec)

mysql> 

--------------操作过程---------------

按照降序

SELECT * FROM Websites
ORDER BY alexa DESC;

--------------操作过程---------------
mysql> select * from websites order by alexa desc;
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
+----+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)

mysql> 

--------------操作过程---------------

上面我只选取了一列进行排序，但我们也可以选择两列进行排序

下面的 SQL 语句从 "Websites" 表中选取所有网站，并按照 "country" 
和 "alexa" 列排序：


SELECT * FROM Websites
ORDER BY country,alexa;

--------------操作过程---------------

+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+----+--------------+---------------------------+-------+---------+
5 rows in set (0.00 sec)

mysql> 

--------------操作过程---------------

补充：
order by A,B        这个时候都是默认按升序排列
order by A desc,B   这个时候 A 降序，B 升序排列
order by A ,B desc  这个时候 A 升序，B 降序排列
即 desc 或者 asc 只对它紧跟着的第一个列名有效，其他
不受影响，仍然是默认的升序