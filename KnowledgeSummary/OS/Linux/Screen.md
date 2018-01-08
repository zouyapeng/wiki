## .screenrc
```bash
# GNU Screen - main configuration file 
# All other .screenrc files will source this file to inherit settings.
# Author: Christian Wills - cwills.sys@gmail.com

# Allow bold colors - necessary for some reason
attrcolor b ".I"

# Tell screen how to set colors. AB = background, AF=foreground
termcapinfo xterm 'Co#256:AB=\E[48;5;%dm:AF=\E[38;5;%dm'

# Enables use of shift-PgUp and shift-PgDn
termcapinfo xterm|xterms|xs|rxvt ti@:te@

# Erase background with current bg color
defbce "on"

# Enable 256 color term
term xterm-256color

# Cache 30000 lines for scroll back
defscrollback 30000

hardstatus alwayslastline 
# Very nice tabbed colored hardstatus line
hardstatus string '%{= Kd} %{= Kd}%-w%{= Kr}[%{= KW}%n %t%{= Kr}]%{= Kd}%+w %-= %{KG} %H%{KW}|%{KY}%101`%{KW}|%D %M %d %Y%{= Kc} %C%A%{-}'

# change command character from ctrl-a to ctrl-b (emacs users may want this)
#escape ^Bb

# Hide hardstatus: ctrl-a f 
bind f eval "hardstatus ignore"
# Show hardstatus: ctrl-a F
bind F eval "hardstatus alwayslastline"
```

## 创建screen
```bash
screen -S test
```

### 新建windows
```bash
ctrl + a  c
```

### 修改windows name
```bash
ctrl + a  a
```

### 切换windows
```bash
ctrl + a N     # 下一个windows
ctrl + a P     # 前一个windows
ctrl + a 1     # windows id
```

## 会话分离和恢复
```bash
# 分离
ctrl+a d

# 查看
$ screen -ls

# 恢复
$ screen -r test
```

## 退出screen
```bash
ctrl+a k
```

## 会话共享
```bash
# 可以多人同时连接一个screen，所有操作都是同步的。
$ screen -x test
```

## 会话锁定与解锁
```bash
# 锁定以后，再进行任何输入屏幕都不会再有反应了。但是要注意虽然屏幕上看不到反应，但你的输入都会被Screen中的进程接收到
ctrl+a s

# 解锁一个会话
ctrl+a q

# 锁定会话，不同的是这样锁定之后，会话会被Screen所属用户的密码保护，需要输入密码才能继续访问这个会话。
ctrl+a x
```

## 屏幕分割
```bash
# 显示器水平分割
ctrl+a S 

# 显示器垂直分割
ctrl+a |

# 区块间切换
ctrl+a tab

# 关闭当前焦点所在的屏幕区块
ctrl+a X

# 除当前区块之外其他的所有区块
ctrl+a Q
```

## C/P模式和操作
```bash
# 进入copy/paste模式，这个模式下可以像在vi中一样移动光标，并可以使用空格键设置标记。其实在这个模式下有很多类似vi的操作，譬如使用/进行搜索，使用y快速标记一行，使用w快速标记一个单词等。关于C/P模式下的高级操作，其文档的这一部分有比较详细的说明
ctrl+a Esc

# 一般情况下，可以移动光标到指定位置，按下空格设置一个开头标记，然后移动光标到结尾位置，按下空格设置第二个标记，同时会将两个标记之间的部分储存在copy/paste buffer中，并退出copy/paste模式

# 将储存在buffer中的内容粘贴到当前窗口。
ctrl+a ]
```

