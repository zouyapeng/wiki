# 删除
## 删除某个容器
```bash
$ docker rm [container id or name]
```

## 删除退出状态容器
```bash
$ docker rm $(docker ps -a -q)
```