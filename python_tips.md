# python 小技巧

## `print()函数`

[参考：【python小技巧1】一文讲尽print函数](https://www.bilibili.com/read/cv20889702/)

### `sep`参数

```python
print('hello world', 'Hello World', sep=' | ')
# hello world | Hello World
```

### `file` 参数

-   可以写入文件而不是打印到控制台

```python
import os
if not os.path.exists("test_pro"):
    os.mkdir('test_pro')
with open('test_pro/print_test.txt', 'w') as f:
    print("hello world", file=f)
```

### 🔺 进度条的打印

```python
import time
n = 100
for i in range(n + 1):
    print("\rProgress Bar:[{}{}] {}%".format('■' * i, '□' * (n - i) , int(i / n * 100)), end='')
    time.sleep(0.01)
# Progress Bar:[■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■] 100%
```

## `*`和`/`的妙用

[参考：【python小技巧2】星号(*)和斜杠(/)的妙用](https://www.bilibili.com/read/cv20929134/)

### 乘法从左向右，乘方从右向左

```python
def f1():
    print(3 * 2)            # 6
    print(3 ** 2)           # 9
    print(2 * 2 ** 2 ** 3)  # 2 * 2 ** 8 = 2 * 256 = 512
```

### `pow()`函数

```python
def f2():
    # pow 的速度比较快，数大的时候用
    # x ** y        <==> pow(x, y)
    # x ** y % z    <==> pow(x, y, z)
    def f21():
        6 ** 6 ** 6 % 66
    def f22():
        pow(6, pow(6, 6), 66)

    print(timeit.timeit(f21, number=100))
    print(timeit.timeit(f22, number=100))
    # 0.0854716
    # 8.659999999999224e-05
```

### 函数传参

-   `/`前只能使用位置传参
-   `*`后只能使用关键字传参

```python
def f3(a, /, b, *, c):
    print(a)
    print(b)
    print(c)
    
f3(1, 2, c=3)
# 1
# 2
# 3
```

### 打包和拆包

-   `*args`将一个序列展开

```python
def add(x, y):
    return x + y

arr = (4, 5)
print(add(arr[0], arr[1]))
print(add(*arr))
```

-   `**kwargs`将一个字典以键值对的形式展开

```python
dic = {'x': 4, 'y': 5}
print(add(x=dic['x'], y=dic['y']))
print(add(**dic))
print(*dic)
```

-   打包

```python
def f4():
    a = (1, 2, 3, 4)
    b = (5, 6, 7, 8)
    print(a + b)
    print((*a, *b))

    x = {'a': 1, 'b': 2}
    y = {'c':3, 'd': 4}
    print({**x, **y})
```

### 接收想要的值

```python
def f5():
    a, *_, c = (1, 2, 3, 4, 5, 6, 7, 8)
    print(a, _, c, sep=' | ')
    # 1 | [2, 3, 4, 5, 6, 7] | 8
    a, _, c = [1, 2, 3]
    print(a, c, sep=' | ')
    # 1 | 3
    a, *_= [1, 2, 3]
    print(a)    # 1
    *_, c = [1, 2, 3]
    print(c)    # 3
```

### 真除和假除

```python
def f6():
    print(11 / 2)	# 5.5
    print(11// 2)	# 5
```

## `else`用法

[参考：【python小技巧3】else的用法](https://www.bilibili.com/read/cv20925057/)

### 三目运算符

```python
cond = True

def f1():
    # print(1)
    return 1

def f2():
    # print(2)
    return 2

def f3():
    res = f1() if cond else f2()    # 1
    print(3) if cond else print(4)

f3()
```

### `for/while else`

循环自然结束时执行`else`里面的代码

### `try - except - else`

```python
try:
  ...
except 某些异常 as e:
  ...
...
else:
  ...
finally:
```

没遇到异常才会执行`else`
`finally`在`python`层面必然执行，就算前面有`return`也会执行

-   例如`os._exit()`是C层面的事情，此时`finally`就不会执行

```python
def f6():
    try:
        exit()
        # <==> raise SystemExit
    except Exception:
        # except Exception 这样就不会打印 after
        # 如果只是except 会捕捉一切异常 会打印出except和after
        print('except')
    finally:
        print('finally')
    print('after')
f6()
```

```python
import os
def f7():
    try:
        os._exit(0)
    except Exception:
        print('except')
    finally:
        print('finally')
f7()
# finally 无效
```

## `for`循环和迭代

-   可迭代对象：实现了`__iter__`方法
-   迭代器：实现了`__next__`方法
-   迭代器必须是可迭代的：实现了`__next__`必然实现了`__iter__`
-   判断是否为迭代器or可迭代对象

```python
from collections.abc import Iterable, Iterator
isinstance(obj, Iterable)
isinstance(obj, Iterator) 
```

### 自己实现可迭代对象和迭代器

-   定义迭代器类对象

```python
class Range:
    def __init__(self, start, end, step=1):
        assert step > 0  # 简单起见，我们只处理步长 > 0 的情况
        self.start = start
        self.end = end
        self.step = step

    def __iter__(self):
        return RangeIterator(self.start, self.end, self.step)  # 返回迭代器


class RangeIterator:
    def __init__(self, num, end, step):
        self.num = num
        self.end = end
        self.step = step

    def __next__(self):
        if self.num < self.end:    # 还可以继续迭代
            output = self.num
            self.num += self.step  # 增长步长
            return output          # 返回值
        else:                      # 迭代到头了就触发 StopIteration
            raise StopIteration
    def __iter__(self):
        return self 
```

-   使用生成器`yield`

```python
class Range:
    def __init__(self, start, end, step=1):
        assert step > 0  # 简单起见，我们只处理步长 > 0 的情况
        self.start = start
        self.end = end
        self.step = step

    def __iter__(self):
        n = self.start
        while n < self.end:
            yield n
            n += self.step 
```

