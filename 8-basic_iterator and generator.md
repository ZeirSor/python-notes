# 迭代器与生成器
<!-- TOC -->

- [1. 可迭代对象](#1-可迭代对象)
- [2. 迭代器](#2-迭代器)
- [3. 可迭代对象不一定是迭代器](#3-可迭代对象不一定是迭代器)
- [4. 将可迭代对象转换为迭代器](#4-将可迭代对象转换为迭代器)
- [5. 生成器](#5-生成器)

<!-- /TOC -->
## 1. 可迭代对象

-   `__iter__`中返回迭代器对象的

-   可以直接作用于循环语句的对象

## 2. 迭代器对象

-   `__iter__`中返回`self`的
-   有`__next__`

-   可被内置函数`next()`调用, 并不断返回下一个值的对象

## 3. 可迭代对象不一定是迭代器

-   判断方法: 使用内置函数`isinstance()`和`collections`模块

```python
from collections import Iterable, Iterator
isinstance(myList, Iterable)	# 判断是否为可迭代对象(依据:是否有__iter__bing)
isinstance(myList, Iterator)	# 判断是否为迭代器
```

## 4. 将可迭代对象转换为迭代器

-   调用`可迭代对象.__iter__`

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

## 6. **for...in...循环的本质**

-   `for item in Iterable `循环的本质
    -   先通过`iter()`函数获取可迭代对象`Iterable`的迭代器
    -   然后对获取到的迭代器不断调用`next()`方法来获取下一个值并将其赋值给`item`
    -   当遇到`StopIteration`的异常后循环结束。
