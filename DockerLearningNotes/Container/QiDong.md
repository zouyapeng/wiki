er# 启动
当利用docker run 来创建容器时,Docker在后台运行的标准操作包括:

- 检查本地是否存在指定的镜像,不存在就从公有仓库下载
- 利用镜像创建并启动一个容器
- 分配一个文件系统,并在只读的镜像层外面挂载一层可读写层
- 从宿主主机配置的网桥接口中桥接一个虚拟接口到容器中去
- 从地址池配置一个ip地址给容器
- 执行用户指定的应用程序
- 执行完毕后容器被终止

## hello world
```bash
$ docker run hello-world
```

## 交互模式
```bash
$ docker run -it ubuntu:14.04 /bin/bash
root@57064404d74b:/#

# -t 分配一个伪终端(pseudo-tty)并绑定到容器的标准输入上
# -i 标准输入保持打开
```

## 启动已终止容器
```bash
docker start 57064404d74b
```

## 后台运行
```bash
# 添加了-d参数
$ docker run -d ubuntu:14.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"
f25d00c5b49b7601259e6f873148a924185e15921f626e12340dbfb05304354d

# 使用docker logs 查看日志
$ docker logs -f dof25d00c5b49b
hello world
hello world
hello world
hello world
hello world
hello world
hello world
hello world

```