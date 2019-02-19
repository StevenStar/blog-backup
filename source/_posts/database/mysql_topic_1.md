---
title: MYSQL 学习笔记
date: 2017-05-27 16:14:28
tags: Database
category: 数据库
---

## 安装
1. `Linux/Unix` 上安装 `MYSQL`
`mysql` -- 服务器
`mysql-client` -- 客服端程序，用于连接并操作数据库
`mysql-devel` -- 库和包含文件
`mysql-shared` -- 该软件包包含某些语言和应用程序需要动态装载的共享库
`mysql-bench` -- 基准和测试工具
2. 验证是否安装成功
```
~$ mysqladmin --version
// 判断是否启动
~$ ps -ef | grep mysqld
```
3. 登录
```
// mysql -h 主机名 -u 用户名 -p
~$ mysql -u root -p
```
4. 管理命令
```
// use 数据库名
mysql> use [RUNOOB];
// 列出数据库列表
mysql> show databases;
// 列出指定数据库所有表
mysql> show tables;
// 显示数据表的属性
mysql> show columns from [RUNOOB]
// 显示数据表的详情索引信息，包括主键
mysql> show index from [RUNOOB]
// 显示数据库管理系统的性能及统计信息
mysql: show table status linke [from db_name][linek 'pattern']\G:
```
## 数据库操作
```
// 创建数据库
mysql> create database 数据库名;
// 删除数据库
mysql> drop database 数据库名;
```
## 数据类型
1. 数值类型
tinyint 1字节
smallint 2字节
mediumint 3
int/integer 4
bigint 8
float 4
double 8
decimal
2. 日期和时间类型
date
time
year
datetime
timestamp
3. 字符串类型
char
varchar
tinyblob
tinytext
blob
mediumblob
mediumtext
longblob
longtext
## 表操作
```
// 创建表
mysql> create table table_name (column_nmae column_type);
// 删除表
mysql> drop table table_name;
// 插入数据
mysql> insert into table_nmae (field1, field2, ...) values (value1, value2, ...);
// 查询数据
mysql> select column_name,column_name from table_name [where Clause] [limit N] [offset M];
// where 子句
mysql> select field1, field2, ... from table_name1, table_name2... [where condition1 [and|or] condition2...];
// 修改表
mysql> update table_name set field1=newvalue1, field2=newvalue2 [where Clause];
// 删除表数据
mysql> delete from table_name [where Clause];
// like语句
mysql> select field1, field2... from table_name where field1 like condition1 [and|or] field2 = 'somevalue';
// union操作符
mysql> select expression1, expression2... from tables [where condition] union [all|distinct] select expression1, expression2... from tables [where conditions];
// 排序
mysql> select field1, field2... table_nam1, table_name2... order by field1,field2... [asc|desc];
// group by 语句 根据一个或多个列对结果集进行分组。
mysql> select column_name, function(column_name) from table_name where column_name operator value group by column_name;
// with rollup 语句 实现在分组统计数据基础上再进行相同的统计（SUM,AVG,COUNT…）。
...
// 正则表达式
mysql> select name from user where name REGEXP '^st';
```
## 连接的使用
`INNER JOIN`（内连接,或等值连接）：获取两个表中字段匹配关系的记录。
`LEFT JOIN`（左连接）：获取左表所有记录，即使右表没有对应匹配的记录。
`RIGHT JOIN`（右连接）： 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。
## 事务
。。。
## `nodejs` 连接数据库
1. 安装驱动
```
$ npm install mysql
```
2. 连接数据
```
const mysql = require('mysql');
const connection = mysql.createConnection({
	host: 'localhost',
	user: 'root',
	password: '123456',
	database: 'test'
});

connection.connect();

connection.query('select 1+1 as solution', function(error, results, fields) {
	if (error) throw error;
	console.log('The solution is: ', results[0].solution);
});
```
3. 数据库连接参数说明
`host` 主机地址（默认：localhost）
`user` 用户名
`password` 密码
`port` 端口号（默认：3306）
`database` 数据库名
`charset` 连接字符集（默认：'UTF8_GENERAL_CI'，注意字符集的字母都要大写）
localAddress` 此IP用于tcp连接（可选）
`socketPath` 连接到unix域路径，当使用host和port时忽略
`timezone` 失去（默认：'local'）
`connectTimeout` 连接超时（默认：不限制；单位：毫秒）
`stringfyObjects` 是否序列化对象
`typeCast` 是否将列值转化为本地js类型值（默认：true）
`queryFormat` 自定义query语句格式化方法
`supportBigNumbers`
`bigNumberStrings`
`dateStrings`
`debug`
`multipleStatements`
`flags`
`ssl`
4. 数据库操作(CURD)
```
const mysql = require('mysql');
const connection = mysql.createConnection({
	host: 'localhost',
	user: 'root',
	password: '123456',
	database: 'test'
});
// 增加
var addSql = 'insert into websites(id, name, url, alexa, country) values(0, ?, ?, ?, ?)';
var addSqlParams = ['菜鸟工具', 'https://c.runoob.com', '2342', 'CN'];
connection.query(addSql, addSqlParams, function(err, result) {
	if (err) {
		console.log('[insert error] - ', err.message);
		return;
	}
	console.log('insert id: ', result.insertId);
})
// 删除
var delSql = 'delete from websites where id = 6';
connection.query(delSql, function(err, result) {
	if (err) {
		console.log('[delete error] - ', err.message);
		return;
	}
	console.log('delete affectedRows: ', result.affectedRows);
})
// 更新
var modSql = 'update websites set name = ?, url = ? where id = ?';
var modParams = ['菜鸟以东站', 'https://m.runoob.com', 6];
connection.query(modSql, modParams, function(err, result) {
	if (err) {
		console.log('[update error] - ', err.message);
		return;
	}
	console.log('update affectedRows: ', result.affectedRows);
})
// 查询
var sql = 'select * from websites';
connection.query(sql, function(err, result) {
	if (err) {
		console.log('[select error] - ', err.message);
		return;
	}
	console.log('select result - ', result);
})
connection.connect();
```









