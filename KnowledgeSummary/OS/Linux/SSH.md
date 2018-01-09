# Shell Aliases
## 正常情况下
```bash
ssh test@example.com -p 30001
password:******
```
每次都要输入好麻烦。


## 使用密钥对（ssh-copy-id）
```bash
$ ssh-copy-id test@example.com -p 30001
password:******
$ ssh test@example.com -p 30001
```
不要输入密码了，但是还是很麻烦。

## 使用alias
```bash
$ alias ssh-example='ssh test@example.com -p 30001'
$ ssh-example
```
这样就听方便的了，但是，要把alias语句写入.bashrc，才能每次打开一个终端才生效

## ~/.ssh/config
虽然上面的方法方便的ssh操作，但是还有很多更加灵活的解决方法。
```bash
# create it if no such file
$ cat ~/.ssh/config
# contents of $HOME/.ssh/config
Host example
    HostName example.com
    Port 30001
    User test
    
$ ssh example
```
[How To Configure Custom Connection Options for your SSH Client](https://www.digitalocean.com/community/tutorials/how-to-configure-custom-connection-options-for-your-ssh-client)

