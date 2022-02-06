# MySQL

## 一、概述

> 为什么使用数据库？
>
> * 持久化(persistence)：把数据保存到可掉电式存储设备中以供之后使用。大多数情况下，特别是企 业级应用，数据持久化意味着将内存中的数据保存到硬盘上加以”固化”，而持久化的实现过程大多 通过各种关系数据库来完成。 
> * 持久化的主要作用是将内存中的数据存储在关系型数据库中，当然也可以存储在磁盘文件、XML数 据文件中。

### 1.数据库的相关概念

* **DB：数据库（Database）**即存储数据的“仓库”，其本质是一个文件系统。它保存了一系列有组织的数据。
* **DBMS：数据库管理系统（Database Management System）**是一种操纵和管理数据库的大型软件，用于建立、使用和维护数据库，对数据库进行统一管理和控 制。用户通过数据库管理系统访问数据库中表内的数据。
* **SQL：结构化查询语言（Structured Query Language）**专门用来与数据库通信的语言。

### 2.MySQL概述

* MySQL是一种关联数据库管理系统，将数据保存在不同的表中，而不是将所有数据放在一个大仓库 内，这样就增加了速度并提高了灵活性。
* MySQL使用 标准的SQL数据语言 形式。
* MySQL可以允许运行于多个系统上，并且支持多种语言。这些编程语言包括C、C++、Python、 Java、Perl、PHP和Ruby等。

### 3. RDBMS 

> 关系型数据库是 DBMS 的主流，其中使用最多的 DBMS 分别是 Oracle、 MySQL 和 SQL Server。这些都是关系型数据库（RDBMS）。

* 这种类型的数据库是 最古老 的数据库类型，关系型数据库模型是把复杂的数据结构归结为简单的 **二元关系** （即**二维表格形式**）。
* 关系型数据库以 **行(row) 和 列(column)** 的形式存储数据，以便于用户理解。
* SQL 就是关系型数据库的**查询语言**。

### 4. 非关系型数据库(非RDBMS)

> 非关系型数据库，可看成传统关系型数据库的功能 阉割版本 ，基于键值对存储数据，不需要经过SQL层 的解析， 性能非常高 。同时，通过减少不常用的功能，进一步提高性能。

* 键值型数据库
* 文档型数据库
* 搜索引擎数据库
* 列式数据库
* 图形数据库

### 5.. 关系型数据库设计规则

### 6.MySQL基本演示

#### (1)查看所有数据库

> show databases;

#### (2)创建自己的数据库

> create database 数据库名;

#### (3)使用自己的数据库

> use 数据库名;
>
> **说明**：如果没有使用use语句，后面针对数据库的操作也没有加“数据名”的限定，那么会报“ERROR 1046 (3D000): No database selected”（没有选择数据库） 使用完use语句之后，如果接下来的SQL都是针对一个数据库操作的，那就不用重复use了，如果要针对另 一个数据库操作，那么要重新use。

#### (4)查看某个库的所有表格

> show tables from 数据库名;

#### (5)创建新的表格

> create tables 表名(字段名 数据类型, 字段名 数据类型);
>
> **说明**：如果是最后一个字段，后面就用加逗号，因为逗号的作用是分割每个字段。

**实例：**

> \#创建学生表 
>
> create table student( 
>
> ​	id int, 
>
> ​	name varchar(20) #说名字最长不超过20个字符 
>
> );

#### (6)查看一个表的数据

> select * from 数据库**表名**;

#### (7)添加一条记录

> insert into 表名 values(值列表);

**实例：**

> \#添加两条记录到student表中 
>
> insert into student values(1,'张三'); 
>
> insert into student values(2,'李四');

#### (8)查看表的创建信息

> show create table 表名\G

#### (9查看数据库的创建信息

> show create database数据库名\G

#### (10)删除表格

> drop table 表名;

#### (11)删除数据库

> drop database 数据库名;



### 7. SQL 分类

SQL语言在功能上主要分为如下3大类： 

* DDL（Data Definition Languages、数据定义语言），这些语句定义了不同的数据库、表、视图、索 引等数据库对象，还可以用来创建、删除、修改数据库和数据表的结构。 
* * 主要的语句关键字包括 CREATE 、 DROP 、 ALTER 等。 
* DML（Data Manipulation Language、数据操作语言），用于添加、删除、更新和查询数据库记 录，并检查数据完整性。 
* * 主要的语句关键字包括 INSERT 、 DELETE 、 UPDATE 、 SELECT 等。 
  * SELECT是SQL语言的基础，最为重要。 
* DCL（Data Control Language、数据控制语言），用于定义数据库、表、字段、用户的访问权限和 安全级别。 
* * 主要的语句关键字包括 GRANT 、 REVOKE 、 COMMIT 、 ROLLBACK 、 SAVEPOINT 等。



### 8. SQL语言的规则与规范

* SQL 可以写在一行或者多行。为了提高可读性，各子句分行写，必要时使用缩进 
* 每条命令以 ; 或 \g 或 \G 结束 
* 关键字不能被缩写也不能分行 
* 关于标点符号 
* * 必须保证所有的()、单引号、双引号是成对结束的 
  * 必须使用英文状态下的半角输入方式 
  * 字符串型和日期时间类型的数据可以使用单引号（' '）表示 
  * 列的别名，尽量使用双引号（" "），而且不建议省略as

### 9. SQL大小写规范

* MySQL 在 Windows 环境下是大小写不敏感的 
* MySQL 在 Linux 环境下是大小写敏感的 
* * 数据库名、表名、表的别名、变量名是严格区分大小写的 
  * 关键字、函数名、列名(或字段名)、列的别名(字段的别名) 是忽略大小写的。 
* 推荐采用统一的书写规范： 
* * 数据库名、表名、表别名、字段名、字段别名等都小写 
  * SQL 关键字、函数名、绑定变量等都大写

#### 10.注释

* 单行注释：#注释文字(MySQL特有的方式) 
* 单行注释：-- 注释文字(--后面必须包含一个空格。) 
* 多行注释：/* 注释文字 */

### 11. 命名规则

* 数据库、表名不得超过30个字符，变量名限制为29个 
* 必须只能包含 A–Z, a–z, 0–9, _共63个字符 
* 数据库名、表名、字段名等对象名中间不要包含空格 同一个MySQL软件中，数据库不能同名；
* 同一个库中，表不能重名；同一个表中，字段不能重名 
* 必须保证你的字段没有和保留字、数据库系统或常用方法冲突。如果坚持使用，请在SQL语句中使 用`（着重号）引起来 
* 保持字段名和类型的一致性，在命名字段并为其指定数据类型的时候一定要保证一致性。假如数据 类型在一个表里是整数，那在另一个表里可就别变成字符型了





## 二、SQL---SELECT使用

### 1.基本的SELECT语句

#### (1)最基本的select语句

> **SELECT 字段1,字段2,... FROM 表名** 
>
>  
>
> SELECT 1 + 1,3 * 2;
>
> SELECT 1 + 1,3 * 2
>
> FROM DUAL; #dual：伪表

#### (2)* : 所有的字段（或列）

> SELECT * FROM 表名;

#### (3)列的别名

> * as:全称：alias(别名),可以省略
> * 列的别名可以使用一对""引起来，不要使用''。

> SELECT employee_id emp_id  ,last_name AS lname   ,department_id "部门id",salary * 12 **AS** "annual sal"
>
> FROM employees;

#### (4)去除重复行

> SELECT **DISTINCT** 表达某个字段 
>
> FROM employees;

> * 错误的：
>
> SELECT **salary,DISTINCT department_id**
>
> FROM employees;
>
> 
>
> * 仅仅是没有报错，但是没有实际意义。
>
> SELECT **DISTINCT department_id,salary**
>
> FROM employees;

#### (5)空值参与预算

> 空值：null
>
> null不等同于0，‘ ’，‘null’

> * 空值参与运算：结果一定也为空。
>
> SELECT **employee_id,salary "月工资",salary * (1 + commission_pct) * 12 "年工资",commission_pct**
>
> FROM employees;
>
> * 实际问题的解决方案：引入IFNULL
>
> SELECT **employee_id,salary "月工资",salary * (1 + IFNULL(commission_pct,0)) * 12 "年工资",commission_pct**
>
> FROM `employees`;

#### (6)着重号

> 需要保证表中的字段、表名等没有和保留字、数据库系统或常用方法冲突。如果真的相同，请在 SQL语句中使用一对``（着重号）引起来。

#### (7)常数查询

> SELECT **'sf',123**,employee_id,last_name
>
> FROM employees;

#### (8)显示表结构

> 使用DESCRIBE 或 DESC 命令，表示表结构。
>
> **DESCRIBE** employees; 
>
> 或 
>
> **DESC** employees;

#### (9)过滤数据

> * 1.练习：查询90号部门的员工信息
>
> **SELECT** * 
>
> **FROM** employees
>
> \#过滤条件,声明在FROM结构的后面
>
> **WHERE** department_id = 90;
>
> * 2.练习：查询last_name为'King'的员工信息
>
> **SELECT** * 
>
> FROM EMPLOYEES
>
> **WHERE** LAST_NAME = 'King'; 
>
> 注：window下的MySQL不严格区分大小写



### 2.运算符

#### (1)算数运算符

| 运算符   | 名称 | 实例                                |
| -------- | ---- | ----------------------------------- |
| +        | 加   | SELECT A + B                        |
| -        | 减   | SELECT A - B                        |
| *        | 乘   | SELECT A * B                        |
| / 或 DIV | 除   | SELECT A / B  或 SELECT A **DIV** B |
| % 或 MOD | 取余 | SELECT A % B  或 SELECT A **MOD** B |

> * 一个整数类型的值对整数进行加法和减法操作，结果还是一个整数； 
> * 一个整数类型的值对浮点数进行加法和减法操作，结果是一个浮点数； 
> * 加法和减法的优先级相同，进行先加后减操作与进行先减后加操作的结果是一样的； 
> * 在Java中，+的左右两边如果有字符串，那么表示字符串的拼接。但是在MySQL中+只表示数 值相加。如果遇到非数值类型，先尝试转成数值，如果转失败，就按0计算。（补充：MySQL 中字符串拼接要使用字符串函数CONCAT()实现）

> 一个数乘以整数1和除以整数1后仍得原数； 
>
> 一个数乘以浮点数1和除以浮点数1后变成浮点数，数值与原数相等； 
>
> 一个数除以整数后，不管是否能除尽，结果都为一个浮点数； 
>
> 一个数除以另一个数，除不尽时，结果为一个浮点数，并保留到小数点后4位； 
>
> 乘法和除法的优先级相同，进行先乘后除操作与先除后乘操作，得出的结果相同。 
>
> 在数学运算中，0不能用作除数，在MySQL中，一个数除以0为NULL。

#### (2)比较运算符

| 运算符       | 名称     | 实例                              |
| ------------ | -------- | --------------------------------- |
| =            | 等于     | SELECT C FROM TABLE WHERE A = B   |
| <=>          | 安全等于 | SELECT C FROM TABLE WHERE A <=> B |
| <>  或  (!=) | 不等于   | SELECT C FROM TABLE WHERE A <> B  |
| <            | 小于     | SELECT C FROM TABLE WHERE A < B   |
| <=           | 小于等于 | SELECT C FROM TABLE WHERE A <= B  |
| >            | 大于     | SELECT C FROM TABLE WHERE A > B   |
| >=           | 大于等于 | SELECT C FROM TABLE WHERE A >= B  |

> * 等号运算符（=）判断等号两边的值、字符串或表达式是否相等，如果相等则返回1，不相等则返回 0。 
> * 在使用等号运算符时，遵循如下规则： 
> * * 如果等号两边的值、字符串或表达式都为字符串，则MySQL会按照字符串进行比较，其比较的 是每个字符串中字符的ANSI编码是否相等。 
>   * 如果等号两边的值都是整数，则MySQL会按照整数来比较两个值的大小。 
>   * 如果等号两边的值一个是整数，另一个是字符串，则MySQL会将字符串转化为数字进行比较。 
>   * 如果等号两边的值、字符串或表达式中有一个为NULL，则比较结果为NULL。

> 安全等于运算符 安全等于运算符（<=>）与等于运算符（=）的作用是相似的， 唯一的区别 是‘<=>’可 以用来对NULL进行判断。在两个操作数均为NULL时，其返回值为1，而不为NULL；当一个操作数为NULL 时，其返回值为0，而不为NULL。

> 不等于运算符 不等于运算符（<>和!=）用于判断两边的数字、字符串或者表达式的值是否不相等， 如果不相等则返回1，相等则返回0。不等于运算符不能判断NULL值。如果两边的值有任意一个为NULL， 或两边都为NULL，则结果为NULL。

#### (3)非符号类运算符

| 运算符      | 名称             | 作用                                     |
| ----------- | ---------------- | ---------------------------------------- |
| IS NULL     | 为空运算符       | 判断值、字符串或表达式是否为空           |
| IS NOT NULL | 不为空运算符     | 判断值、字符串或表达式是否不为空         |
| LEAST       | 最小值运算符     | 在多个值中返回最小值                     |
| GREATEST    | 最大值运算符     | 在多个值中返回最大值                     |
| BETWEEN AND | 两值之间的运算符 | 判断一个值是否在两个值之间               |
| IN          | 属于运算符       | 判断一个值是否为列表中的任意一个值       |
| NOT IN      | 不属于运算符     | 判断一个值是否不是一个列表中的任意一个值 |
| LIKE        | 模糊匹配运算符   | 判断一个值是否符合模糊匹配规则           |
| PEGEXP      | 正在表达式运算符 | 判断一个值是否符合正则表达式的规则       |
| PLIKE       | 正则表达式运算符 | 判断一个值是否符合正则表达式的规则       |



#### (4)逻辑运算符

| 运算符     | 作用     | 实例           |
| ---------- | -------- | -------------- |
| NOT 或 ！  | 逻辑非   | SELECT NOT A   |
| AND 或 &&  | 逻辑与   | SELECT A AND B |
| OR 或 \|\| | 逻辑或   | SELECT A OR B  |
| XOR        | 逻辑异或 | SELECT A XOR B |

> * OR可以和AND一起使用，但是在使用时要注意两者的优先级，由于AND的优先级高于OR，因此先 对AND两边的操作数进行操作，再与OR中的操作数结合。

##### 代码演示


```mysql
# 第04章_运算符
#1. 算术运算符： +  -  *  /  div  % mod

SELECT 100, 100 + 0, 100 - 0, 100 + 50, 100 + 50 * 30, 100 + 35.5, 100 - 35.5 
FROM DUAL;

# 在SQL中，+没有连接的作用，就表示加法运算。此时，会将字符串转换为数值（隐式转换）
SELECT 100 + '1'  # 在Java语言中，结果是：1001。 
FROM DUAL;

SELECT 100 + 'a' #此时将'a'看做0处理
FROM DUAL;

SELECT 100 + NULL  # null值参与运算，结果为null
FROM DUAL;

SELECT 100, 100 * 1, 100 * 1.0, 100 / 1.0, 100 / 2,
100 + 2 * 5 / 2,100 / 3, 100 DIV 0  # 分母如果为0，则结果为null
FROM DUAL;

# 取模运算： % mod
SELECT 12 % 3,12 % 5, 12 MOD -5,-12 % 5,-12 % -5
FROM DUAL;

#练习：查询员工id为偶数的员工信息
SELECT employee_id,last_name,salary
FROM employees
WHERE employee_id % 2 = 0;

#2. 比较运算符
#2.1 =  <=>  <> !=  <  <=  >  >= 

# = 的使用
SELECT 1 = 2,1 != 2,1 = '1',1 = 'a',0 = 'a' #字符串存在隐式转换。如果转换数值不成功，则看做0
FROM DUAL;

SELECT 'a' = 'a','ab' = 'ab','a' = 'b' #两边都是字符串的话，则按照ANSI的比较规则进行比较。
FROM DUAL;

SELECT 1 = NULL,NULL = NULL # 只要有null参与判断，结果就为null
FROM DUAL;

SELECT last_name,salary,commission_pct
FROM employees
#where salary = 6000;
WHERE commission_pct = NULL;  #此时执行，不会有任何的结果

# <=> ：安全等于。 记忆技巧：为NULL而生。

SELECT 1 <=> 2,1 <=> '1',1 <=> 'a',0 <=> 'a'
FROM DUAL;

SELECT 1 <=> NULL, NULL <=> NULL
FROM DUAL;

#练习：查询表中commission_pct为null的数据有哪些
SELECT last_name,salary,commission_pct
FROM employees
WHERE commission_pct <=> NULL;

SELECT 3 <> 2,'4' <> NULL, '' != NULL,NULL != NULL
FROM DUAL;

#2.2 
#① IS NULL \ IS NOT NULL \ ISNULL
#练习：查询表中commission_pct为null的数据有哪些
SELECT last_name,salary,commission_pct
FROM employees
WHERE commission_pct IS NULL;
#或
SELECT last_name,salary,commission_pct
FROM employees
WHERE ISNULL(commission_pct);

#练习：查询表中commission_pct不为null的数据有哪些
SELECT last_name,salary,commission_pct
FROM employees
WHERE commission_pct IS NOT NULL;
#或
SELECT last_name,salary,commission_pct
FROM employees
WHERE NOT commission_pct <=> NULL;

#② LEAST() \ GREATEST 

SELECT LEAST('g','b','t','m'),GREATEST('g','b','t','m')
FROM DUAL;

SELECT LEAST(first_name,last_name),LEAST(LENGTH(first_name),LENGTH(last_name))
FROM employees;

#③ BETWEEN 条件下界1 AND 条件上界2  （查询条件1和条件2范围内的数据，包含边界）
#查询工资在6000 到 8000的员工信息
SELECT employee_id,last_name,salary
FROM employees
#where salary between 6000 and 8000;
WHERE salary >= 6000 && salary <= 8000;

#交换6000 和 8000之后，查询不到数据
SELECT employee_id,last_name,salary
FROM employees
WHERE salary BETWEEN 8000 AND 6000;

#查询工资不在6000 到 8000的员工信息
SELECT employee_id,last_name,salary
FROM employees
WHERE salary NOT BETWEEN 6000 AND 8000;
#where salary < 6000 or salary > 8000;

#④ in (set)\ not in (set)

#练习：查询部门为10,20,30部门的员工信息
SELECT last_name,salary,department_id
FROM employees
#where department_id = 10 or department_id = 20 or department_id = 30;
WHERE department_id IN (10,20,30);

#练习：查询工资不是6000,7000,8000的员工信息
SELECT last_name,salary,department_id
FROM employees
WHERE salary NOT IN (6000,7000,8000);

#⑤ LIKE :模糊查询
# % : 代表不确定个数的字符 （0个，1个，或多个）

#练习：查询last_name中包含字符'a'的员工信息
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%';

#练习：查询last_name中以字符'a'开头的员工信息
SELECT last_name
FROM employees
WHERE last_name LIKE 'a%';

#练习：查询last_name中包含字符'a'且包含字符'e'的员工信息
#写法1：
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%' AND last_name LIKE '%e%';
#写法2：
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%e%' OR last_name LIKE '%e%a%';

# _ ：代表一个不确定的字符

#练习：查询第3个字符是'a'的员工信息
SELECT last_name
FROM employees
WHERE last_name LIKE '__a%';

#练习：查询第2个字符是_且第3个字符是'a'的员工信息
#需要使用转义字符: \ 
SELECT last_name
FROM employees
WHERE last_name LIKE '_\_a%';

#或者  (了解)
SELECT last_name
FROM employees
WHERE last_name LIKE '_$_a%' ESCAPE '$';

#⑥ REGEXP \ RLIKE :正则表达式

SELECT 'shkstart' REGEXP '^shk', 'shkstart' REGEXP 't$', 'shkstart' REGEXP 'hk'
FROM DUAL;

SELECT 'atguigu' REGEXP 'gu.gu','atguigu' REGEXP '[ab]'
FROM DUAL;

#3. 逻辑运算符： OR ||  AND && NOT ! XOR

# or  and 
SELECT last_name,salary,department_id
FROM employees
#where department_id = 10 or department_id = 20;
#where department_id = 10 and department_id = 20;
WHERE department_id = 50 AND salary > 6000;

# not 
SELECT last_name,salary,department_id
FROM employees
#where salary not between 6000 and 8000;
#where commission_pct is not null;
WHERE NOT commission_pct <=> NULL;

# XOR :追求的"异"
SELECT last_name,salary,department_id
FROM employees
WHERE department_id = 50 XOR salary > 6000;

#注意：AND的优先级高于OR

#4. 位运算符： & |  ^  ~  >>   <<

SELECT 12 & 5, 12 | 5,12 ^ 5 
FROM DUAL;

SELECT 10 & ~1 FROM DUAL;

#在一定范围内满足：每向左移动1位，相当于乘以2；每向右移动一位，相当于除以2。
SELECT 4 << 1 , 8 >> 1
FROM DUAL;
```



#### (5)位运算符

#### (6)运算符优先级



### 3.排序与分页

#### (1)排序数据

> * 使用 ORDER BY 子句排序 
> * * ASC（ascend）: 升序 
>   * DESC（descend）:降序

* 单列排序

```mysql
SELECT last_name, job_id, department_id, hire_date
FROM employees
ORDER BY hire_date ;
#默认升序

SELECT last_name, job_id, department_id, hire_date
FROM employees
ORDER BY hire_date DESC ;

```

* 多列排序

```mysql
SELECT last_name, department_id, salary
FROM employees
ORDER BY department_id, salary DESC;

```

**注：**

1.可以使用不在SELECT列表中的列排序。 

2.在对多列进行排序的时候，首先排序的第一列必须有相同的列值，才会对第二列进行排序。如果第 一列数据中所有值都是唯一的，将不再对第二列进行排序。



#### (2)分页

> * 页原理：将数据库中的结果集，一段一段显示出来需要的条件。 
> * MySQL中使用 LIMIT 实现分页
> * 格式：**LIMIT **  [位置偏移量,] 行数
> * 第一个“位置偏移量”参数指示MySQL从哪一行开始显示，是一个可选参数，**如果不指定“位置偏移 量”**，将会从表中的**第一条**记录开始（第一条记录的位置偏移量是0，第二条记录的位置偏移量是 1，以此类推）；第二个参数“行数”指示返回的记录条数。

```mysql
--前10条记录：
SELECT * FROM 表名 LIMIT 0,10;
或者
SELECT * FROM 表名 LIMIT 10;
--第11至20条记录：
SELECT * FROM 表名 LIMIT 10,10;
--第21至30条记录：
SELECT * FROM 表名 LIMIT 20,10;

```

* 分页显式公式：（当前页数-1）*每页条数，每页条数
* 注意：LIMIT 子句必须放在整个SELECT语句的最后！



### 4.多表查询及分类

```mysql
#案例：查询员工的姓名及其部门名称
SELECT last_name, department_name
FROM employees, departments
WHERE employees.department_id = departments.department_id;

SELECT e.job_id,d.location_id,l.city
FROM employees e,departments d,locations l
WHERE e.`department_id` = d.`department_id`
AND d.`location_id` = l.`location_id`;
```

#### (1)等值连接

```mysql
#employees表和departments表有相同字段 department_id，进行的连接，叫等值连接

SELECT employees.employee_id, employees.last_name,
employees.department_id, departments.department_id,
departments.location_id
FROM employees, departments
WHERE employees.department_id = departments.department_id;
```

* 当有多个连接条件时要用AND操作符

```mysql
SELECT e.job_id,d.location_id,l.city
FROM employees e,departments d,locations l
WHERE e.`department_id` = d.`department_id`
AND d.`location_id` = l.`location_id`;
```

* 多个表中有相同列时，必须在列名之前加上表名前缀。

```mysql
SELECT employees.last_name, departments.department_name,employees.department_id
FROM employees, departments
WHERE employees.department_id = departments.department_id;

#注：如果我们使用了表的别名，在查询字段中、过滤条件中就只能使用别名进行代替，不能使用原有的表名，否则就会报错。
```

* 连接 n个表,至少需要n-1个连接条件。比如，连接三个表，至少需要两个连接条件。

#### (2)非等值连接

> 如下图，根据job_grades表中的lowest_sal和highest_sal通过employees中的员工salary给员工工资划分等级；代码如下：

![image-20211217173438890](D:\Typora笔记\javapicture\image-20211217173438890.png)

```mysql
SELECT last_name,salary,grade_level
FROM employees e,job_grades j
WHERE e.`salary` >= j.`lowest_sal`
AND e.`salary` <=j.`highest_sal`;
```

#### (3)自连接

> 本质上是同一张表，只是用取别名的方式虚拟成两张表以代表不同的意义。然后两 个表再进行内连接，外连接等查询。

![image-20211217174629233](D:\Typora笔记\javapicture\自连接.png)

```mysql
#查询员工姓名及其管理者的ID和姓名
SELECT emp.employee_id,emp.last_name,mar.employee_id,mar.last_name
FROM employees emp,employees mar
WHERE emp.`manager_id` = mar.`employee_id`
```

#### (4)非自连接

> 自连接以外的其他连接。。。

#### (5)内连接

> 合并具有同一列的两个以上的表的行, 结果集中不包含一个表与另一个表不匹配的行.

#### (6)外连接

> 合并具有同一列的两个以上的表的行, 结果集中除了包含一个表与另一个表匹配的行之外，还查询到了左表 或 右表中不匹配的行。

* SQL92语法实现内连接：以上都是
* SQL92语法实现外连接  用 ‘+’ 号，但是MySQL不支持
* MySQL实现外连接使用**SQL99**语法，以下是**SQL99**语法(SQL99语法中使用 **JOIN ...ON** 的方式实现多表的查询)

##### 左外连接

> 两个表在连接过程中除了返回满足连接条件的行以外还返回左表中不满足条件的行，这种连接称为左外连接。

```mysql
# 查询所有员工的last_name,department_name信息(使用左外连接
SELECT last_name,department_name
FROM employees e LEFT OUTER JOIN departments d
ON e.`department_id` = d.`department_id`
```

**注**：OUTER和INNER可省略

##### 右外连接

> 右外连接：两个表在连接过程中除了返回满足连接条件的行以外还返回右表中不满足条件的行，这种连接称为右外连接。

```mysql
#右外连接
SELECT last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
```

##### 满外连接

> **FULL OUT JOIN** 虽然SQL99中是这么写，但是MySQL不支持。用7种join方法中的一种

#### (7)SQL99语法实现多表查询

* SQL99实现内连接

```mysql
#sql99实现内连接
SELECT last_name,department_name
FROM employees e INNER JOIN departments d
ON e.`department_id` = d.`department_id`

SELECT last_name,department_name,city
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`
JOIN locations l
ON d.`location_id` = l.location_id;
```

* UNION的使用

> **合并查询结果** 利用**UNION**关键字，可以给出多条SELECT语句，并将它们的结果组合成单个结果集。合并 时，两个表对应的列数和数据类型必须相同，并且相互对应。各个SELECT语句之间使用UNION或UNION ALL关键字分隔。

**格式**：

```mysql
SELECT column,... FROM table1
UNION [ALL]
SELECT column,... FROM table2
```

**UNION与UNION ALL区别：**

> **UNION** 操作符返回两个查询的结果集的并集，去除重复记录。
>
> **UNION ALL**操作符返回两个查询的结果集的并集。对于两个结果集的重复部分，不去重。

**注意**：执行UNION ALL语句时所需要的资源比UNION语句少。如果明确知道合并数据后的结果数据 不存在重复数据，或者不需要去除重复的数据，则**尽量使用UNION ALL**语句，以提高数据查询的效 率。

#### (8)7种JOIN的实现

![image-20211217185254702](D:\Typora笔记\javapicture\7种join.png)

```mysql
# 中图：内连接
SELECT employee_id,department_name
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`;

# 左上图：左外连接
SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`;

# 右上图：右外连接
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;

# 左中图：
SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL;

# 右中图：
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;


# 左下图：满外连接
# 方式1：左上图 UNION ALL 右中图

SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
UNION ALL
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;


# 方式2：左中图 UNION ALL 右上图

SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;

# 右下图：左中图  UNION ALL 右中图
SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;
```

#### (8) SQL99语法新特性

* 自然连接

> SQL99 在 SQL92 的基础上提供了一些特殊语法，比如 NATURAL JOIN 用来表示自然连接。我们可以把 自然连接理解为 SQL92 中的等值连接。它会帮你自动查询两张连接表中 所有相同的字段 ，然后进行 等值 连接 。

在SQL92标准中：

```mysql
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`
AND e.`manager_id` = d.`manager_id`;
```

在 SQL99 中你可以写成：

```mysql
SELECT employee_id,last_name,department_name
FROM employees e NATURAL JOIN departments d;
```

* USING连接

> 当我们进行连接的时候，SQL99还支持使用 USING 指定数据表里的 同名字段 进行等值连接。但是只能配 合JOIN一起使用。

```mysql
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
USING (department_id);

SELECT employee_id,last_name,department_name
FROM employees e ,departments d
WHERE e.department_id = d.department_id;
```



### 5.单行函数

#### (1)数值函数

##### 基本函数

| 函数                   | 用法                                                         |
| ---------------------- | ------------------------------------------------------------ |
| ABS(x)                 | 返回x的绝对值                                                |
| SIGN(x)                | 返回x的符号。正数返回1，负数返回-1，0返回0                   |
| PI()                   | 返回圆周率的值                                               |
| CEIL(x), CEILING(x)    | 返回大于或等于某个值的最小整数                               |
| FLOOR(x)               | 返回小于或等于某个值的最大整数                               |
| LEAST(e1,e2,e3,...)    | 返回列表中的最小值                                           |
| GREATEST(e1,e2,e3,...) | 返回列表中的最大值                                           |
| MOD(x,y)               | 返回x除以y后的余数                                           |
| RAND()                 | 返回0-1的随机数                                              |
| RAND(x)                | 返回0-1的随机数，其中x的值用作种子值，相同的x值会产生相同的随机数 |
| ROUND(x)               | 返回一个对x的值进行四舍五入后，最接近于x的整数               |
| ROUND(x,y)             | 返回一个对x的值进行四舍五入后最接近x的值，并保留到小数点后面y位 |
| TRUNCATE(x,y)          | 返回数字x截断为y位小数的结果                                 |
| SQRT(x)                | 返回x的平方根。当x的值为负数时，返回NULL                     |

```mysql
SELECT
ABS(-123),ABS(32),SIGN(-23),SIGN(43),PI(),CEIL(32.32),CEILING(-43.23),FLOOR(32.32),
FLOOR(-43.23),MOD(12,5)
FROM DUAL;

SELECT RAND(),RAND(),RAND(10),RAND(10),RAND(-1),RAND(-1)
FROM DUAL;

SELECT
ROUND(12.33),ROUND(12.343,2),ROUND(12.324,-1),TRUNCATE(12.66,1),TRUNCATE(12.66,-1)
FROM DUAL;
```

##### 角度与弧度互换函数

| **函数**   | **用法**                              |
| ---------- | ------------------------------------- |
| RADIANS(x) | 将角度转化为弧度，其中，参数x为角度值 |
| DEGREES(x) | 将弧度转化为角度，其中，参数x为弧度值 |

```mysql
SELECT RADIANS(30),RADIANS(60),RADIANS(90),DEGREES(2*PI()),DEGREES(RADIANS(90))
FROM DUAL;

```

##### 三角函数

| **函数**   | **用法**                                                     |
| ---------- | ------------------------------------------------------------ |
| SIN(x)     | 返回x的正弦值，其中，参数x为弧度值                           |
| ASIN(x)    | 返回x的反正弦值，即获取正弦为x的值。如果x的值不在-1到1之间，则返回NULL |
| COS(x)     | 返回x的余弦值，其中，参数x为弧度值                           |
| ACOS(x)    | 返回x的反余弦值，即获取余弦为x的值。如果x的值不在-1到1之间，则返回NULL |
| TAN(x)     | 返回x的正切值，其中，参数x为弧度值                           |
| ATAN(x)    | 返回x的反正切值，即返回正切值为x的值                         |
| ATAN2(m,n) | 返回两个参数的反正切值                                       |
| COT(x)     | 返回x的余切值，其中，X为弧度值                               |

> ATAN2(M,N)函数返回两个参数的反正切值。 与ATAN(X)函数相比，ATAN2(M,N)需要两个参数，例如有两个 点point(x1,y1)和point(x2,y2)，使用ATAN(X)函数计算反正切值为ATAN((y2-y1)/(x2-x1))，使用ATAN2(M,N)计 算反正切值则为ATAN2(y2-y1,x2-x1)。由使用方式可以看出，当x2-x1等于0时，ATAN(X)函数会报错，而 ATAN2(M,N)函数则仍然可以计算。

```mysql
SELECT
SIN(RADIANS(30)),DEGREES(ASIN(1)),TAN(RADIANS(45)),DEGREES(ATAN(1)),DEGREES(ATAN2(1,1)
)
FROM DUAL;
```

##### 指数与对数函数

| **函数**             | **用法**                                             |
| -------------------- | ---------------------------------------------------- |
| POW(x,y)，POWER(X,Y) | 返回x的y次方                                         |
| EXP(X)               | 返回e的X次方，其中e是一个常数，2.718281828459045     |
| LN(X)，LOG(X)        | 返回以e为底的X的对数，当X <= 0 时，返回的结果为NULL  |
| LOG10(X)             | 返回以10为底的X的对数，当X <= 0 时，返回的结果为NULL |
| LOG2(X)              | 返回以2为底的X的对数，当X <= 0  时，返回NULL         |

```mysql
mysql> SELECT POW(2,5),POWER(2,4),EXP(2),LN(10),LOG10(10),LOG2(4)
-> FROM DUAL;
+----------+------------+------------------+-------------------+-----------+---------+
| POW(2,5) | POWER(2,4) | EXP(2) | LN(10) | LOG10(10) | LOG2(4) |
+----------+------------+------------------+-------------------+-----------+---------+
| 32 | 16 | 7.38905609893065 | 2.302585092994046 | 1 | 2 |
+----------+------------+------------------+-------------------+-----------+---------+
1 row in set (0.00 sec)
```

##### 进制间的转换

| **函数**      | **用法**                 |
| ------------- | ------------------------ |
| BIN(x)        | 返回x的二进制编码        |
| HEX(x)        | 返回x的十六进制编码      |
| OCT(x)        | 返回x的八进制编码        |
| CONV(x,f1,f2) | 返回f1进制数变成f2进制数 |

```mysql
mysql> SELECT BIN(10),HEX(10),OCT(10),CONV(10,2,8)
-> FROM DUAL;
+---------+---------+---------+--------------+
| BIN(10) | HEX(10) | OCT(10) | CONV(10,2,8) |
+---------+---------+---------+--------------+
| 1010 | A | 12 | 2 |
+---------+---------+---------+--------------+
1 row in set (0.00 sec)
```



#### (2)字符串函数

> 注意：MySQL中，字符串的位置是从**1**开始的。

| **函数**                           | **用法**                                                     |
| ---------------------------------- | ------------------------------------------------------------ |
| ASCII(S)                           | 返回字符串S中的第一个字符的ASCII码值                         |
| CHAR_LENGTH(s)                     | 返回字符串s的字符数。作用与CHARACTER_LENGTH(s)相同           |
| LENGTH(s)                          | 返回字符串s的字节数，和字符集有关                            |
| CONCAT(s1,s2,. ,sn)                | 连接s1,s2,.... ,sn为一个字符串                               |
| CONCAT_WS(x, s1,s2,.... ,sn)       | 同CONCAT(s1,s2,...)函数，但是每个字符串之间要加上x           |
| INSERT(str, idx, len,  replacestr) | 将字符串str从第idx位置开始，len个字符长的子串替换为字符串replacestr |
| REPLACE(str, a, b)                 | 用字符串b替换字符串str中所有出现的字符串a                    |
| UPPER(s) 或 UCASE(s)               | 将字符串s的所有字母转成大写字母                              |
| LOWER(s) 或LCASE(s)                | 将字符串s的所有字母转成小写字母                              |
| LEFT(str,n)                        | 返回字符串str最左边的n个字符                                 |
| RIGHT(str,n)                       | 返回字符串str最右边的n个字符                                 |
| LPAD(str, len, pad)                | 用字符串pad对str最左边进行填充，直到str的长度为len个字符     |
| RPAD(str ,len, pad)                | 用字符串pad对str最右边进行填充，直到str的长度为len个字符     |
| LTRIM(s)                           | 去掉字符串s左侧的空格                                        |
| RTRIM(s)                           | 去掉字符串s右侧的空格                                        |
| TRIM(s)                            | 去掉字符串s开始与结尾的空格                                  |
| TRIM(s1 FROM s)                    | 去掉字符串s开始与结尾的s1                                    |
| TRIM(LEADING s1 FROM s)            | 去掉字符串s开始处的s1                                        |
| TRIM(TRAILING s1 FROM s)           | 去掉字符串s结尾处的s1                                        |
| REPEAT(str, n)                     | 返回str重复n次的结果                                         |
| SPACE(n)                           | 返回n个空格                                                  |
| STRCMP(s1,s2)                      | 比较字符串s1,s2的ASCII码值的大小                             |
| SUBSTR(s,index,len)                | 返回从字符串s的index位置其len个字符，作用与SUBSTRING(s,n,len)、  MID(s,n,len)相同 |
| LOCATE(substr,str)                 | 返回字符串substr在字符串str中首次出现的位置，作用于POSITION(substr IN str)、INSTR(str,substr)相同。未找到，返回0 |
| ELT(m,s1,s2,…,sn)                  | 返回指定位置的字符串，如果m=1，则返回s1，如果m=2，则返回s2，如果m=n，则返回sn |
| FIELD(s,s1,s2,…,sn)                | 返回字符串s在字符串列表中第一次出现的位置                    |
| FIND_IN_SET(s1,s2)    | 返回字符串s1在字符串s2中出现的位置。其中，字符串s2是一个以逗号分隔的字符串 |
| REVERSE(s)            | 返回s反转后的字符串                                          |
| NULLIF(value1,value2) | 比较两个字符串，如果value1与value2相等，则返回NULL，否则返回  value1 |

```mysql
#2. 字符串函数

SELECT ASCII('Abcdfsf'),CHAR_LENGTH('hello'),CHAR_LENGTH('我们'),
LENGTH('hello'),LENGTH('我们')
FROM DUAL;

# xxx worked for yyy
SELECT CONCAT(emp.last_name,' worked for ',mgr.last_name) "details"
FROM employees emp JOIN employees mgr
WHERE emp.`manager_id` = mgr.employee_id;

SELECT CONCAT_WS('-','hello','world','hello','beijing')
FROM DUAL;
#字符串的索引是从1开始的！
SELECT INSERT('helloworld',2,3,'aaaaa'),REPLACE('hello','lol','mmm')
FROM DUAL;

SELECT UPPER('HelLo'),LOWER('HelLo')
FROM DUAL;

SELECT last_name,salary
FROM employees
WHERE LOWER(last_name) = 'King';

SELECT LEFT('hello',2),RIGHT('hello',3),RIGHT('hello',13)
FROM DUAL;

# LPAD:实现右对齐效果
# RPAD:实现左对齐效果
SELECT employee_id,last_name,LPAD(salary,10,' ')
FROM employees;

SELECT CONCAT('---',LTRIM('    h  el  lo   '),'***'),
TRIM('oo' FROM 'ooheollo')
FROM DUAL;

SELECT REPEAT('hello',4),LENGTH(SPACE(5)),STRCMP('abc','abe')
FROM DUAL;


SELECT SUBSTR('hello',2,2),LOCATE('lll','hello')
FROM DUAL;

SELECT ELT(2,'a','b','c','d'),FIELD('mm','gg','jj','mm','dd','mm'),
FIND_IN_SET('mm','gg,mm,jj,dd,mm,gg')
FROM DUAL;

SELECT employee_id,NULLIF(LENGTH(first_name),LENGTH(last_name)) "compare"
FROM employees;
```



#### (3)日期和时间函数

##### *获取日期、时间

| **函数**                                                     | **用法**                       |
| ------------------------------------------------------------ | ------------------------------ |
| **CURDATE()** ，CURRENT_DATE()                               | 返回当前日期，只包含年、月、日 |
| **CURTIME()** ， CURRENT_TIME()                              | 返回当前时间，只包含时、分、秒 |
| **NOW()** / SYSDATE() / CURRENT_TIMESTAMP() / LOCALTIME() / LOCALTIMESTAMP() | 返回当前系统日期和时间         |
| UTC_DATE()                                                   | 返回UTC（世界标准时间） 日期   |
| UTC_TIME()                                                   | 返回UTC（世界标准时间） 时间   |

```mysql
#3.1  获取日期、时间
SELECT CURDATE(),CURRENT_DATE(),CURTIME(),NOW(),SYSDATE(),
UTC_DATE(),UTC_TIME()
FROM DUAL;

SELECT CURDATE(),CURDATE() + 0,CURTIME() + 0,NOW() + 0
FROM DUAL;
```

##### *日期与时间戳的转换

| **函数**                 | **用法**                                                     |
| ------------------------ | ------------------------------------------------------------ |
| UNIX_TIMESTAMP()         | 以UNIX时间戳的形式返回当前时间。SELECT UNIX_TIMESTAMP() -  >1634348884 |
| UNIX_TIMESTAMP(date)     | 将时间date以UNIX时间戳的形式返回。                           |
| FROM_UNIXTIME(timestamp) | 将UNIX时间戳的时间转换为普通格式的时间                       |

```mysql
#3.2 日期与时间戳的转换
SELECT UNIX_TIMESTAMP(),UNIX_TIMESTAMP('2021-10-01 12:12:32'),
FROM_UNIXTIME(1635173853),FROM_UNIXTIME(1633061552)
FROM DUAL;
```

##### *获取月份、星期、星期数、天数等函数

| **函数**                                 | **用法**                                          |
| ---------------------------------------- | ------------------------------------------------- |
| YEAR(date) / MONTH(date) / DAY(date)     | 返回具体的日期值                                  |
| HOUR(time) / MINUTE(time) / SECOND(time) | 返回具体的时间值                                  |
| MONTHNAME(date)                          | 返回月份：January，...                            |
| DAYNAME(date)                            | 返回星期几：MONDAY，TUESDAY SUNDAY                |
| WEEKDAY(date)                            | 返回周几，注意，周1是0，周2是1，。。。周日是6     |
| QUARTER(date)                            | 返回日期对应的季度，范围为1～4                    |
| WEEK(date) ， WEEKOFYEAR(date)           | 返回一年中的第几周                                |
| DAYOFYEAR(date)                          | 返回日期是一年中的第几天                          |
| DAYOFMONTH(date)                         | 返回日期位于所在月份的第几天                      |
| DAYOFWEEK(date)                          | 返回周几，注意：周日是1，周一是2，。。。周六是  7 |

```mysql
#3.3 获取月份、星期、星期数、天数等函数
SELECT YEAR(CURDATE()),MONTH(CURDATE()),DAY(CURDATE()),
HOUR(CURTIME()),MINUTE(NOW()),SECOND(SYSDATE())
FROM DUAL;


SELECT MONTHNAME('2021-10-26'),DAYNAME('2021-10-26'),WEEKDAY('2021-10-26'),
QUARTER(CURDATE()),WEEK(CURDATE()),DAYOFYEAR(NOW()),
DAYOFMONTH(NOW()),DAYOFWEEK(NOW())
FROM DUAL;
```

##### *日期的操作函数

| **函数**                | **用法**                                   |
| ----------------------- | ------------------------------------------ |
| EXTRACT(type FROM date) | 返回指定日期中特定的部分，type指定返回的值 |

```mysql
#3.4 日期的操作函数

SELECT EXTRACT(SECOND FROM NOW()),EXTRACT(DAY FROM NOW()),
EXTRACT(HOUR_MINUTE FROM NOW()),EXTRACT(QUARTER FROM '2021-05-12')
FROM DUAL;
```


##### *时间和秒钟转换的函数

| **函数**             | **用法**                                                     |
| -------------------- | ------------------------------------------------------------ |
| TIME_TO_SEC(time)    | 将 time 转化为秒并返回结果值。转化的公式为： 小时*3600+分钟  *60+秒 |
| SEC_TO_TIME(seconds) | 将  seconds 描述转化为包含小时、分钟和秒的时间               |

```mysql
#3.5 时间和秒钟转换的函数
SELECT TIME_TO_SEC(CURTIME()),
SEC_TO_TIME(83355)
FROM DUAL;
```

##### *计算日期和时间的函数

**第一组**：

| **函数**                                                     | **用法**                                       |
| ------------------------------------------------------------ | ---------------------------------------------- |
| DATE_ADD(datetime, INTERVAL expr type)， ADDDATE(date,INTERVAL  expr type) | 返回与给定日期时间相差INTERVAL时间段的日期时间 |
| DATE_SUB(date,INTERVAL expr type)， SUBDATE(date,INTERVAL expr type) | 返回与date相差INTERVAL时间间隔的日期           |

![image-20211218150303376](D:\Typora笔记\javapicture\第一组.png)

**第二组：**

| **函数**                     | **用法**                                                     |
| ---------------------------- | ------------------------------------------------------------ |
| ADDTIME(time1,time2)         | 返回time1加上time2的时间。当time2为一个数字时，代表的是  秒 ，可以为负数 |
| SUBTIME(time1,time2)         | 返回time1减去time2后的时间。当time2为一个数字时，代表的是 秒 ，可以为负数 |
| DATEDIFF(date1,date2)        | 返回date1 - date2的日期间隔天数                              |
| TIMEDIFF(time1, time2)       | 返回time1 - time2的时间间隔                                  |
| FROM_DAYS(N)                 | 返回从0000年1月1日起，N天以后的日期                          |
| TO_DAYS(date)                | 返回日期date距离0000年1月1日的天数                           |
| LAST_DAY(date)               | 返回date所在月份的最后一天的日期                             |
| MAKEDATE(year,n)             | 针对给定年份与所在年份中的天数返回一个日期                   |
| MAKETIME(hour,minute,second) | 将给定的小时、分钟和秒组合成时间并返回                       |
| PERIOD_ADD(time,n)           | 返回time加上n后的时间                                        |


```mysql
#3.6 计算日期和时间的函数

SELECT NOW(),DATE_ADD(NOW(),INTERVAL 1 YEAR),
DATE_ADD(NOW(),INTERVAL -1 YEAR),
DATE_SUB(NOW(),INTERVAL 1 YEAR)
FROM DUAL;


SELECT DATE_ADD(NOW(), INTERVAL 1 DAY) AS col1,DATE_ADD('2021-10-21 23:32:12',INTERVAL 1 SECOND) AS col2,
ADDDATE('2021-10-21 23:32:12',INTERVAL 1 SECOND) AS col3,
DATE_ADD('2021-10-21 23:32:12',INTERVAL '1_1' MINUTE_SECOND) AS col4,
DATE_ADD(NOW(), INTERVAL -1 YEAR) AS col5, #可以是负数
DATE_ADD(NOW(), INTERVAL '1_1' YEAR_MONTH) AS col6 #需要单引号
FROM DUAL;


SELECT ADDTIME(NOW(),20),SUBTIME(NOW(),30),SUBTIME(NOW(),'1:1:3'),DATEDIFF(NOW(),'2021-10-01'),
TIMEDIFF(NOW(),'2021-10-25 22:10:10'),FROM_DAYS(366),TO_DAYS('0000-12-25'),
LAST_DAY(NOW()),MAKEDATE(YEAR(NOW()),32),MAKETIME(10,21,23),PERIOD_ADD(20200101010101,10)
FROM DUAL;
```

##### *日期的格式化与解析

| **函数**                          | **用法**                                   |
| --------------------------------- | ------------------------------------------ |
| DATE_FORMAT(date,fmt)             | 按照字符串fmt格式化日期date值              |
| TIME_FORMAT(time,fmt)             | 按照字符串fmt格式化时间time值              |
| GET_FORMAT(date_type,format_type) | 返回日期字符串的显示格式                   |
| STR_TO_DATE(str, fmt)             | 按照字符串fmt对str进行解析，解析为一个日期 |

**上述 非GET_FORMAT 函数中fmt参数常用的格式符：**

| **格式符** | **说明**                                                     | 格式     | **说明**                                                     |
| ---------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| %Y         | 4位数字表示年份                                              | %y       | 表示两位数字表示年份                                         |
| %M         | 月名表示月份（January,... ）                                 | %m       | 两位数字表示月份  （01,02,03。。。）                         |
| %b         | 缩写的月名（Jan.，Feb.，.. ）                                | %c       | 数字表示月份（1,2,3,...）                                    |
| %D         | 英文后缀表示月中的天数  （1st,2nd,3rd,...）                  | %d       | 两位数字表示月中的天数(01,02...)                             |
| %e         | 数字形式表示月中的天数  （1,2,3,4,5.....）                   |          |                                                              |
| %H         | 两位数字表示小数，24小时制  （01,02..）                      | %h  和%I | 两位数字表示小时，12小时制  （01,02..）                      |
| %k         | 数字形式的小时，24小时制(1,2,3)                              | %l       | 数字形式表示小时，12小时制  （1,2,3,4....）                  |
| %i         | 两位数字表示分钟（00,01,02）                                 | %S  和%s | 两位数字表示秒(00,01,02...)                                  |
| %W         | 一周中的星期名称（Sunday...）                                | %a       | 一周中的星期缩写（Sun.，  Mon.,Tues.，..）                   |
| %w         | 以数字表示周中的天数  (0=Sunday,1=Monday )                   |          |                                                              |
| %j         | 以3位数字表示年中的天数(001,002...)                          | %U       | 以数字表示年中的第几周，  （1,2,3。。）其中Sunday为周中第一天 |
| %u         | 以数字表示年中的第几周，  （1,2,3。。）其中Monday为周中第一天 |          |                                                              |
| %T         | 24小时制                                                     | %r       | 12小时制                                                     |
| %p         | AM或PM                                                       | %%       | 表示%                                                        |

**GET_FORMAT函数中date_type和format_type参数取值如下：**

![image-20211218150736479](D:\Typora笔记\javapicture\image-20211218150736479.png)



```mysql
#3.7 日期的格式化与解析
# 格式化：日期 ---> 字符串
# 解析：  字符串 ----> 日期

#此时我们谈的是日期的显式格式化和解析

#之前，我们接触过隐式的格式化或解析
SELECT *
FROM employees
WHERE hire_date = '1993-01-13';

#格式化：
SELECT DATE_FORMAT(CURDATE(),'%Y-%M-%D'),
DATE_FORMAT(NOW(),'%Y-%m-%d'),TIME_FORMAT(CURTIME(),'%h:%i:%S'),
DATE_FORMAT(NOW(),'%Y-%M-%D %h:%i:%S %W %w %T %r')
FROM DUAL;

#解析：格式化的逆过程
SELECT STR_TO_DATE('2021-October-25th 11:37:30 Monday 1','%Y-%M-%D %h:%i:%S %W %w')
FROM DUAL;

SELECT GET_FORMAT(DATE,'USA')
FROM DUAL;

SELECT DATE_FORMAT(CURDATE(),GET_FORMAT(DATE,'USA'))
FROM DUAL;
```



#### (4)流程控制函数

| **函数**                                                     | **用法**                                         |
| ------------------------------------------------------------ | ------------------------------------------------ |
| IF(value,value1,value2)                                      | 如果value的值为TRUE，返回value1， 否则返回value2 |
| IFNULL(value1, value2)                                       | 如果value1不为NULL，返回value1，否则返回value2   |
| CASE WHEN 条件1 THEN 结果1 WHEN 条件2 THEN 结果2  .... [ELSE resultn] END | 相当于Java的if...else if...else...               |
| CASE expr WHEN 常量值1 THEN 值1 WHEN 常量值1 THEN  值1..... [ELSE 值n] END | 相当于Java的switch...case...                     |

```mysql
#4.流程控制函数
#4.1 IF(VALUE,VALUE1,VALUE2)

SELECT last_name,salary,IF(salary >= 6000,'高工资','低工资') "details"
FROM employees;

SELECT last_name,commission_pct,IF(commission_pct IS NOT NULL,commission_pct,0) "details",
salary * 12 * (1 + IF(commission_pct IS NOT NULL,commission_pct,0)) "annual_sal"
FROM employees;

#4.2 IFNULL(VALUE1,VALUE2):看做是IF(VALUE,VALUE1,VALUE2)的特殊情况
SELECT last_name,commission_pct,IFNULL(commission_pct,0) "details"
FROM employees;

#4.3 CASE WHEN ... THEN ...WHEN ... THEN ... ELSE ... END
# 类似于java的if ... else if ... else if ... else
SELECT last_name,salary,CASE WHEN salary >= 15000 THEN '白骨精' 
			     WHEN salary >= 10000 THEN '潜力股'
			     WHEN salary >= 8000 THEN '小屌丝'
			     ELSE '草根' END "details",department_id
FROM employees;

SELECT last_name,salary,CASE WHEN salary >= 15000 THEN '白骨精' 
			     WHEN salary >= 10000 THEN '潜力股'
			     WHEN salary >= 8000 THEN '小屌丝'
			     END "details"
FROM employees;

#4.4 CASE ... WHEN ... THEN ... WHEN ... THEN ... ELSE ... END
# 类似于java的swich ... case...
/*

练习1
查询部门号为 10,20, 30 的员工信息, 
若部门号为 10, 则打印其工资的 1.1 倍, 
20 号部门, 则打印其工资的 1.2 倍, 
30 号部门,打印其工资的 1.3 倍数,
其他部门,打印其工资的 1.4 倍数

*/
SELECT employee_id,last_name,department_id,salary,CASE department_id WHEN 10 THEN salary * 1.1
								     WHEN 20 THEN salary * 1.2
								     WHEN 30 THEN salary * 1.3
								     ELSE salary * 1.4 END "details"
FROM employees;

/*

练习2
查询部门号为 10,20, 30 的员工信息, 
若部门号为 10, 则打印其工资的 1.1 倍, 
20 号部门, 则打印其工资的 1.2 倍, 
30 号部门打印其工资的 1.3 倍数

*/
SELECT employee_id,last_name,department_id,salary,CASE department_id WHEN 10 THEN salary * 1.1
								     WHEN 20 THEN salary * 1.2
								     WHEN 30 THEN salary * 1.3
								     END "details"
FROM employees
WHERE department_id IN (10,20,30);
```







#### (5)加密与解密函数

> 加密与解密函数主要用于对数据库中的数据进行加密和解密处理，以防止数据被他人窃取。这些函数在 保证数据库安全时非常有用。

| **函数**                    | **用法**                                                     |
| --------------------------- | ------------------------------------------------------------ |
| PASSWORD(str)               | 返回字符串str的加密版本，41位长的字符串。加密结果 不可逆 ，常用于用户的密码加密 |
| MD5(str)                    | 返回字符串str的md5加密后的值，也是一种加密方式。若参数为  NULL，则会返回NULL |
| SHA(str)                    | 从原明文密码str计算并返回加密后的密码字符串，当参数为  NULL时，返回NULL。 SHA加密算法比MD5更加安全  。 |
| ENCODE(value,password_seed) | 返回使用password_seed作为加密密码加密value                   |
| DECODE(value,password_seed) | 返回使用password_seed作为加密密码解密value                   |

```mysql
#5. 加密与解密的函数
# PASSWORD()在mysql8.0中弃用。
SELECT MD5('mysql'),SHA('mysql'),MD5(MD5('mysql'))
FROM DUAL;

#ENCODE()\DECODE() 在mysql8.0中弃用。
/*
SELECT ENCODE('atguigu','mysql'),DECODE(ENCODE('atguigu','mysql'),'mysql')
FROM DUAL;
*/
```



#### (6)MySQL信息函数

> MySQL中内置了一些可以查询MySQL信息的函数，这些函数主要用于帮助数据库开发或运维人员更好地 对数据库进行维护工作。

| **函数**                                               | **用法**                                                   |
| ------------------------------------------------------ | ---------------------------------------------------------- |
| VERSION()                                              | 返回当前MySQL的版本号                                      |
| CONNECTION_ID()                                        | 返回当前MySQL服务器的连接数                                |
| DATABASE()，SCHEMA()                                   | 返回MySQL命令行当前所在的数据库                            |
| USER()，CURRENT_USER()、SYSTEM_USER()， SESSION_USER() | 返回当前连接MySQL的用户名，返回结果格式为  “主机名@用户名” |
| CHARSET(value)                                         | 返回字符串value自变量的字符集                              |
| COLLATION(value)                                       | 返回字符串value的比较规则                                  |

```mysql
#6. MySQL信息函数

SELECT VERSION(),CONNECTION_ID(),DATABASE(),SCHEMA(),
USER(),CURRENT_USER(),CHARSET('尚硅谷'),COLLATION('尚硅谷')
FROM DUAL;
```



#### (7)其他函数

| **函数**                        | **用法**                                                     |
| ------------------------------- | ------------------------------------------------------------ |
| FORMAT(value,n)                 | 返回对数字value进行格式化后的结果数据。n表示 四舍五入  后保留到小数点后n位 |
| CONV(value,from,to)             | 将value的值进行不同进制之间的转换                            |
| INET_ATON(ipvalue)              | 将以点分隔的IP地址转化为一个数字                             |
| INET_NTOA(value)                | 将数字形式的IP地址转化为以点分隔的IP地址                     |
| BENCHMARK(n,expr)               | 将表达式expr重复执行n次。用于测试MySQL处理expr表达式所耗费的时间 |
| CONVERT(value USING  char_code) | 将value所使用的字符编码修改为char_code                       |

```mysql
#7. 其他函数
#如果n的值小于或者等于0，则只保留整数部分
SELECT FORMAT(123.125,2),FORMAT(123.125,0),FORMAT(123.125,-2)
FROM DUAL;

SELECT CONV(16, 10, 2), CONV(8888,10,16), CONV(NULL, 10, 2)
FROM DUAL;
#以“192.168.1.100”为例，计算方式为192乘以256的3次方，加上168乘以256的2次方，加上1乘以256，再加上100。
SELECT INET_ATON('192.168.1.100'),INET_NTOA(3232235876)
FROM DUAL;

#BENCHMARK()用于测试表达式的执行效率
SELECT BENCHMARK(100000,MD5('mysql'))
FROM DUAL;
# CONVERT():可以实现字符集的转换
SELECT CHARSET('atguigu'),CHARSET(CONVERT('atguigu' USING 'gbk'))
FROM DUAL;
```





### 6.聚合函数

> 聚合函数作用于一组数据，并对一组数据返回一个值。

#### (1)常用集合函数

##### AVG和SUM函数

```mysql
SELECT AVG(salary), MAX(salary),MIN(salary), SUM(salary)
FROM employees
WHERE job_id LIKE '%REP%';
```

#####  MIN和MAX函数

```mysql
SELECT MIN(hire_date), MAX(hire_date)
FROM employees;
```

##### COUNT函数

* **COUNT(*)**返回表中记录总数，适用于任意数据类型。

```mysql
SELECT COUNT(*)
FROM employees
WHERE department_id = 50;
```

* COUNT(expr) 返回expr不为空的记录总数。

```mysql
SELECT COUNT(commission_pct)
FROM employees
WHERE department_id = 50;
```

* 问题：用count(*)，count(1)，count(列名)谁好呢?

> 对于MyISAM引擎的表是没有区别的。这种引擎内部有一计数器在维护着行数。 Innodb引擎的表用count(*),count(1)直接读行数，复杂度是O(n)，因为innodb真的要去数一遍。但好 于具体的count(列名)。

* 问题：能不能使用count(列名)替换count(*)?

> 不要使用 count(列名)来替代 count(*) ， count(*) 是 SQL92 定义的标准统计行数的语法，跟数 据库无关，跟 NULL 和非 NULL 无关。 说明：count(*)会统计值为 NULL 的行，而 count(列名)不会统计此列为 NULL 值的行。

#### (2)GROUP BY

```mysql
#需求：查询各个部门的平均工资，最高工资
SELECT department_id,AVG(salary),SUM(salary)
FROM employees
GROUP BY department_id

#需求：查询各个job_id的平均工资
SELECT job_id,AVG(salary)
FROM employees
GROUP BY job_id;

#需求：查询各个department_id,job_id的平均工资
#方式1：
SELECT department_id,job_id,AVG(salary)
FROM employees
GROUP BY  department_id,job_id;
#方式2：
SELECT job_id,department_id,AVG(salary)
FROM employees
GROUP BY job_id,department_id;


#错误的！
SELECT department_id,job_id,AVG(salary)
FROM employees
GROUP BY department_id;
```



* SELECT中出现的非组函数的字段必须声明在GROUP BY 中。反之，GROUP BY中声明的字段可以不出现在SELECT中。
* GROUP BY 声明在FROM后面、WHERE后面，ORDER BY 前面、LIMIT前面.
* MySQL中GROUP BY中使用WITH ROLLUP.

* 使用 WITH ROLLUP 关键字之后，在所有查询出的分组记录之后增加一条记录，该记录计算查询出的所 有记录的总和，即统计记录数量。

**说明**：当使用ROLLUP时，不能同时使用ORDER BY子句进行结果排序，即ROLLUP和ORDER BY是互相排斥的。

```mysql
#错误的：
SELECT department_id,AVG(salary) avg_sal
FROM employees
GROUP BY department_id WITH ROLLUP
ORDER BY avg_sal ASC;
```

#### (3)HAVING

> 和WHERE相似，用于过滤分组，但是和WHERE不全相同。
>
> * 行已经被分组。
> * 使用了聚合函数。 
> * 满足HAVING 子句中条件的分组将被显示。
> * HAVING 不能单独使用，必须要跟 GROUP BY 一起使用。

```mysql
SELECT department_id, MAX(salary)
FROM employees
GROUP BY department_id
HAVING MAX(salary)>10000 ;
```

* **非法使用聚合函数** ： 不能在 WHERE 子句中使用聚合函数。

```mysql
#错误
SELECT department_id, AVG(salary)
FROM employees
WHERE AVG(salary) > 8000
GROUP BY department_id;
```

* WHERE和HAVING的对比

> * **区别1**：WHERE 可以直接使用表中的字段作为筛选条件，但不能使用分组中的计算函数作为筛选条件； HAVING 必须要与 GROUP BY 配合使用，可以把分组计算的函数和分组字段作为筛选条件。 这决定了，在需要对数据进行分组统计的时候，HAVING 可以完成 WHERE 不能完成的任务。这是因为， 在查询语法结构中，WHERE 在 GROUP BY 之前，所以无法对分组结果进行筛选。HAVING 在 GROUP BY 之 后，可以使用分组字段和分组中的计算函数，对分组的结果集进行筛选，这个功能是 WHERE 无法完成 的。另外，WHERE排除的记录不再包括在分组中。 
> * **区别2**：如果需要通过连接从关联表中获取需要的数据，WHERE 是先筛选后连接，而 HAVING 是先连接 后筛选。 这一点，就决定了在关联查询中，WHERE 比 HAVING 更高效。因为 WHERE 可以先筛选，用一 个筛选后的较小数据集和关联表进行连接，这样占用的资源比较少，执行效率也比较高。HAVING 则需要 先把结果集准备好，也就是用未被筛选的数据集进行关联，然后对这个大的数据集进行筛选，这样占用 的资源就比较多，执行效率也较低。

|        | 优点                         | 缺点                                   |
| ------ | ---------------------------- | -------------------------------------- |
| WHERE  | 先筛选数据再关联，执行效率高 | 不能使用分组中的计算函数进行筛选       |
| HAVING | 可以使用分组中的计算函数     | 在最后的结果集中进行筛选，执行效率较低 |

* 开发中的选择

> WHERE 和 HAVING 也不是互相排斥的，我们可以在一个查询里面同时使用 WHERE 和 HAVING。包含分组 统计函数的条件用 HAVING，普通条件用 WHERE。这样，我们就既利用了 WHERE 条件的高效快速，又发 挥了 HAVING 可以使用包含分组统计函数的查询条件的优点。当数据量特别大的时候，运行效率会有很 大的差别。



#### (4)SELECT的执行过程

*  **查询的结构**

```mysql
#方式1：
SELECT ...,....,...
FROM ...,...,....
WHERE 多表的连接条件
AND 不包含组函数的过滤条件
GROUP BY ...,...
HAVING 包含组函数的过滤条件
ORDER BY ... ASC/DESC
LIMIT ...,...
#方式2：
SELECT ...,....,...
FROM ... JOIN ...
ON 多表的连接条件
JOIN ...
ON ...
WHERE 不包含组函数的过滤条件
AND/OR 不包含组函数的过滤条件
GROUP BY ...,...
HAVING 包含组函数的过滤条件
ORDER BY ... ASC/DESC
LIMIT ...,...
#其中：
#（1）from：从哪些表中筛选
#（2）on：关联多表查询时，去除笛卡尔积
#（3）where：从表中筛选的条件
#（4）group by：分组依据
#（5）having：在统计结果中再次筛选
#（6）order by：排序
#（7）limit：分页
```

*  **SELECT执行顺序**

1. 关键字的顺序是不能颠倒的：

```mysql
SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... LIMIT...
```

2.SELECT 语句的执行顺序（在 MySQL 和 Oracle 中，SELECT 执行顺序基本相同）：

```mysql
FROM -> WHERE -> GROUP BY -> HAVING -> SELECT 的字段 -> DISTINCT -> ORDER BY -> LIMIT
```

**实例**：

```mysql
SELECT DISTINCT player_id, player_name, count(*) as num # 顺序 5
FROM player JOIN team ON player.team_id = team.team_id # 顺序 1
WHERE height > 1.80 # 顺序 2
GROUP BY player.team_id # 顺序 3
HAVING num > 2 # 顺序 4
ORDER BY num DESC # 顺序 6
LIMIT 2 # 顺序 7
```

