# mysql-final-test

2019-2020 mysql final test

姓名：童言

学号：17061902

说明1：考试为开卷，可以上网，自觉不要相互电话和QQ；

说明2：考试时间为：2020 年 4 月 10 日 8:10分-9:40分。

说明3：试题比较多，抓紧时间，超时提交的github commit不被接受。未避免完全超时提交，可以在做题过程中多 commit 几次。

说明4：结束后发邮件给 42225@hdu.edu.cn 标题为“MySQL期末考试,姓名+学号”，内容为github链接。


## 1 打印当前时间（例如 2020-04-07 13:41:42），写出SQL语句和结果
```sql
 select now();
 ```
 ### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/%E6%89%93%E5%8D%B0%E5%BD%93%E5%89%8D%E6%97%B6%E9%97%B4.png)

### 2 组合打印自己的姓名和学号
```sql
INSERT INTO user VALUES("tongyan+17061902");
SELECT*FROM user;
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/%E8%BE%93%E5%87%BA%E5%AD%A6%E5%8F%B7%2B%E5%A7%93%E5%90%8D.png)


## 3 建立如下表1和表2，写出建表语句和插入语句。

### 表1：其中deptno为主键
```sql
CREATE TABLE dept_100(
deptno INT PRIMARY KEY,
dname VARCHAR(20),
loc VARCHAR(40)
);

INSERT INTO dept_100(deptno,dname,loc)VALUES(10, "ACCOUNTING", "NEW YORK"),
(20, "RESEARCH", "DALLAS"),
(30, "SALES", "CHICAGO"),
(40, "OPERATIONS", "BOSTON");

SELECT * FROM dept_100;
```
#### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3%E9%A2%98%E8%A1%A81.png)


表2：其中empno字段为主键
```sql
CREATE TABLE dept_10(
empno INT PRIMARY KEY, 
ename VARCHAR(40),   
job VARCHAR(40),    
MGR INT,  
Hiredate VARCHAR(40),   
 sal INT,  
 comm INT, 
deptno INT
);


  INSERT INTO dept_10(empno, ename,    job,    MGR,   Hiredate,    sal,   comm, deptno)
   VALUES (7369, "SMITH", "CLERK", 7902, "1981-03-12", 800.00, NULL, 20),
	(7499, "ALLEN", "SALESMAN", 7698, "1982-03-12", 1600, 300, 30),
	(7521, "WARD", "SALESMAN", 7698, "1838-03-12", 1250, 500, 30),
	(7566, "JONES", "MANAGER", 7839, "1981-03-12", 2975, NULL, 20),
	(7654, "MARTIN", "SALESMAN", 7698, "1981-01-12", 1250, 1400, 30),
	(7698, "BLAKE", "MANAGER", 7839, "1985-03-12", 2450, NULL, 10),
	(7788, "SCOTT", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
	(7839, "KING", "PRESIDENT", NULL, "1981-03-12", 5000, NULL, 10),
	(7844, "TURNER", "SALESMAN", 7689, "1981-03-12", 1500, 0, 30),
	(7878, "ADAMS", "CLERK", 7788, "1981-03-12", 1100, NULL,20),
	(7900, "JAMES", "CLERK", 7698,"1981-03-12",  950, NULL, 30),
	(7902, "FORD", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
	(7934, "MILLER", "CLERK", 7782, "1981-03-12", 1300, NULL, 10);

SELECT * FROM dept_10;
```
#### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3%E9%A2%98%E8%A1%A82.png)

## 3.1 表2 中再插入一条记录：
```sql
INSERT INTO dept_10(empno, ename,    job,    MGR,   Hiredate,    sal,   comm, deptno)
   VALUES (17061902, "Tongyan", "STUDENT", 7782, "2000-03-12", NULL, NULL, 10);
   ```
#### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.1%E6%8F%92%E5%85%A5%E6%95%B0%E6%8D%AE.png)

## 3.2 表中入职时间（Hiredate字段）最短的人。
```sql
select ename,min(hiredate)from dept_10;
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.1.png)


## 3.3 有几种职位（job字段）？在关系代数中，本操作是什么运算？
```sql
SELECT DISTINCT job
FROM dept_10;
```

### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.3.png)

## 3.4 将 MILLER 的 comm 增加 100； 然后，找到 comm 比 MILLER 低的人；
```sql
update dept_10
set comm+comm+100 where ename='mitter';
select*from dept_10 where comm<=(select sal from dept_100 where ename='mitter');
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.4.png)

## 3.5 计算每个人的收入(ename, sal + comm)；计算总共有多少人；计算所有人的平均收入。 提示：计算时 NULL 要当做 0 处理； 
```sql
select ename,(sal+comm)from dept_10
WHERE NOT comm=0;

SELECT COUNT(*)  number
FROM dept_10;

select avg(salary+comm)average
from dept_10
where not comm=0;

```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/%E6%80%BB%E4%BA%BA%E6%95%B0.png)
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/%E5%B9%B3%E5%9D%87%E5%B7%A5%E8%B5%84.png)



## 3.6 显示每个人的下属, 没有下属的显示 NULL。本操作使用关系代数中哪几种运算？
```sql
SELECT empno, ename,job,dname,loc
FROM dept_100  INNER JOIN dept_10
ON dept_100.deptno=dept_10.deptno;
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.6.png)

## 3.7 建立一个视图：每个人的empno, ename, job 和 loc。简述为什么要建立本视图。
```sql
create view v1
as select empno,ename,job,loc
FROM dept_100  INNER JOIN dept_10
ON dept_100.deptno=dept_10.deptno;
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.7.png)

## 3.8 为表2增加一个约束：deptno字段需要在表1中存在；这称做什么完整性？
```sql
alter dept_10
constraint dept_10_fk2 foreign key(deptno) references dept_100(depno);
```
这叫做参照完整性。

## 3.9 为表2增加一个索引：ename 字段。简述为什么要在 ename 字段建立索引
```sql
create index indexname on dept_10(ename);
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.9.png)

## 3.10 将表2的 sal 字段改名为 salary
```sql
alter table dept_10
change sal salary INT;
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.10.png)

## 3.11 撰写一个函数 get_deptno_from_empno，输入 empno，输出对应的 deptno。 简述函数和存储过程有什么不同。
```sql
delimiter $$
create function get_deptno_from_empno(empno int)
returns int
begin
return(select deptno from dept_10 where dept_10.empno=empno);
end$$
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/3.11.png)

## 4 建立一个新用户，账号为自己的姓名拼音，密码为自己的学号；
```sql
CREATE USER 'Tongyan'@'localhost' IDENTIFIED BY '17061902';
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/4.png)

## 4.1 将表1的SELECT, INSERT, UPDATE(ename)权限赋给该账号。
```sql
grant SELECT, INSERT, UPDATE(ename) on dept_100.* to test@localhost identified by '1234';
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/4.1.png)

## 4.2 显示该账号权限
```sql
show grants;
```
### 运行结果
 ![](https://github.com/ty0816/mysql-final-test/blob/master/photo/4.2.png)

## 4.3 `with grant option` 是什么意思。
### 答：WITH GRANT OPTION 这个选项表示该用户可以将自己拥有的权限授权给别人。

## 5 表 1 和表 2 这样设计是否符合第一范式，是否符合第二范式，为什么？
### 答：符合第一范式，因为列的区分很明显已经不能够再分成其他几列；但不符合第二范式，因为第二范式的规定一是表必须有一个主键；二是没有包含在主键中的列必须完全依赖于主键，而不能只依赖于主键的一部分，而该两表有主键，但没有完全依赖主键。

## 6 画出表 1 和表 2 所对应的 E-R 图
![](https://github.com/ty0816/mysql-final-test/blob/master/photo/IMG_20200410_115128.jpg)

## 7 什么是外模式，什么是内模式。为什么要分成这几层？
### 答：外模式：外模式又称子模式或用户模式，对应于用户级。它是某个或某几个用户所看到的数据库的数据视图，是与某一来应用有关的数据的逻辑表示。外模式是从模式导出的一个子集，包含模式中允许特定用户使用的那部分数据。外模式反映了数据库的用户观。内模式又称存储模式，百对应于物理级，它是数据库中全体数据的内部表示或底层描述，是数据库最低一级的逻辑描述，它描述了数据在存度储问介质上的存储方式和物理结构，对应着实际存储在外存储介质上的数据库。内模式由内模式描述语言来描述、定义，它是数据库的存储观。在一个数据库系统中，只有唯一的数据库， 因而作为定义 、描述数据库存储结构的内模式和定义、描述数据库逻辑结答构的模式，也是唯一的，但建立在数据库系统之上的应用则是非常广泛、多样的，所以对应的外模式不是唯一的，也不可能是唯一的。

## 8 什么是ACID？
### 答：ACID，指数据库事务正确执行的四个基本要素的缩写。包含：原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）、持久性（Durability）。

## 8.1 编写一个事务，“将 MILLER 的 comm 增加 100，如果增加后的 comm 大于 1000 则回滚”；

## 8.2 如何查看 MySQL 当前的隔离级别？
```sql
show VARIABLES LIKE 'tx_isolation';
```
### 执行结果
![](https://github.com/ty0816/mysql-final-test/blob/master/photo/%E6%9F%A5%E7%9C%8B%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB.png)
## 8.3 如果隔离级别为 READ-UNCOMMITED, 完成 “MILLER 的 comm 增加 100” 事务操作完成后，可能读到的结果有哪些，原因是什么？

## 9 有哪些场景不适合用关系型数据库？为什么？
### 答：图片，文件，二进制数据，短期数据，日志文件，会使问题更加复杂化，达不到简洁的效果。
