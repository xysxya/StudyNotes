LEFT JOIN 是左连接，返回左表中所有的记录以及右表中连接字段相等的记录。

LEFT JOIN 关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。
如果右表中没有匹配，则结果为 NULL。


SQL LEFT JOIN 语法
----------------------------------------------------
SELECT <select_list>
FROM Table A 
LEFT JOIN Table B 
ON A.Key=B.Key;
或：
SELECT column_name(s)
FROM table1
LEFT OUTER JOIN table2
ON table1.column_name=table2.column_name;
----------------------------------------------------
注释：在某些数据库中，LEFT JOIN 称为 LEFT OUTER JOIN。


下面的 SQL 语句将返回所有网站及他们的访问量（如果有的话）。
以下实例中我们把 Websites 作为左表，access_log 作为右表：


----------------------------------------------------
mysql> select websites.name,access_log.count,access_log.date 
    ->from websites 
    ->left join access_log 
    ->on websites.id=access_log.site_id 
    ->order by access_log.count desc;

+---------------+-------+------------+
| name          | count | date       |
+---------------+-------+------------+
| Facebook      |   545 | 2016-05-16 |
| Google        |   230 | 2016-05-14 |
| 菜鸟教程      |   220 | 2016-05-15 |
| Facebook      |   205 | 2016-05-14 |
| 菜鸟教程      |   201 | 2016-05-17 |
| 菜鸟教程      |   100 | 2016-05-13 |
| Google        |    45 | 2016-05-10 |
| 微博          |    13 | 2016-05-15 |
| 淘宝          |    10 | 2016-05-14 |
| stackoverflow |  NULL | NULL       |
+---------------+-------+------------+
10 rows in set (0.00 sec)

mysql> 

----------------------------------------------------

最后一行即使没有匹配，也会返回null值

