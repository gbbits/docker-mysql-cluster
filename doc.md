# master 步骤

#### 1.创建用户
`create user mysqlsync;`
#### 2.赋予权限及密码
`GRANT REPLICATION SLAVE ON *.* TO 'mysqlsync'@'%' IDENTIFIED BY 'mysqlsync';`
#### 2-1.使上面配置生效
`flush privileges;`
#### 3.锁库,这个命令在结束终端会话的时候会自动解锁
`FLUSH TABLES WITH READ LOCK;`
#### 4.查看master状态
`show master status;`
#### 5.记下 File 和 Position 字段值
mysql-bin.000003
789

# slave 步骤
#### 1.连接 master
`change master to master_host='mysql-master', master_user='mysqlsync', master_password='mysqlsync', master_port=3306, master_log_file='mysql-bin.000003', master_log_pos=789, master_connect_retry=30;`  
master_host: Master 的IP地址  
master_user: 在 Master 中授权的用于数据同步的用户  
master_password: 同步数据的用户的密码  
master_port: Master 的数据库的端口号  
master_log_file: 指定 Slave 从哪个日志文件开始复  制数据，即上文中提到的 File 字段的值  
master_log_pos: 从哪个 Position   开始读，即上文中提到的 Position 字段的值  
master_connect_retry: 当重新建立主从连接时，如果连接失败，重试的时间间隔，单位是秒，默认是60秒。
#### 2.开始开启主从同步
`start slave;`
#### 3.查看主从同步状态
`show slave status \G;`
##### 注意查看Slave_IO_Running、Slave_SQL_Running这两列必须为yes


