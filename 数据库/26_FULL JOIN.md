SQL FULL OUTER JOIN 外连接，返回两个表中的行，相当于left join + right join。
只要左表（table1）和右表（table2）其中一个表中存在匹配，则返回行.


SQL FULL OUTER JOIN 语法
----------------------------------------------------
SELECT <select_list>
FROM Table A 
FULL OUTER JOIN Table B
ON A.Key=B.Key
----------------------------------------------------

下面的 SQL 语句选取所有网站访问记录。

注意：MySQL中不支持 FULL OUTER JOIN
你可以在 SQL Server 测试以下实例。

----------------------------------------------------
SELECT Websites.name, access_log.count, access_log.date
FROM Websites
FULL OUTER JOIN access_log
ON Websites.id=access_log.site_id
ORDER BY access_log.count DESC;
----------------------------------------------------

注释：FULL OUTER JOIN 关键字返回左表（Websites）和右表（access_log）中所有
的行。如果 "Websites" 表中的行在 "access_log" 中没有匹配或者 "access_log" 表中的行
在 "Websites" 表中没有匹配，也会列出这些行。

----------------------------------------------------
补充：
A inner join B 取交集。

A left join B 取 A 全部，B 没有对应的值为 null。

A right join B 取 B 全部 A 没有对应的值为 null。

A full outer join B 取并集，彼此没有对应的值为 null。

对应条件在 on 后面填写。

