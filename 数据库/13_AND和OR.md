上一节结尾，但我们想要查询大于20的数据又想查询字符是CN的数据。
这样一个复杂条件需要用到关键字AND。

表示，返回第一个条件和第二个条件都成立的所有数据。



--------------操作过程---------------

mysql> SELECT * FROM websites WHERE  alexa>=20 AND country='CN';
+----+--------------+------------------------+-------+---------+
| id | name         | url                    | alexa | country |
+----+--------------+------------------------+-------+---------+
|  3 | 菜鸟教程     | http://www.runoob.com/ |  4689 | CN      |
|  4 | 微博         | http://weibo.com/      |    20 | CN      |
+----+--------------+------------------------+-------+---------+
2 rows in set (0.00 sec)

mysql> 

--------------操作过程---------------

   如果第一个条件和第二个条件中只要有一个成立，就符合筛选
条件，这时需要用到关键字OR。


下面的 SQL 语句从 "Websites" 表中选取国家为 "USA" 或者 "CN" 的所有客户

SELECT * FROM Websites
WHERE country='USA'
OR country='CN';

--------------操作过程---------------

mysql> select * from websites where country='USA' OR alexa<20;
+----+----------+---------------------------+-------+---------+
| id | name     | url                       | alexa | country |
+----+----------+---------------------------+-------+---------+
|  1 | Google   | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝     | https://www.taobao.com/   |    13 | CN      |
|  5 | Facebook | https://www.facebook.com/ |     3 | USA     |
+----+----------+---------------------------+-------+---------+
3 rows in set (0.00 sec)

mysql> 

--------------操作过程---------------


