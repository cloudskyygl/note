# MySQL 安装指南

## 内容概要

[在 Windows 上安装](#在-Windows-上安装)

## 安装依赖



## 在 Windows 上安装

**仅适用于 ZIP 归档文件形式的安装包**

* 解压缩到指定目录，假定安装目录为 **%MYSQL_HOME%**

* 创建选项文件

  - https://dev.mysql.com/doc/refman/5.7/en/windows-create-option-file.html

  - MySQL 查找选项文件的路径参考 https://dev.mysql.com/doc/refman/5.7/en/option-files.html

  - 可以在 %MYSQL_HOME% 下创建选项文件 my.ini

```
[mysqld]
# set basedir to your installation path
basedir=E:/mysql
# set datadir to the location of your data directory
datadir=E:/mydata/data
```

* 使用 mysqld 手动初始化 data 目录, https://dev.mysql.com/doc/refman/5.7/en/data-directory-initialization-mysqld.html

需要管理员权限

```cmd
D:\MySQL\mysql-server>bin\mysqld --defaults-file=D:\MySQL\mysql-server\my.ini --initialize --console
```

注: 日期2017-9-20 版本5.7.19 选项--defaults-file 默认使用相对当前目录的路径

* 首次启动 mysql:https://dev.mysql.com/doc/refman/5.7/en/windows-server-first-start.html

```cmd
D:\MySQL\mysql-server>bin\mysqld --console
```

* 把 `%MYSQL_HOME%\bin` 加入环境变量 PATH
>You should not add the MySQL bin directory to your Windows PATH if you are running multiple MySQL servers on the same machine.https://dev.mysql.com/doc/refman/5.7/en/windows-start-service.html

```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
```

* 测试

https://dev.mysql.com/doc/refman/5.7/en/testing-server.html

```cmd
shell> mysqladmin -u root -p version
shell> mysqladmin -u root -p variables
shell> mysqlshow -u root -p
shell> mysqlshow -u root -p mysql
shell> mysql -u root -p -e "SELECT User, Host, plugin FROM mysql.user" mysql
```

实际操作知道下面的语句也是可行的

```cmd
 mysql -u root -p -e "SELECT User, Host, plugin FROM mysql.user"
 mysql -u root -p -e "SELECT User, Host, plugin FROM user" mysql
```

```cmd
shell> mysqladmin -u root -p shutdown
```

* 创建服务

先关闭 mysql `mysqladmin -u root -p shutdown`

安装服务:
https://dev.mysql.com/doc/refman/5.7/en/windows-start-service.html
需要管理员权限

```cmd
> mysqld --install #启动类型为自动
> msyqld --install-manual #或者手动安装，启动类型为手动
> net start mysql
```
