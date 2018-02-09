## 间隔固定时间执行
```python
#!/usr/bin/env python
 
import sched
import datetime
import time
 
INTERVAL = 10
scheduler = sched.scheduler(time.time, time.sleep)
 
 
def main_loop(sc):
    sc.enter(INTERVAL, 1, main_loop, (sc,))
    print datetime.datetime.now()
 
 
def main():
    scheduler.enter(INTERVAL, 1, main_loop, (scheduler,))
    scheduler.run()
 
 
if __name__ == '__main__':
    main()
```


## 每天指定时间执行
```python
#!/usr/bin/env python
 
import datetime
import time
 
def do_something():
    print datetime.datetime.now()
 
def main_loop():
    while True:
        tomorrow = datetime.datetime.replace(datetime.datetime.now() + datetime.timedelta(days=1),
                                             hour=2, minute=0,
                                             second=0, microsecond=0)
        delta = tomorrow - datetime.datetime.now()
        time.sleep(delta.seconds)
        do_something()
 
 
if __name__ == '__main__':
    main_loop()
```