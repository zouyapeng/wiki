# 导出导入

## 导出
```bash
$ docker save -o ubuntu_14.04.tar ubuntu:14.04
```

## 导入
```bash
$ docker load --input ubuntu_14.04.tar
$ docker load < ubuntu_14.04.tar
```