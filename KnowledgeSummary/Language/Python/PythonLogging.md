## Simple usage
### 终端打印
```python
import logging
 
logging.warning('Watch out!') # will print a message to the console
logging.info('I told you so') # will not print anything
```
### 日志文件
```python
import logging
 
logging.basicConfig(filename='example.log', 
                    filemode='a', 
                    format='%(asctime)s - %(levelname)s - %(message)s', 
                    datefmt='%Y-%m-%d %H:%M:%S', 
                    level=logging.DEBUG)
logging.debug('This message should appear on the console')
logging.info('So should this')
logging.warning('And this, too')
```
### logging.basicConfig参数
```
filename: 指定日志文件名
filemode: 和file函数意义相同，指定日志文件的打开模式，'w'或'a'
format: 指定输出的格式和内容，format可以输出很多有用信息，如上例所示:
 %(levelno)s: 打印日志级别的数值
 %(levelname)s: 打印日志级别名称
 %(pathname)s: 打印当前执行程序的路径，其实就是sys.argv[0]
 %(filename)s: 打印当前执行程序名
 %(funcName)s: 打印日志的当前函数
 %(lineno)d: 打印日志的当前行号
 %(asctime)s: 打印日志的时间
 %(thread)d: 打印线程ID
 %(threadName)s: 打印线程名称
 %(process)d: 打印进程ID
 %(message)s: 打印日志信息
datefmt: 指定时间格式，同time.strftime()
level: 设置日志级别，默认为logging.WARNING
stream: 指定将日志的输出流，可以指定输出到sys.stderr,sys.stdout或者文件，默认输出到sys.stderr，当stream和filename同时指定时，stream被忽略
```

## Handler用法
### 日志主对象
```python
import logging
 
logging.basicConfig(level=logging.DEBUG,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S',
                    filename='myapp.log',
                    filemode='a')
 
#定义一个StreamHandler，将INFO级别或更高的日志信息打印到标准错误，并将其添加到当前的日志处理对象#
console = logging.StreamHandler()
console.setLevel(logging.INFO)
formatter = logging.Formatter('%(name)-12s: %(levelname)-8s %(message)s')
console.setFormatter(formatter)
logging.getLogger('').addHandler(console)
 
logging.debug('This message should appear on the console')
logging.info('So should this')
logging.warning('And this, too')
```
### 日志回滚
```python
import logging
from logging.handlers import RotatingFileHandler
 
#定义一个RotatingFileHandler，最多备份5个日志文件，每个日志文件最大10M
Rthandler = RotatingFileHandler('myapp.log', maxBytes=10*1024*1024,backupCount=5)
Rthandler.setLevel(logging.INFO)
formatter = logging.Formatter('%(name)-12s: %(levelname)-8s %(message)s')
Rthandler.setFormatter(formatter)
logging.getLogger('').addHandler(Rthandler)
 
logging.debug('This message should appear on the console')
logging.info('So should this')
logging.warning('And this, too')
```
### 其他Handler
```
logging.StreamHandler: 日志输出到流，可以是sys.stderr、sys.stdout或者文件
logging.FileHandler: 日志输出到文件
日志回滚方式，实际使用时用RotatingFileHandler和TimedRotatingFileHandler
logging.handlers.BaseRotatingHandler
logging.handlers.RotatingFileHandler
logging.handlers.TimedRotatingFileHandler
logging.handlers.SocketHandler: 远程输出日志到TCP/IP sockets
logging.handlers.DatagramHandler:  远程输出日志到UDP sockets
logging.handlers.SMTPHandler:  远程输出日志到邮件地址
logging.handlers.SysLogHandler: 日志输出到syslog
logging.handlers.NTEventLogHandler: 远程输出日志到Windows NT/2000/XP的事件日志
logging.handlers.MemoryHandler: 日志输出到内存中的制定buffer
logging.handlers.HTTPHandler: 通过"GET"或"POST"远程输出到HTTP服务器
```

## logging.config 配置文件管理日志
```
#logging.conf
###############################################
[loggers]
keys=root,example1,example2
 
[logger_root]
level=DEBUG
handlers=handler1,handler2
 
[logger_example1]
handlers=handler1,handler2
qualname=example1
propagate=0
 
[logger_example2]
handlers=handler3
qualname=example2
propagate=0
###############################################
[handlers]
keys=handler1,handler2,handler3
 
[handler_handler1]
class=StreamHandler
level=INFO
formatter=form2
args=(sys.stderr,)
 
[handler_handler2]
class=FileHandler
level=DEBUG
formatter=form1
args=('example.log', 'a')
 
[handler_handler3]
class=handlers.RotatingFileHandler
level=INFO
formatter=form2
args=('example.log', 'a', 10*1024*1024, 5)
###############################################
[formatters]
keys=form1,form2
 
[formatter_form1]
format=%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s
datefmt=%a, %d %b %Y %H:%M:%S
 
[formatter_form2]
format=%(name)-12s: %(levelname)-8s %(message)s
datefmt=
```
```python
import logging
import logging.config
 
logging.config.fileConfig("logger.conf")
logger = logging.getLogger("root")
# logger = logging.getLogger("example1")
# logger = logging.getLogger("example2")
 
logging.debug('This message should appear on the console')
logging.info('So should this')
logging.warning('And this, too')
```
