# Ubuntu 14.04安装
## 准备
- Docker需要64位的操作系统
- Linux kernel 版本不得低于3.10

### 跟新源
```bash
$ sudo apt-get update
$ sudo apt-get install apt-transport-https ca-certificates
```

### 添加GPG key
```bash
$ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```

### 检查docker.list
```bash
$ sudo vim /etc/apt/sources.list.d/docker.list 
```
修改内容：
```bash
deb https://apt.dockerproject.org/repo ubuntu-trusty main
```

### 跟新docker源
```bash
$ sudo apt-get update
```

## 安装
- 安装docker
```bash
$ sudo apt-get install docker-engine
```

- 启动服务
```bash
$ sudo service docker start
```

- 测试
```bash
$ sudo docker run hello-world
```

## run without sudo
- 添加当前用户到docker组
```bash
$ sudo groupadd docker
$ sudo gpasswd -a ${USER} docker
$ sudo service docker restart
```

- 注销当前用户，重新登陆




