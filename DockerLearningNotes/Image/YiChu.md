# 移除
## 使用docker rmi来移除镜像
```bash
$ docker rmi ubuntu:14.04
```
## 清理所有未打过标签的本地镜像
```bash
$ docker rmi $(docker images -q -f "dangling=true")
$ docker rmi $(docker images --quiet --filter "dangling=true")
```