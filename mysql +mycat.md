## mysql 5.7 安装

` wget http://repo.mysql.com/mysql57-community-release-el7-8.noarch.rpm`

`rpm -ivh mysql57-community-release-el7-8.noarch.rpm `

`yum install mysql-server`

`systemctl start mysqld`

5.7版本的root账号有一个随机码，grep "password" /var/log/mysqld.log

mysql -uroot -p

输入随机码

修改密码

* set global validate_password_length=1;
* set global validate_password_policy=0;
* set password=password("root");



赋权：

GRANT ALL PRIVILEGES ON \*.\* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;







主：

创建一个用户

` create user repl identified by 'repl';`

 `GRANT ALL PRIVILEGES ON \*.\* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;`

赋权：

`grant replication slave on *.* to 'repl'@'%' identified by 'repl';`



配置文件：`/etc/my.cnf`

数据文件和二进制文件: `/var/lib/mysql`



vi /etc/my.cnf

`log-bin=mysql-bin
server-id=129`

重启：`systemctl restart mysqld`

登录：

mysql: `show master status;`





slave:

中继日志：

server-id=142

relay-log=slave-relay-bin

relay-log-index=slave-relay-bin.index

read_only=1

重启。

登录进去

`change master to master_host='192.168.144.129',master_port=3306,master_user='repl',master_password='repl',master_log_file='mysql-bin.000001',master_log_pos=154;`

`start slave;`

`show slave status\G;`

slave由iothread和SQLThread 



binlog有3种格式：

* statement 基于sql语句   （有些函数，uuid，now()等，不能用这个）

* row：基于行模式，记录修改以后每一条记录变化的值

* mixed： 混合模式，由mysql自动判断处理

  修改binlog_formater

  set global binlog_format=row

  





## mycat  TDDL   Sharding-JDBC   cobar

MYCAT:

* schema  逻辑数据库
* rule 表的分片规则
* server



