---
title: "数据库笔记"
tags: [ "MySQL", "Note"]
date: 2023-02-28
description: "描述了MySQL数据库的基础语法，含有增删改查，外键，视图，游标，存储过程，事务等知识"
slug: "database-note"
---
#### 创建数据库
>CREATE DATABASE name

#### 删除数据库
>DROP DATABASE name

#### 使用数据库
>USE name

#### 设置数据库编码字符集和排序方式
>ALTER DATABASE name
DEFAULT CHARACTER SET utf8
COLLATE utf8_general_ci;

#### 创建表
>CREATE TABLE IF NOT EXISTS name
(列 数据类型 (参数),
列 数据类型 (约束)，
特殊语句
)

- 从name2复制出新表name
>CREATE TABLE name AS SELECT * FROM name2

- 数据类型
  - CHAR(大小)
  - VARCHAR(大小)`可变字符数组`
  - DATE `日期`
  - YEAR
  - TIME
  - DATETIME `日期和时间`
  - DECIMAL(数字长度，小数位长度) `十进制数`
  - TINYINT `小整数(-128，127)`
  - SMALLINT `(-32768，32767)`
  - INT `(-2^32, 2^32-1)`
  - BIGINT `(-2^64, 2^64)`

- 参数
  - NOT NULL `非空`
  - PRIMARY KEY `主键`
  - DEFAULT number `默认值`
  - COMMENT `` `备注`
  - UNIQUE `唯一`
  - UNSIGNED `无符号`
  - AUTO_INCREMENT `自动增加编号`
  - CHECK() `条件约束`

- 特殊语句
  - CONSTRAINT 约束名称 (FOREIGN KEY(列) REFERENCES 表(列))`外键约束`

#### 查询表
>SHOW TABLES (LIKE 'sc%') 查询当前表中sc开头的数据表

>SHOW TABLES STATUS (FROM name)(LIKE XXX)

- 查看表结构
>DESC|DESCRIBE name 字段
>SHOW COLUMNS FROM name

- 查看表的创建语句
>SHOW CREATE TABLE name

#### 修改表
>ALTER TABLE name RENAME TO|AS newname

>RENAME TABLE name TO newname

- 修改字符集
>ALTER TABLE name CHARSET=utf8

- 修改表结构
>ALTER TABLE name ADD 字段 类型 (FIRST|AFTER name2)

- 修改字段名
>ALTER TABLE name CHANGE oldname newname type

- 修改字段类型和位置
>ALTER TABLE name MODIFY name2 type (FIRST|AFTER name3)

- 删除字段
>ALTER TABLE name DROP name2

- 添加约束
>ALTER TABLE name ADD CONSTRAINT name2 UNIQUE(sno,cno)

- 删除约束
>ALTER TABLE name DROP CONSTRAINT name2

#### 删除表
>DROP TABLE name 删除整个表
>TRUNCATE TABLE name 删除全部数据
>DELETE TABLE name  删除部分数据

#### 查询数据
>SELECT 目标表达式 FROM 表 WHERE 条件表达式

- 目标表达式
>AS name 别名

>COUNT((DISTINCT) 列名) 统计该列有几行

>SYSDATE() 当前日期

>SUM(列名) 求和

>AVG(列名) 平均数

>MAX(列名) 最大值

>MIN(列名) 最小值


- 条件表达式
>(NOT) BETWEEN data1 AND data2 限制范围

>GROUP BY name 按列名分组(提取同一类型数据)

>HAVING 选择满足条件的组

>DISTINCT   放在列名前，对该列去重

>(NOT) IN 放在（WHERE 列）后面 表示(不)在某集合里

>（NOT）EXISTS(查询表达式) 放在where后面表示查询条件

>ORDER BY 列名 ASC/DESC 升序、降序输出

>LIMIT x,y 筛选第x行开始y行
>LIMIT (x-1) * 每页显示数量, 每页显示数量 显示第x页

>(NOT) LIKE '条件' 模糊查询

'%'表示任意字符，'_'表示任一个字符，使用'\'转义为普通字符

>IS (NOT) NULL (非)空

#### 链接查询
- 交叉连接
>SELECT * FROM student CROSS JOIN course 交叉链接，笛卡尔积
>SELECT * FROM student,course

- 内连接（查询满足条件的行，支持其中一个表中行为NULL
>table1 INNER JOIN table2 ON table1.column = table2.column

- 自然连接
>table1 NATURAL JOIN table2 NATURAL JOIN table3...
>table1 JOIN table2 USING(列名)

- 自身连接
>SELECT b.column FROM table a(别名) JOIN table b(别名) ON a.column 比较运算符 b.column where ...

- 外连接（将满足条件但其他位置为空的填为NULL
>table1 LEFT/RIGHT OUTER JOIN table2 ON 连接条件

满连接
>SELECT * FROM 左连接 UNION SELECT * FROM 右连接

#### 子查询
- 在限定范围内查询
>SELECT FROM WHERE 条件 比较运算符 [(NOT)ANY/(NOT)ALL] / (NOT)IN  
(SELECT FROM WHERE)

>SELECT FROM (SELECT FROM WHERE)

- 创建表
>CREATE TABLE table (SELECT FROM WHERE)

- 插入表
>INSERT INTO table (SELECT FROM WHERE)

- 子查询 UNION 子查询

#### 插入数据
>INSERT INTO student(sno,sname,dept) VALUES('001243','李四','计算机');
INSERT INTO student VALUES('001242','张青','计算机','女','04-01-22',50,'三好生');

- 从其他表中插入多个记录
>INSERT INTO stu SELECT sno,sname,sex,dept FROM student


#### 更新数据
>UPDATE name SET 列=新数值，列=新数值 (WHERE 条件)

>IFNULL(列，数值) 如果该列为NULL，返回数值
>UPDATE course SET credit = IFNULL(credit,0)+10 WHERE credit IS NULL;

#### 删除数据
>DELETE FROM name WHERE 条件

#### 创建索引
>CREATE UNIQUE/FULLTEXT/SPATIAL INDEX 索引名 ON 表名 (列名，列名(前x位长度)...) ;

#### 查看索引
>SHOW INDEX FROM tablename

#### 删除索引
>ALTER TABLE tablename DROP INDEX indexname； 
DROP INDEX indexname ON tablename ;

#### 查看索引使用情况
>EXPLAIN SELECT...

#### 索引命名规范
主键索引名为 pk_字段名；唯一索引名为 uk_字段名；普通索引名为 idx_字段名。

#### 索引设计
  - 条件子句中频繁使用的字段、数字型的字段、存储空间较小的字段适合建立索引；
  - 选择在WHERE子句、GROUP BY子句、ORDER BY子句或表与表之间连接运算等频繁使用的字段上建立索引
  - 重复值较高的字段、更新频繁的字段不适合建立索引
  - 索引字段的值很长，最好使用字段值的前缀建立索引
  >CREATE INDEX idx_came ON  course(cname(6));
  - 限制索引的数量，否则会降低系统效率

#### 索引使用
  - 模糊查询中通配符不要放在最左边使用
  - 对于联合索引，系统按从左到右的顺序使用索引中的字段，一个查询可以只使用索引中靠左侧部分。例如索引是index (a,b,c) 可以支持a、a,b、a,b,c三种组合进行查找，但不支持b,c或c进行查找。
  - 索引覆盖；当SELECT查询语句涉及的字段包含在复合索引文件中，WHERE语句不需要满足最左前缀匹配，系统也会按索引执行

#### 索引类别
  - PRIMARY：主键索引，索引列值唯一且不能为空
  - INDEX：普通索引，索引列没有任何限制
  - UNIQUE：唯一索引，索引列的值必须是唯一的，但允许有空值
  - FULLTEXT：全文索引
  - SPATIAL：空间索引，对空间数据类型的字段建立的索引(自学)
  - 哈希索引（也称HASH索引）：对于每一条行数据，存储引擎对所有的索引列计算一个哈希码。将所有的哈希码存储在索引中，同时在哈希表中保存指向每一个数据行的指针。系统自建。


#### 创建视图
>CREATE (OR REPLACE) VIEW viewname(name1,name2) AS SELECT... (WITH CHECK OPTION)

#### 修改视图
>ALTER VIEW viewname AS SELECT...

#### 删除视图
>DROP viewname

#### 查看视图字段信息
>DESCRIBE viewname

#### 查看视图创建语句
>SHOW CREATE VIEW viewname

#### 查看数据库下的视图
>SELECT * FROM table.views

#### 显示系统变量
>SHOW [GLOBAL | SESSION] VARIABLES LIKE ''

#### 设置系统变量
>SET {@@GLOBAL.|@@SESSION.|@@}name=value|DEFAULT

#### 设置用户变量
>SET @v_sno='02300'
SET @v_sno=(SELECT sno FROM student WHERE sname='王燕');
SELECT @num:=(SELECT COUNT(*) FROM student);
SELECT COUNT(\*) into @num FROM student;

#### 声明局部变量
>DECLARE name1,name2 type

在BEGIN...END内定义
使用SELECT或SET语句赋値，变量不以“@”开头。
作为存储过程或存储函数的形式参数时，无需声明，但需指定数据类型。

#### 改变结束符
>DELIMITER 符号

DELIMITER命令可以重新定义代码执行的结束符，用DELIMITER新定界符就是告诉MySQL解释器，代码的结束有了新的标识。

#### 循环
```sql
标签名:LOOP
  循环语句序列
  IF <条件> THEN
    LEAVE label / ITERATE label
  END IF 
END LOOP 标签名;
```

#### 创建存储过程
默认是IN
>CREATE PROCEDURE 过程名 ( [[IN|OUT|INOUT] 参数名 类型[,...]) BEGIN...END

#### 执行存储过程
>CALL name(参数1，参数2...)

- 例子
>DELIMITER //
CREATE PROCEDURE   pro_del_sc2 (v_sno CHAR(6),v_cno CHAR(3))
BEGIN
      DELETE FROM score WHERE sno=v_sno AND cno=v_cno;
END//
DELIMITER ;
CALL pro_del_sc2 ('001106','102');

>DELIMITER //
CREATE PROCEDURE pro_inquire(v_name VARCHAR(20))
BEGIN
  SELECT sno, sname FROM student WHERE sname LIKE CONCAT('%',v_name,'%');
END //
DELIMITER ;
CALL pro_inquire('林');


#### 定义游标
>DCELARE name CURSOR FOR SELECT...；

#### 打开游标
>OPEN name

#### 使用游标
>FETCH name INTO 变量名1,变量名2...;

#### 关闭游标
>CLOSE name

#### 定义异常处理程序
>DECLARE (CONTINUE|EXIT) HANDLER FOR 
(SQLWARNING|NOT FOUND|SQLEXCEPTION) 处理语句

CONTINUE：表示遇到错误不处理，继续执行。
EXIT：表示遇到错误马上退出。

SQLWARNING：匹配所有以01开头的错误代码；
NOT FOUND：匹配所有以02开头的错误代码；
SQLEXCEPTION：匹配所有没有被SQLWARNING或NOT FOUND捕获的错误代码；

#### 查看存储过程
>SHOW CREATE PROCEDURE name

#### 删除存储过程
DROP PROCEDURE name

#### 创建存储函数
>CREATE FUNCTION name(参数1，参数2) RETURNS 返回类型 
[DETERMINISTIC|NO SQL|READS SQL DATA] BEGIN...END

>
```sql
DELIMITER $$
DROP FUNCTION IF EXISTS func$$
CREATE FUNCTION func(v_sno CHAR(6)) RETURNS INT
DETERMINISTIC
BEGIN
   DECLARE sum_credit, v_grade,v_credit INT;    
   DECLARE v_done INT DEFAULT FALSE; 
   DECLARE cs_credit_grade CURSOR FOR    
   SELECT credit,grade  FROM course JOIN score ON course.cno=score.cno WHERE sno=v_sno;
   DECLARE CONTINUE HANDLER FOR NOT FOUND SET v_done=TRUE;          
   SET sum_credit=0;
   OPEN cs_credit_grade ;
   label:LOOP
                FETCH cs_credit_grade INTO v_credit,v_grade;
                 IF v_done THEN 
                       LEAVE label;
                END IF;           
                IF v_grade>=70 THEN
                    SET sum_credit=sum_credit+v_credit;
                END IF;               
         END LOOP label;
   CLOSE cs_credit_grade;
   RETURN sum_credit;
END$$
DELIMITER ;
```

#### 执行存储函数
>name
>SELECT name

#### 创建触发器
ORACLE支持一个触发器中设计多事件触发，MySQL不支持多个事件触发
>CREATE TRIGGER name (BEFORE|AFTER) (UPDATE|INSERT|DELETE) ON tablename FOR EACH ROW BEGIN ... END

例子
>DELIMITER //
DROP TRIGGER IF EXISTS trig_score//
CREATE TRIGGER trig_score AFTER UPDATE ON score
FOR EACH ROW
BEGIN
 INSERT INTO score_log(id, operate_date, operate_user, log_text)
 VALUES(NULL,NOW(),USER(),CONCAT('学号:', OLD.sno,'原成绩',OLD.grade,'新成绩', NEW.grade));
END //
DELIMITER ;

#### 查看触发器
>SHOW TRIGGERS

#### 查看某个触发器的详细信息 
>SHOW CREATE TRIGGER name

#### 删除触发器
>DROP TRIGGER IF EXISTS name

#### 数据加密
>CREATE TABLE users(username VARCHAR(128),pwd BLOB)
- 插入一条测试语句
>INSERT INTO users VALUES ('john', AES_ENCRYPT('guessme', '芝麻开门'))
- 查询john的密码 
>SELECT username, AES_DECRYPT(PASSWORD,'芝麻开门')  FROM users
- 插入一条测试语句
> INSERT INTO users VALUES ('jery', MD5('mypwd'))


#### 创建用户
创建一个新的用户user1，并设置密码为 user1，具体的SQL语句如下。
- 本地登录帐户
>CREATE USER user1@localhost IDENTIFIED BY 'password';
- 任何主机登录帐户
>CREATE USER user1 IDENTIFIED BY 'user1';
- 可添加参数
  - PASSWORD EXPIRE 密码设置为过期
  - PASSWORD EXPIRE DEFAULT 系统设置是否有效
  - PASSWORD EXPIRE NEVER   永不过期
  - PASSWORD EXPIRE INTRVAL n DAY 设置有效期为n天

#### 修改用户
>RENAME USER oldname TO newname;
RENAME USER user1@localhost TO user1@'202.208.5.8'

将user1密码修改为'user_1'，验证方式为 'sha256_password'，密码长期有效，用户为解锁状态，具体SQL语句如下。
>ALTER USER user1 IDENTIFIED  WITH 'sha256_password' BY 'user_1' PASSWORD EXPIRE NEVER ACCOUNT UNLOCK;

#### 删除用户
>DROP USER user1,user1@202.208.5.8;

#### 修改权限
- 权限类型
  - ALL PRIVILEGES
  - SELECT
  - INSERT
  - UPDATE
>GRANT ALL PRIVILEGES / SELECT,INSERT / SELECT,INSERT(grade)(对grade列) 
ON *.* / 数据库名.* / 数据库名.表名 / (字段列表)[,…] 
TO 账户名[WITH GRANT OPTION];

#### 查看权限
>SHOW GRANTS FOR username
- 查看数据库访问权限
SELECT * FROM mysql.tables_priv WHERE USER='用户名';

#### 收回权限
>REVOKE SELECT,UPDATE(grade) / SELECT,UPDATE / ALL ON teaching_manage.score FROM user1;

#### 创建角色
>CREATE ROLE [IF NOT EXISTS] role1,role2

#### 授权权限
>GRANT 权限列表 ON 数据库名.表名 TO 角色名`[WITH GRANT OPTION]

#### 为用户指定角色
>GRANT role TO user

#### 查看角色权限
>SHOW GRANTS FOR <角色|用户>

#### 收回角色权限
>REVOKE role FROM user

#### 删除角色
>DROP ROLE [IF EXISTS] role[,role]...

#### 数据备份
命令行操作
>mysqldump –u username -h host –ppassword databasename [tablename...] / --all_databases > filename.sql

#### 数据还原
>mysql -u username -p databasename < filename.sql

#### 二进制日志文件
- 查看是否开启
>SHOW VARIABLES LIKE 'log_bin%'

- 查看所有binlog日志列表
>SHOW BINARY LOGS

- 刷新log日志，并产生一个新编号的binlog日志文件
>FLUSH LOGS

- 删除所有binlog日志，重新建立二进制日志文件扩展名的编号从000001开始
>RESET MASTER

- 查看binlog日志内容
>SHOW BINLOG EVENTS IN 'name'

- 查看最后一条日志状态
>SHOW MASTER STATUS

### 事务
- 自动提交
>SET AUTOCOMMIT = 0;
>SET AUTOCOMMIT = 1;
- 开始事务
>START TRANSACTION;
- 提交事务
>COMMIT;
- 回滚事务
>ROLLBACK;
- 设置保存点
>SAVEPOINT savepoint_name;
- 回滚保存点
>ROLLBACK TO savepoint_name;
