## Example
```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import sys
import os
 
def daemon():
    """ A demo daemon main routine, write a datestamp to
        /tmp/daemon-log every 10 seconds.
    """
    import time
    f = open("/tmp/daemon-log", "w")
    while 1:
        f.write('%s\n' % time.ctime(time.time()))
        f.flush()
        time.sleep(10)
if __name__ == "__main__":
    # do the UNIX double-fork magic, see Stevens' "Advanced
    # Programming in the UNIX Environment" for details (ISBN 0201563177)
    try:
        pid = os.fork()
        if pid > 0:
            # exit first parent
            sys.exit(0)
    except OSError, e:
        print >>sys.stderr, "fork #1 failed: %d (%s)" % (e.errno, e.strerror)
        sys.exit(1)
    # decouple from parent environment
    os.chdir("/")
    os.setsid()
    os.umask(0)
    # do second fork
    try:
        pid = os.fork()
        if pid > 0:
            # exit from second parent, print eventual PID before
            print "Daemon PID %d" % pid
            sys.exit(0)
    except OSError, e:
        print >>sys.stderr, "fork #2 failed: %d (%s)" % (e.errno, e.strerror)
        sys.exit(1)
    # start the daemon main loop
    daemon()
编辑

```

## 说明
1. 运行后程序fork一个进程，如果fork成功则程序自己退出
2. 通过setsid() 创建了一个独立于当前会话的进程
3. 再一次fork一个进程，如果fork成功则当前程序退出
4. 这时候进程的父进程就变成了 init，成为了一个独立的deamon

## 装修器
```python
def daemon(func):
    """
    :param func:
    :return:
    """
    def _daemon():
        try:
            pid = os.fork()
            if pid > 0:
                sys.exit(0)
        except OSError, error:
            logging.error("Fork #1 failed: %s." % error.strerror)
            sys.exit(1)
 
        os.chdir('/')
        os.umask(0)
        os.setsid()
 
        try:
            pid = os.fork()
            if pid > 0:
                sys.exit(0)
        except OSError, error:
            logging.error("Fork #2 failed: %s." % error.strerror)
            sys.exit(1)
 
        pid = str(os.getpid())
        file("/var/run/instance_monitor.pid", 'w+').write("%s\n" % pid)
 
        func()
 
    return _daemon
```