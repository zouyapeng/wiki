# 进入

## docker attach

在使用 -d 参数时，容器启动后会进入后台。 某些时候需要进入容器进行操作
```bash
$ docker run -d ubuntu:14.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"
bf7d5922f9fe4949608ed0bdd67d2e496873580399a41d1cd21af4282aa8b104
$ docker attach bf7d5922f9fe
hello world
hello world
hello world
hello world

```

## docker exec
docker attach会进入进入容器并继续执行CMD,类似于linux的fg命令

```bash
$ docker exec -it bf7d5922f9fe /bin/bash
```