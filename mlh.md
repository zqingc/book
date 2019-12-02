## MySQL使用手册

MySQL 登陆

`mysql -h 主机名 -u用户名 -p密码`

1，创建数据库 	`create database 数据库名;`

2，切换到指定数据库	`use 数据库名;`

3，显示数据库列表	`show databases;`

4，显示数据库建立语句	`show create database 数据库名;`

5，修改数据	`alter database 数据库名 选项;`

如 ` alter database itsource charse=gbk;`

6，删除数据库	`drop database 数据库名;`

7，查看数据表列表	`show tables;`

8，查看数据表结构	`desc 数据表名;`

9，查看数据表建表语句	`show create table 数据表名;`

10，删除数据表	`drop table 数据表名;`

11，修改数据表	`alter table 数据表名 选项;`

如	`alter table news charset=utf8;`

12，修改字段定义	`alter table 数据表名 modify column 字段名 新的定义;`

如	`alter table news modify column content longtext;`

13，修改字段名及定义	`alter table 数据表名 change column  旧字段名 新字段名 新的定义;`

14，删除字段	`alter table 数据表名 drop column 字段名;`

15，新增记录	`insert into 数据表名(字段1,字段2,字段n)values(值1,值2,值n);`

如	`insert into news(title,author,content)values('新闻标题','作者','新闻详细内容');`

注意：值的数量与类型必须与字段列表数量与类型定义一致

16，查看记录	`select 字段列表 from 数据表名 where 条件 order by 字段名 desc limit m,n;`

如	`select * from news;`

​		`select * from news where id = 10;`

​		`select * from news order by id desc limit 10;`

17，修改记录	`update 数据表名 set 字段1 = 值1 and 字段2 = 值2 where 条件;`

如	`update news set title = '新的新闻标题' where id =1;`

18，删除记录	`delete from 数据表名 where 条件`

如	`delete from news where id =10;`





