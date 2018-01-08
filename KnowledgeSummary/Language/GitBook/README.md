# GitBook 语法
## 标题

使用标题有两种方法，第一种是使用 "#" 开头，第二种是打完文字后在下一行加上 "==" :
### 使用 "#"
```markdown
#第一层标题
##第二层标题
###第三层标题
####第四层标题
#####第五层标题
```

### 使用 "=="
```markdown
第一层标题
==
第二层标题
--
```

## 强调
在这边会有三种强调的方式

## 斜体，使用 "*" 或 "_" 将文字包起来
```markdown
*强调，这是斜体*
_强调，这也是斜体_
```

## 粗体，使用 "**" 或 "__" 将文字包起来
```markdown
**强调，这是粗体**
__强调，这也是粗体__
```

## 斜粗体，使用 "***" 或 "___" 将文字包起来
```markdown
***强调，这是斜粗体***
___强调，这也是斜粗体___
```

## 清单
### 数字清单，在前面使用 "数字. " 开头，在测试过程中发现数字清单只能到第二层，再细分下去排版会乱
```markdown
1. 这是数字清单
   1. 这是数字清单
   2. 这是数字清单
2. 这是数字清单
3. 这是数字清单
```

### 项目清单，在前面使用 "-" 或 "+" 开头，可以混用
```markdown
- 这是项目清单
  - 这是项目清单
  - 这是项目清单
    + 这是项目清单 
+ 这是项目清单
```

## 链接
在使用链接也有两种方法可以进行

### 类似目录的方法
```markdown
[zouyapeng-wiki](http://wiki.zouyapeng.com)
```

### 使用注释方式
```markdown
[zouyapeng-wiki][1]

[1]: http://wiki.zouyapeng.com
```

## 图片
插入图片的方法会跟前面 链接 很像，差別只在于最前面多了一个 "!" 符号，或是可使用 HTML 內嵌的方式进行

### 方法一
```markdown
![Image test](../images/test.jpg)
```

### 方法二
```markdown
![Image test][1]

[1]: ../images/test.jpg
```

### HTML内嵌
```html
<img src="../images/test.jpg" alt="Image test" width="240" height="180" border="10" />
```
## 代码
在代码也是有两种方式表示

### 8个空格
```markdown
       ls -al
```

### 使用```将代码抱起来
```markdown
```bash
ls -al
```

## 表格
表格使用 "|" 进行分割，再使用 "-" 表示出表格抬头
```markdown
name | id | code
- | - | -
gitbook | 1 | nodejs
wordpress | 2 | php
```

## 引言
使用 ">" 进行引言的标记，以 ">" 的数量介定属于第几层引言
```markdown
> 第一层引言
>> 第二层引言
>>> 第三层引言
>>>> 第四层引言
```
## 内嵌HTML
可以在 Markdown 中使用 HTML 语法來辅助展示的效果，例如局中、字体颜色、iframe 等
```markdown
这沒有居中
<center>这有居中</center>
<font color="red">红色</font>
```

## 水平线
使用连续3个 "-" 、 "_" 或是 "*" 进行标识 (中间可以放置相同的空白)

## 视频
使用 iframe 的方式將 Youtube 影片嵌进來
```html
<iframe width="560" height="315" src="//www.youtube.com/embed/SwrKzkRUlaw?hd=1&autoplay=1&loop=1&playlist=SwrKzkRUlaw" frameborder="0" allowfullscreen></iframe>
```