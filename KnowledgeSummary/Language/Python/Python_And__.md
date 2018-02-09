## Difference between _, __ and __xx__ in Python
### Example
```python
#!/usr/local/bin/python
#-*-coding:utf-8-*-
 
class A:
    def __init__(self):
        self.value = '1'
        self._value = '2'
        self.__value = '3'
 
    def method(self):
        try:
            print self.value, self._value, self.__value
        except Exception, error:
            print str(error)
 
    def _method(self):
        try:
            print self.value, self._value, self.__value
        except Exception, error:
            print str(error)
 
    def __method(self):
        try:
            print self.value, self._value, self.__value
        except Exception, error:
            print str(error)
 
 
class B(A):
    pass
 
if __name__ == '__main__':
    a = A()
    b = B()
    try:
        print a.value,a._value,a.__value
    except Exception,error:
        print str(error)
 
    a.method()
    a._method()
    try:
        a.__method()
    except Exception, error:
        print str(error)
 
    print dir(b)
```

#### Output
```bash
1 2 A instance has no attribute '__value'
1 2 3
1 2 3
A instance has no attribute '__method'
['_A__method', '_A__value', '__doc__', '__init__', '__module__', '_method', '_value', 'method', 'test', 'value']
编辑

```

### 单下划线开头
从上面的例子可见, 变量_value、方法_method() 与 value、method()其实没有区别。 

所以 _ 只是表明变量为私有, 外部类还是可以访问到这个变量

### 双下划线开头
标识一个方法或属性是私有的，但是其真正作用是用来避免子类覆盖其内容

### 双下划线开头结尾
当你看到"__xxxx__"的时，就知道不要调用它。为什么？ 因为它的意思是它是用于Python调用的, 比如__add__,__str__等等
```python
c = 1
print c + 1
print c.__add__(1)
```