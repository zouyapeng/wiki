## 使用python的10个良好习惯
### 1. Make a script both importable and executable
```python
def main():
    print('Doing stuff in module', __name__)
 
if __name__ == '__main__':
    print('Executed from the command line')
    main()
```

```bash
$ python mymodule.py
Executed from the command line
Doing stuff in module __main__


$ python
>>> import mymodule
>>> mymodule.main()
Doing stuff in module mymodule
```

### 2. Test for “truthy” and “falsy” values

* Checking for truth doesn't tie the conditional expression to the type of object being checked(检测对象真实不应该使用和对象类型相应的表达式)
* Checking for truth clearly shows the sxh's intention rather than drawing attention to a specific outcome(检测对象时应当清楚的表达代码的意向，而不是为了得到一个结果)

```python
name = 'Safe'
pets = ['Dog', 'Cat', 'Hamster']
owners = {'Safe': 'Cat', 'George': 'Dog'}

# Good
if name and pets and owners:
    print('We have pets!')

# Not so Good
if name != '' and len(pets) > 0 and owners != {}:
    print('We have pets!')
```

#### What is truth
True | False
- | -
Non-empty string | Empty string
Number not 0 | Number 0
Non-empty container: len(x) > 0 | Empty container: len(x) == 0
- | None
True | False
nonzero (2.x) / bool (3.x) | nonzero (2.x) / bool (3.x)

### 3. Use in where possible

* Using in to check if an item is in a sequence is clear and concise(用于检测元素在不在序列中显得意图明显且简洁)
* Can be used on lists, dicts (keys), sets, strings, and your own classes by implementing the contains special method(可以适用于多种数据类型，并且可以通过定义contains方法来适用于自定义类)

```python
# contains
name = 'Safe Hammad'
# Good
if 'H' in name:
    print('This name has an H in it!')
    
# Not So Good
if name.find('H') != -1:
    print('This name has an H in it!')
    
# iteration
pets = ['Dog', 'Cat', 'Hamster']
# Good 
for pet in pets:
    print('A', pet, 'can be very cute!')
    
# Not So Good
i = 0
while i < len(pets):
    print('A', pets[i], 'can be very cute!')
    i += 1
```


### 4. Swap values without temp variable

* Avoids polluting namespace with temp variable used only once(避免因为仅仅使用一次的temp变量污染命名空间)

```python
a, b = 5, 6
print(a, b) # 5, 6

# Good
a, b = b, a
print(a, b) # 6, 5

# Not So Good
temp = a
a = b
b = temp
print(a, b) # 6, 5
```

### 5. Build strings using sequence

* The join method called on a string and passed a list of strings takes linear time based on length of list(join()可以用于字符串和字符串的list，并且只使用一次方的遍历事件)
* Repeatedly appending to a string using '+' takes quadratic time!(使用 + 将会使用二次方的时间)

```python
chars = ['S', 'a', 'f', 'e']

# Good
name = ''.join(chars)

# Not So Good
name = ''
for char in chars:
    name += char
```

### 6. EAFP is preferable to LBYL
>It's <font color="red">E</font>asier to <font color="red">A</font>sk for <font color="red">F</font>orgiveness than <font color="red">P</font>ermission.

><font color="red">L</font>ook <font color="red">B</font>efore <font color="red">Y</font>ou <font color="red">L</font>eap.

>请求原谅比请求许可要简单的多，所以三思而后行。

* Throwing exceptions is not “expensive” in Python unlike e.g. Java(抛出异常并不像java这样的软件一样重)
* Rely on duck typing rather than checking for a specific type(尽量不要依赖数据的类型)

```python
# Good
d = {'x': '5'}
try:
    value = int(d['x'])
except (KeyError, TypeError, ValueError):
    value = None
    
# Not So Good
d = {'x': '5'}
if 'x' in d and \
   isinstance(d['x'], str) and \
   d['x'].isdigit():
    value = int(d['x'])
else:
    value = None
```

### 7. Enumerate

* Available since Python 2.3!
* Use the start parameter available since Python 2.6 to start at a number other than 0.
```python
names = ['Safe', 'George', 'Mildred']

# Good
for i, name in enumerate(names):
    print(i, name) # 0 Safe, 1 Georg
    
# Not So Good
count = 0
for name in names:
    print(i, name) # 0 Safe, 1 George etc.
    count += 1
```


### 8. Build lists using list comprehensions

* Very concise syntax(非常简洁的语法)
* Be careful it doesn't get out of hand (in which case the second formcan be clearer)(要小心不要脱离控制（部分情况下，第二种方法可能会更好一些)

```python
data = [7, 20, 3, 15, 11]

# Good
result = [i * 3 for i in data if i > 10]

# Not So Good
result = []
for i in data:
    if i > 10:
    result.append(i * 3)
```


### 9. Create dict from keys and values using zip

* There are several ways of constructing dicts!(其实有很多方法来创建一个字典)

```python
keys = ['Safe', 'Bob', 'Thomas']
values = ['Hammad', 'Builder', 'Engine']

# Good
d = dict(zip(keys, values))

# Not So Good
d = {}
for i, key in enumerate(keys):
    d[keys] = values[i]

```

### 10. And the rest ... !
* while True: break # This will spark discussion!!!
* Generators and generator expressions.
* Avoid from module import *
* Use _ for “throwaway” variables e.g.:
```python
for k, _ in [('a', 1), ('b', 2), ('c', 3)]:
    pass
```
* dict.get() and dict.setdefault()
* collections.defaultdict
* Sort lists using l.sort(key=key_func)


[原作者pdf](http://safehammad.com/downloads/python-idioms-2014-01-16.pdf)