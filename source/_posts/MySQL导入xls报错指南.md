---
title: MySQL导入xls报错指南
tags:
  - Mac
  - MySQL
categories:
  - 填坑指南
abbrlink: 7ac9323a
date: 2018-02-14 16:48:08
toc: true
---

 今天是二月十四，传说中的情人节，在这样一个美好的日子里，不如一起来干一点有意义的事情，比如:在 Mac 上为 MySQL 导入 excel 数据 🌚

<!--more-->

## **基本步骤**

---

### 创建 TABLE

使用 CREATE TABLE 语句:

```mysql
CREATE TABLE `tablename`(
`id_name` int NOT NULL auto_increment primary key,
`content_name` varchar(20) NOT NULL
)ENGING=InnoDB DEFAULT CHARSET=utf8;
```

关键元素:

* tablename 　表名
* id_name content_name 　列名
* int varchar 　数据类型
* primary key 　主键

可选元素：

* NOT NULL 　不允许 NULL 值
* auto_increment 　自动匹配可用主键值，仅为主键可选项

其他:

* ENGING 　引擎
* CHARSET 编码，最好是 UTF-8

创建时应该关注导入数据的数据类型。

### 导入命令

使用 load 语句:

```mysql
LOAD DATA INFILE "your excel file path" INTO TABLE [tablename] fields terminated by '\t';
```

* path 　需要绝对路径
* DATA 　后面可以加 LOCAL，表示本地客户机文件
* 如果必要，在 fields 前面加 编码设置 character set utf8
* fields terminated by 　表示制表符，视情况而定

## **建议**

---

下面的建议也许帮忙避免一些不必要的麻烦:

* 将 xls 文件转为 TXT 或者 CSV 文件再导入
* 将导入文件储存为 UTF8 格式
* 注意文件的制表符分割，在选取制表符分割是建议是‘,’

## **报错处理**

---

乍看语法是很简单的，但是报错很扎心啊 QAQ

### Permission denied

```mysql
(13,u'at line 1: Cant get stat of `your excel file path`')
```

读取权限不够，尝试使用`LOAD DATA LOCAL INFILE`

### 配置问题

```mysql
(1290, u'The MySQL server is running with the --secure-file-priv option so it cannot execute this statement')
```

这是由于数据导入导出操作功能配置出现了问题,输入：

```mysql
show variables like '%secure%';
```

然后看到  
![secure](/media/secure.png)

secure-file-prive 为 NULL 的意思是不支持文件导入/出在~目录查找有没有 my.cnf,没有的话创建一个,然后在[mysqld]处添加：secure_file_priv=/tmp/mysqldata。将文件放在 secure-file-prive 路径下，就可以正常导入导出了。

> 这里提供一个小技巧,终端输入：

```sh
mysql --help | more
```

> 找到如： ![option](/media/option.png)

> 其中列举的是配置文件的合法路径

然后重启 MySQL 生效

```sh
mysql.server restart
```

### 配置文件不生效

重启后也许会出现：

```sh
my_print_defaults: [Warning] World-writable config file '/Users/bitcoin/.my.cnf' is ignored.
```

这里是说配置文件权限太高不安全，系统自动忽略了给 🌚，权限改为 664 即可:

```shell
 chmod 644 /etc/my.cnf
```

664 为该用户可读写，其他用户只可读

### 编码问题

```json
(1300, u"Invalid utf8 character string: ''")
```

编码问题有时候确实很头疼，导入 MySQL 要确保是 UTF8 格式，然而讲道理只要将 excel 另存为 UTF8 格式的 TXT 后者 CSV 格式即可。

> 酱，excel 终于导入 MySQL 了 🌞，节日快乐么么哒。
