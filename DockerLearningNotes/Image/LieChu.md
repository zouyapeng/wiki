# 列出

使用docker images显示本地已有的镜像。

```bash
zyp@work:~$ docker images 
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
ubuntu               14.04               8f1bd21bd25c        4 days ago          188 MB
zouyapeng/dokuwiki   latest              c9bf1b678f65        2 weeks ago         266.1 MB
```

在列出信息中,可以看到几个字段信息

REPOSITORY | TAG | IMAGE ID | CREATED | SIZE
- | - | - | - | - 
来自于哪个仓库 | 标记 | 镜像唯一ID | 创建时间 | 镜像大小 

IMAGE ID唯一标识了镜像,注意到 ubuntu:14.04 和 ubuntu:trusty 具有相同的镜像ID,说明它们实际上是同一镜像。

TAG信息用来标记来自同一个仓库的不同镜像。

例如 ubuntu 仓库中有多个镜像,通过 TAG 信息来区分发行版本, 10.04、12.04、12.10、13.04、14.04等。

如果不指定具体的标记,则默认使用 latest 标记信息。