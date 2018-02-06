# CentOS 7安装

## 准备
- Docker需要64位的操作系统
- Linux kernel 版本不得低于3.10

## 安装
- 更新
```bash
$ sudo yum update
```

- 添加源
```bash
$ sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/centos/$releasever/
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF
```

- 安装docker
```bash
$ sudo yum install docker-engine
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
