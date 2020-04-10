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

### 2 组合打印自己的姓名和学号
```sql
INSERT INTO user VALUES("tongyan+17061902");
SELECT*FROM user;
```
### 运行结果



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



表2：其中empno字段为主键
```sql
CREATE TABLE dept_10(
empno INT, 
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

## 3.1 表2 中再插入一条记录：
```sql
INSERT INTO dept_10(empno, ename,    job,    MGR,   Hiredate,    sal,   comm, deptno)
   VALUES (17061902, "Tongyan", "STUDENT", 7782, "2000-03-12", NULL, NULL, 10);
   ```
#### 运行结果


## 3.2 表中入职时间（Hiredate字段）最短的人。
```sql
select ename,min(hiredate)from dept_10;
```
### 运行结果

## 3.3 有几种职位（job字段）？在关系代数中，本操作是什么运算？


## 3.4 将 MILLER 的 comm 增加 100； 然后，找到 comm 比 MILLER 低的人；
```sql
update dept_10
set comm+comm+100 where ename='mitter';
select*from dept_10 where comm<=(select sal from dept_100 where ename='mitter');
```
### 运行结果

## 3.5 计算每个人的收入(ename, sal + comm)；计算总共有多少人；计算所有人的平均收入。 提示：计算时 NULL 要当做 0 处理； 

## 3.6 显示每个人的下属, 没有下属的显示 NULL。本操作使用关系代数中哪几种运算？
```sql
select*
from((dept_10 t1 inner join dept_10 t2 on t1.mgr=t2.empno)inner join t3 on ta.mgr=t3.empno)inner join t4
on t3.mgr=t4.empno;

```
## 3.7 建立一个视图：每个人的empno, ename, job 和 loc。简述为什么要建立本视图。

## 3.8 为表2增加一个约束：deptno字段需要在表1中存在；这称做什么完整性？


## 3.9 为表2增加一个索引：ename 字段。简述为什么要在 ename 字段建立索引

## 3.10 将表2的 sal 字段改名为 salary

## 3.11 撰写一个函数 get_deptno_from_empno，输入 empno，输出对应的 deptno。 简述函数和存储过程有什么不同。

## 4 建立一个新用户，账号为自己的姓名拼音，密码为自己的学号；

## 4.1 将表1的SELECT, INSERT, UPDATE(ename)权限赋给该账号。

## 4.2 显示该账号权限

## 4.3 `with grant option` 是什么意思。

## 5 表 1 和表 2 这样设计是否符合第一范式，是否符合第二范式，为什么？

## 6 画出表 1 和表 2 所对应的 E-R 图

## 7 什么是外模式，什么是内模式。为什么要分成这几层？
### 答：外模式：外模式又称子模式或用户模式，对应于用户级。它是某个或某几个用户所看到的数据库的数据视图，是与某一来应用有关的数据的逻辑表示。外模式是从模式导出的一个子集，包含模式中允许特定用户使用的那部分数据。外模式反映了数据库的用户观。内模式又称存储模式，百对应于物理级，它是数据库中全体数据的内部表示或底层描述，是数据库最低一级的逻辑描述，它描述了数据在存度储问介质上的存储方式和物理结构，对应着实际存储在外存储介质上的数据库。内模式由内模式描述语言来描述、定义，它是数据库的存储观。在一个数据库系统中，只有唯一的数据库， 因而作为定义 、描述数据库存储结构的内模式和定义、描述数据库逻辑结答构的模式，也是唯一的，但建立在数据库系统之上的应用则是非常广泛、多样的，所以对应的外模式不是唯一的，也不可能是唯一的。

## 8 什么是ACID？
### 答：ACID，指数据库事务正确执行的四个基本要素的缩写。包含：原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）、持久性（Durability）。

## 8.1 编写一个事务，“将 MILLER 的 comm 增加 100，如果增加后的 comm 大于 1000 则回滚”；

## 8.2 如何查看 MySQL 当前的隔离级别？

## 8.3 如果隔离级别为 READ-UNCOMMITED, 完成 “MILLER 的 comm 增加 100” 事务操作完成后，可能读到的结果有哪些，原因是什么？

## 9 有哪些场景不适合用关系型数据库？为什么？
### 答：图片，文件，二进制数据，短期数据，日志文件，
