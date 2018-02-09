## 常用命令
### 备份文件
```bash
$ cp /etc/nova/nova.cof{,.bak}
```

### 无密码sudo
```bash
$ sudo chmod 740 /etc/sudoers
 
$ sudo vim /etc/sudoers
 
#  在最下边添加如下内容
# stack是需要无密码执行sudo的用户
stack    ALL=(ALL) NOPASSWD: ALL
```

### recovery mode进入read-write模式
```bash
$ mount -o rw,remount /
```

### ubuntu 16.04 Desktop Setting
```bash
# 底部
gsettings set com.canonical.Unity.Launcher launcher-position Bottom
 
# 左边（Default）
gsettings set com.canonical.Unity.Launcher launcher-position Left

# 启动器最小化_恢复
gsettings set org.compiz.unityshell:/org/compiz/profiles/unity/plugins/unityshell/ launcher-minimize-window true

# Ubuntu工作区(4列1行)
dconf write /org/compiz/profiles/unity/plugins/core/hsize 4
dconf write /org/compiz/profiles/unity/plugins/core/vsize 1
```

### Mysql 
```mysql
# 查看现有连接
SHOW [FULL] PROCESSLIST;

# 查看DB size
SELECT table_schema AS "Database name", SUM(data_length + index_length) / 1024 / 1024 AS "Size (MB)" FROM information_schema.TABLES where table_schema = "memory" GROUP BY table_schema;

SELECT 
     table_schema as `Database`, 
     table_name AS `Table`, 
     round(((data_length + index_length) / 1024 / 1024), 2) `Size in MB` 
FROM information_schema.TABLES WHERE table_schema = "<your db_name>"
ORDER BY (data_length + index_length) DESC;
```