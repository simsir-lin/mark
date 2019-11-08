#### 执行顺序
1. from
2. on
3. outer(join)
4. where
5. group by
6. cube|rollup
7. having
8. select
9. distinct
10. order by
11. top

#### 操作语句
* create table tablename (field datatype not null,,,) -- 新建表
* drop table tablename -- 删除表，清除数据和表结构
* insert into tablename (field,field,,,) values(value,value,,,) -- 插入数据
* update tablename set field=value,field=value,,, -- 没有加where条件则整列赋同一个值,值是中文时前面加N
* delete from tablename -- 删除表的数据,表的结构还在

#### 查询语句
* select [count(field),max(field),min(field),avg(field),sum(field)] from 表名 -- 数量,最大值,最小值,平均值,总和
* select * from tablename order by field ASC(升序)/DESC(降序)
* select * from 表名 where 字段 like '\_lhy' -- \_是单字符通配符,这检索出以lhy结尾的字段
* select * from 表名 where 字段 like '%lhy%' -- %是多字符通配符,这里检索含有lhy的字段
* select * from Person1 where age=20 or age=25 or age=18
等价于 select * from Person1 where age in (20,25,18)
* select distinct field,field,,, from 表名 -- distinct去除重复数据,注意:distinct是对整个结果进行数据重复处理,不是针对每一个列
* select field,field from table1 union all select field,field from table2 -- union两个结果整合在一起,不加all相同的只会显示一条结果
* select field from table1 as name1 join table2 as name2 on name1.field=name2.field\
* select * from table limit m,n -- 其中m是指记录开始的index，从0开始,表示第一条记录n是指从第m+1条开始，取n条


#### 存储过程
* declare 表变量名 数据类型 -- 创建表变量
* create Proc 存储过程名 参数 as 代码 -- 创建存储过程
* exec 存储过程名 -- 调用存储过程
* 好处：减少数据库对SQL语句的解析所消耗的时间，数据库直接调用存储过程
* 坏处：可移植性差，换平台时得重新写存储过程

#### 常识
* sql是单引号
* GETDATE() -- 获取当前日期

#### SQL Server
* varchar与nvarchar的区别：nvarchar支持utf编码

#### MySql
* CREATE DATABASE `test2` DEFAULT CHARACTER SET utf8 -- 创建并设置默认编码
* insert into t1 (stuname,age) select stuname,age from t2 -- 将t2所有数据搬到t1
* int(5)  -- 表示  00005  用0补到5位
* CREATE TABLE `users` (     `id` int(11) NOT NULL AUTO_INCREMENT,     `sessionkey` varchar(255) NOT NULL,   PRIMARY KEY (`id`)   ) ENGINE=MyISAM  DEFAULT CHARSET=utf8;
* ALTER TABLE table_name ADD INDEX index_name (column);  // 新增索引
