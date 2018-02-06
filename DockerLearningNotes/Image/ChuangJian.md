
# 创建
## 创建Ubuntu基础镜像
```bash
$ sudo [debootstrap](https://wiki.debian.org/Debootstrap) trusty trusty > /dev/null
$ sudo tar -C trusty -c . | docker import - trusty
sha256:2c2a1ef844faf88c0fd6e188ad68e08e42ab7732071c2a41a23e287af1efdde1
$ docker run trusty cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=14.04
DISTRIB_CODENAME=trusty
DISTRIB_DESCRIPTION="Ubuntu 14.04 LTS"
```

在Docker GitHub仓库里还有创建其他基础镜像的脚本的例子:

- [BusyBox](https://github.com/docker/docker/blob/master/contrib/mkimage-busybox.sh)
- CentOS / Scientific Linux CERN (SLC) on [Debian/Ubuntu](https://github.com/docker/docker/blob/master/contrib/mkimage-rinse.sh) or on [CentOS/RHEL/SLC/etc](https://github.com/docker/docker/blob/master/contrib/mkimage-yum.sh).
- [Debian / Ubuntu](https://github.com/docker/docker/blob/master/contrib/mkimage-debootstrap.sh)



## 使用Dockerfile创建镜像

```bash
$ mkdir trusty && cd trusty
$ touch Dockerfile
$ touch run.sh
```
run.sh:
```bash
#!/bin/bash
if [ $# == 1 ];then
    echo $1
elif [ $# == 2 ];then
    echo $2
elif [ $# == 3 ];then
    echo $3
else
    echo '----'
fi
```
Dockerfile:
```Dockerfile
FROM trusty:latest

MAINTAINER Zouyapeng<zyp19901009@163.com>

ENV \
  TEST_ENV1=123456 \
  TEST_ENV2=true \
  TEST_ENV3=/var/log

RUN apt-get update && apt-get install -y \
  apache2 \
  php5
  
COPY run.sh /

RUN chmod +x /run.sh

COPY . /tmp/
# ADD http://example.com/big.tar.xz /

VOLUME ["/etc/custom-config", "/opt/user"]

EXPOSE 80 443 162/udp 22 10080

ENTRYPOINT ["/run.sh"]
CMD ["param1","param2","param3"]
```

```bash
$ docker build -t="trusty:custom" .
Sending build context to Docker daemon 3.072 kB
Step 1 : FROM trusty:latest
 ---> 2c2a1ef844fa
Step 2 : MAINTAINER Zouyapeng<zyp19901009@163.com>
 ---> Using cache
 ---> 6de654f69aa5
Step 3 : ENV TEST_ENV1 123456 TEST_ENV2 true TEST_ENV3 /var/log
 ---> Using cache
 ---> 530a80f32021
Step 4 : RUN apt-get update && apt-get install -y   apache2   php5
 ---> Using cache
 ---> 567c91ceeb2b
Step 5 : COPY run.sh /
 ---> Using cache
 ---> 064dbb556a6f
Step 6 : RUN chmod +x /run.sh
 ---> Using cache
 ---> 3c0398aaec8c
Step 7 : VOLUME /etc/custom-config /opt/user
 ---> Running in 789fed374aed
 ---> f900bb13e8fd
Removing intermediate container 789fed374aed
Step 8 : EXPOSE 80 443 162/udp 22 10080
 ---> Running in e60d416f815c
 ---> 0ba17f4d19b1
Removing intermediate container e60d416f815c
Step 9 : ENTRYPOINT /run.sh
 ---> Running in 32c7d0383e7b
 ---> b304a2716df7
Removing intermediate container 32c7d0383e7b
Step 10 : CMD param1 param2 param3
 ---> Running in b43e771e38e7
 ---> 2e1f283c5aa9
Removing intermediate container b43e771e38e7
Successfully built 2e1f283c5aa9
```

```bash
$ docker images 
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
trusty               custom              2e1f283c5aa9        51 seconds ago      291 MB
trusty               latest              2c2a1ef844fa        About an hour ago   232.7 MB
```

```bash
$ docker run -i trusty:custom 1111
1111
$ docker run -i trusty:custom 1111 2222
2222
$ docker run -i trusty:custom 1111 2222 3333
3333
$ docker run -i trusty:custom 1111 2222 3333 4444
----
$ docker run -i trusty:custom
param3
```

