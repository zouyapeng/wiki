
# 私有仓库

## 安装
### 容器安装
```bash
# 没有国外服务器的用户建议先使用pull下镜像
$ docker pull registry

$ docker run -d -p 5000:5000 -v /opt/registry:/tmp/registry registry
```
### Packages安装
- Ubuntu
```bash
$ sudo apt-get install -y build-essential python-dev libevent-dev python-pip liblzma-dev
$ sudo pip install docker-registry
```

- Centos
```bash
$ sudo yum install -y python-devel libevent-devel python-pip gcc xz-devel
$ sudo python-pip install docker-registry
```

## 其他更多查考我的wiki
[Docker私有仓库搭建(nginx代理)](http://wiki.zouyapeng.com/doku.php?id=docker%E7%A7%81%E6%9C%89%E4%BB%93%E5%BA%93%E6%90%AD%E5%BB%BA_nginx%E4%BB%A3%E7%90%86)