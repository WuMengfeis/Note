1、创建一个数据库   create database wumengfei;

2、使用数据库   use wumengfei;

3、查看数据库   show databases;

4、创建一个表格   MariaDB [wumengfei]> create table ww(
    -> name varchar(10),
    -> sex varchar(3));
Query OK, 0 rows affected (0.15 sec)

5、在表格中添加元素   insert into www value("a","A");

6、查看表格元素   select * from www;

7、删除表格元素   delete from www where name="a";

8、更改表格元素   update www set name="b" where sex="nan";

9、根据表格的一个属性（后面的）来查找另一个属性（前面的）   
    select sex from www where name="y";

10、删除表格   drop database wumengfei;

11、查看数据库   show databases;

