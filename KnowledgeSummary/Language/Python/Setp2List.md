## 常用方法
```python
for f, b in zip(foo, bar):
    print(f, b)
```
* 这种方法只能适用于foo和bar都不是很大的情况下，如果量比较大的使用zip将会产生大量的临时变量。
* 不过在python3里面zip返回就是一个迭代器。

## 更好的方法（迭代）
```python
import itertools
 
for f,b in itertools.izip(foo,bar):
    print(f,b)
for f,b in itertools.izip_longest(foo,bar):
    print(f,b)
```