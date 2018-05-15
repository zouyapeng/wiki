# 使用ngrok实现内网穿透
## 获取 ngrok 源码：
```bash
git clone https://github.com/inconshreveable/ngrok.git
```

## 生成并替换源码里默认的证书，注意域名修改为你自己的。（之后编译出来的服务端客户端会基于这个证书来加密通讯，保证了安全性）

```bash
NGROK_DOMAIN="ngrok.zouyapeng.com"

openssl genrsa -out base.key 2048
openssl req -new -x509 -nodes -key base.key -days 10000 -subj "/CN=$NGROK_DOMAIN" -out base.pem
openssl genrsa -out server.key 2048
openssl req -new -key server.key -subj "/CN=$NGROK_DOMAIN" -out server.csr
openssl x509 -req -in server.csr -CA base.pem -CAkey base.key -CAcreateserial -days 10000 -out server.crt

cp base.pem assets/client/tls/ngrokroot.crt
```

## 编译
```bash
# 如果一切正常，ngrok/bin 目录下应该有 ngrok、ngrokd 两个可执行文件
# 如果需要交叉编译，需要修改一下Makefile
sudo make release-server release-client
```

## 生产软链接
```bash
ln -s /path/to/ngrok/ngrokd /usr/local/sbin/ngrokd
ln -s /path/to/ngrok/ngrok /usr/local/sbin/ngrok
```

## 启动Server端（公网能访问到）
```bash
# 不知道怎么用的，可以ngrokd -h看一下
ngrokd -tlsKey=server.key -tlsCrt=server.crt -domain="ngrok.zouyapeng.com"
```

## 启动Clinet端（内网机器）
### 编写配置文件
```bash
server_addr: "ngrok.zouyapeng.com:4443"
inspect_addr: disabled
tunnels:
  work:
    remote_port: 10022
    proto:
      tcp: 192.168.0.10:22
```

### 启动
```bash
# 不知道怎么用的，可以ngrok -h看一下
ngrok -config=/opt/ngrok-client/ngrok.cfg start-all
```

## 验证
```bash
ssh bob@ngrok.zouyapeng.com -p 10022
```



