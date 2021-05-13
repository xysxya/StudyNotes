
INNER JOIN 内连接，又叫等值连接，只返回两个表中连接字段相等的行。
关键字在表中存在至少一个匹配时返回行。两者是有交集的

SQL INNER JOIN 语法

----------------------------------------------------
SELECT <select_list>
FROM Table A 
INNER JOIN Table B 
ON A.Key=B.Key
或：

SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name=table2.column_name;
----------------------------------------------------

JOIN INNER 与 JOIN 是一样的没有什么区别

下面的实例是对表wensites和表access_log的操作

----------------------------------------------------
mysql> select websites.name,access_log.count,access_log.date
    -> FROM websites
    -> INNER JOIN access_log
    -> ON websites.id=access_log.site_id
    -> ORDER BY access_log.count;
+--------------+-------+------------+
| name         | count | date       |
+--------------+-------+------------+
| 淘宝         |    10 | 2016-05-14 |
| 微博         |    13 | 2016-05-15 |
| Google       |    45 | 2016-05-10 |
| 菜鸟教程     |   100 | 2016-05-13 |
| 菜鸟教程     |   201 | 2016-05-17 |
| Facebook     |   205 | 2016-05-14 |
| 菜鸟教程     |   220 | 2016-05-15 |
| Google       |   230 | 2016-05-14 |
| Facebook     |   545 | 2016-05-16 |
+--------------+-------+------------+
9 rows in set (0.00 sec)

----------------------------------------------------

补充：
INNER JOIN 关键字在表中存在至少一个匹配时返回行。如果 "Websites" 
表中的行在 "access_log" 中没有匹配，则不会列出这些行。


----------------------------------------------------
在使用 join 时，on 和 where 条件的区别如下：
1、 on 条件是在生成临时表时使用的条件，它不管 on 中的条件是否为真，都
会返回左边表中的记录。
2、where 条件是在临时表生成好后，再对临时表进行过滤的条件。这时已经没有 left join 的含
义（必须返回左边表的记录）了，条件不为真的就全部过滤掉

