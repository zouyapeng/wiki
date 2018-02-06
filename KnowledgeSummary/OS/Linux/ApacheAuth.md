## 修改或者创建conf文件
```bash
$ vim /etc/httpd/conf.d/auth_basic.conf
```
```bash
[root@www ~]# vi /etc/httpd/conf.d/auth_basic.conf
# create new
<Directory /var/www/html/auth-basic>
    AuthType Basic
    AuthName "Basic Authentication"
    AuthUserFile /etc/httpd/conf/.htpasswd
    require valid-user
</Directory>
# add a user : create a new file with "-c" ( add the "-c" option only for the initial registration )
```
```bash
[root@www ~]# htpasswd -c /etc/httpd/conf/.htpasswd cent 
New password: # set password
Re-type new password: # confirm
Adding password for user cent
[root@www ~]# systemctl restart httpd
[root@www ~]# mkdir /var/www/html/auth-basic 
[root@www ~]# vi /var/www/html/auth-basic/index.html
# create a test page
 <html>
<body>
<div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
Test Page for Basic Auth
</div>
</body>
</html>
```
##  打开浏览器试试
会有认证框出来

[参考](http://www.server-world.info/en/note?os=CentOS_7&p=httpd&f=8)
