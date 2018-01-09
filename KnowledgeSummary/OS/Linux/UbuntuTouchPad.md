# xSwipe
xSwipe is multitouch gesture recognizer. This script make your linux PC able to recognize swipes like a Macbook.

## Get xSwipe
```bash
$ git clone https://github.com/zouyapeng/xSwipe.git
```

## Install X11::GUITest
```bash
$ sudo apt install libx11-guitest-perl
$ sudo cpan install Smart::Comments
```
###Ubuntu 14.04 或者更高版本
```bash
$ sudo apt install -y git build-essential libevdev-dev autoconf automake libmtdev-dev xorg-dev xutils-dev libtool
$ sudo apt remove -y xserver-xorg-input-synaptics
$ git clone https://github.com/Chosko/xserver-xorg-input-synaptics.git
$ cd xserver-xorg-input-synaptics
$ ./autogen.sh
$ ./configure --exec_prefix=/usr
$ make
$ sudo make install
```
## Enable SHMConfig
```bash
$ sudo mkdir -p /etc/X11/xorg.conf.d/
$ sudo vim /etc/X11/xorg.conf.d/50-synaptics.conf
```

```bash
Section "InputClass"
Identifier "evdev touchpad catchall"
Driver "synaptics"
MatchDevicePath "/dev/input/event*"
MatchIsTouchpad "on"
Option "Protocol" "event"
Option "SHMConfig" "on"
EndSection
```

# Run
```bash
$ perl xSwipe.pl
```

# 常用手势
  - 三指上下（切换工作区）[ps.建议工作区为横向4个]
  - 三次左右（浏览器切换tab）
  - 四指向上 （显示所以工作区）
  - 四指向下 （显示当前工作区的所有应用）
  - 四指左右 （将当前选中应用程序移动的上一个，或者下一个工作区）
  - 其他