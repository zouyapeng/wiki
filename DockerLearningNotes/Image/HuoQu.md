# 获取

可以使用docker pull 命令来从仓库获取所需要的镜像。

下面的例子将从Docker Hub仓库下载一个Ubuntu 14.04操作系统的镜像。

```bash
$ docker pull ubuntu:14.04
14.04: Pulling from library/ubuntu
6c953ac5d795: Pull complete 
3eed5ff20a90: Pull complete 
f8419ea7c1b5: Pull complete 
51900bc9e720: Pull complete 
a3ed95caeb02: Pull complete 
Digest: sha256:7c151496aefa83d7d5faeff87493d471f86ff5673b829b0e1724e66be69d011c
Status: Downloaded newer image for ubuntu:14.04
```
该命令实际上相当于
```bash
$ docker pull docker.io/ubuntu:14.04
```
即从官方仓库注册服务器获取镜像。

14.04为镜像的tag。

有时候官方仓库注册服务器下载较慢，甚至不能下载,这时可以从其他仓库下载或者翻墙。
