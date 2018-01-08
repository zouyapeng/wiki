### history 查看时间
```bash
echo 'export HISTTIMEFORMAT="%F %T `whoami` "' >> /etc/profile
source /etc/profile
```
执行上面的语句,再执行history就是有时间了

<font color="red">注意:在source修改之前的命令都是一样的，为这次登录机器的时间，之后只要不重启，就会一直有时间信息</font>
