# 迭代器与生成器
<!-- TOC -->

- [1. 可迭代对象](#1-可迭代对象)
- [2. 迭代器](#2-迭代器)
- [3. 可迭代对象不一定是迭代器](#3-可迭代对象不一定是迭代器)
- [4. 将可迭代对象转换为迭代器](#4-将可迭代对象转换为迭代器)
- [5. 生成器](#5-生成器)

<!-- /TOC -->
## 1. 可迭代对象

-   可以直接作用于循环语句的对象

## 2. 迭代器

-   可被内置函数`next()`调用, 并不断返回下一个值的对象

## 3. 可迭代对象不一定是迭代器

-   判断方法: 使用内置函数`isinstance()`和`collections`模块

```python
from collections import Iterable
isinstance(myList, Iterable)
```

## 4. 将可迭代对象转换为迭代器

-   内置函数`iter()`

```python
myIterator = iter(myList)
print(next(myIterator))
print(next(myIterator))
print(next(myIterator))
```

## 5. 生成器

-   指生成一个新的迭代器的函数
-   用`yield`, 不用`return`
-   惰性计算, 非立刻计算

```python
def myGen():
    x = range(1, 11)
    for i in x:
        yield i + 2
        
for x in myGen():
    print(x, end=" ")
# 3 4 5 6 7 8 9 10 11 12
```

