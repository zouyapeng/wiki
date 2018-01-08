# MYSQL的root密码忘记解决方法
> 首先确认服务器出于安全的状态，也就是没有人能够任意地连接MySQL数据库。 因为在重新设置MySQL的root密码的期间，MySQL数据库完全出于没有密码保护的 状态下，其他的用户也可以任意地登录和修改MySQL的信息。可以采用将MySQL对外的端口封闭，并且停止Apache以及所有的用户进程的方法实现服务器的准安全状态。最安全的状态是到服务器的Console上面操作，并且拔掉网线

## 修改MySQL的登录设置
```bash
vim /etc/mysql/my.cnf
```

在[mysqld]的段中加上一句：skip-grant-tables 保存并且退出vim

## 重新启动mysql服务
```bash
service mysqld restart
```

## 登录并修改MySQL的root密码
```bash
USE mysql; 
UPDATE user SET Password = password ( 'new-password' ) WHERE User = 'root'; 
flush privileges; 
exit;
```

## 去掉一开始无密码登录的设置，重新启动mysql
```bash
service mysqld restart
```
