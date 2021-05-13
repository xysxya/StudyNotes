在默认的情况下，表的列接受 NULL 值。
NOT NULL 约束强制列不接受 NULL 值。

NOT NULL 约束强制字段始终包含值。这意味着，如果不向字段添加值，就无法插入新记录或者更新记录。

下面的 SQL 强制 "ID" 列、 "LastName" 列以及 "FirstName" 列不接受 NULL 值：
----------------------------------------------------
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
----------------------------------------------------

对于一个已经创建好的表添加NOT NULL
----------------------------------------------------
ALTER TABLE Persons
MODIFY Age int NOT NULL;
----------------------------------------------------


在一个已创建的表的 "Age" 字段中删除 NOT NULL 约束如下所示：
----------------------------------------------------
ALTER TABLE Persons
MODIFY Age int NULL;
----------------------------------------------------
