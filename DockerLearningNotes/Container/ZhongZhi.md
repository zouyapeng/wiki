# 终止

可以使用 docker stop 来终止一个运行中的容器。

此外，当Docker容器中指定的应用终结时，容器也自动终止。 例如对于上一章节中只启动了一个终端的容器，用户通过 exit 命令或 Ctrl+d 来退出终端时，所创建的容器立刻终止。

```bash
$ docker stop f25d00c5b49b
f25d00c5b49b
```