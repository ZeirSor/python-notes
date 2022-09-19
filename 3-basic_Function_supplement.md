
<!-- TOC -->

- [1. 函数多返回值](#1-函数多返回值)
- [2. 函数参数](#2-函数参数)
  - [2.1. 位置参数](#21-位置参数)
  - [2.2. 默认(缺省)参数](#22-默认缺省参数)
  - [2.3. 可变参数](#23-可变参数)
  - [2.4. 关键字参数](#24-关键字参数)
  - [2.5. 命名关键字参数](#25-命名关键字参数)
  - [2.6. 不定长参数](#26-不定长参数)
    - [2.6.1. 位置传递](#261-位置传递)
    - [2.6.2. 关键字传递](#262-关键字传递)
- [3. 类型注解: 对函数的参数和返回值进行指定类型和检查](#3-类型注解-对函数的参数和返回值进行指定类型和检查)
  - [3.1. 变量类型注解格式](#31-变量类型注解格式)
    - [3.1.1. 基础容器类型注解](#311-基础容器类型注解)
    - [3.1.2. `tuple、dict`详细注解](#312-tupledict详细注解)
  - [3.2. 函数（方法）类型注解](#32-函数方法类型注解)
  - [3.3. `Union`类型](#33-union类型)
- [4. `lambda`匿名函数](#4-lambda匿名函数)
  - [4.1. 格式: `lambda 传入参数: 函数体(一行代码)`](#41-格式-lambda-传入参数-函数体一行代码)
  - [4.2. 调用方法](#42-调用方法)
    - [4.2.1. 变量接收](#421-变量接收)
    - [4.2.2. (lambda)(parameter)](#422-lambdaparameter)
    - [4.2.3. 作参数](#423-作参数)
    - [4.2.4. 作返回值](#424-作返回值)
- [5. 过滤函数 `filter(function, iterable)`](#5-过滤函数-filterfunction-iterable)
- [6. 映射函数`map(function, iterable)`](#6-映射函数mapfunction-iterable)

<!-- /TOC -->

## 1. 函数多返回值

```python
def multiple_return_values():
    return 1, 'ZeirSor', True, [1, 2, 3]

x, y, z, w = multiple_return_values()
```

## 2. 函数参数

### 2.1. 位置参数
普通，略
### 2.2. 默认(缺省)参数
`参数名=默认值`
```python
def add(x, y=3):
    return x + y

print(add(1))  # 4
print((add(1, 5)))  # 6
```
- 默认参数必须在最右端
- 定义默认参数时一定要使用**不可变对象**
### 2.3. 可变参数
`*参数`
- 方便进行参数个数未知时的调用。
- 可变参数将以`tuple`形式传递。
- 只能放在最右边的参数
```python
list_example = {1, 2, 3, 4, 5}

def get_sum(*num):
    sum = 0
    for x in num:
        sum += x
    return sum

print(get_sum(1, 2, 3))  # 6
print(get_sum(*list_example))  # 15
```

### 2.4. 关键字参数
`**kw`
- 关键字参数则是以dict形式传递。 
- 关键字参数传递的是参数名:参数值键值对。
- 只能放在最右边的参数
- 关键字参数可以不用一一对应,指定即可
```python
def personinfo(name, age, **kw):
    print('name:', name, 'age:', age, 'ps:', kw)

personinfo('Steve', 22)
personinfo('Lily', 23, city='Shanghai')
personinfo('Leo', 23, gender='male', city='Shanghai')
# name: Steve age: 22 ps: {}
# name: Lily age: 23 ps: {'city': 'Shanghai'}
# name: Leo age: 23 ps: {'gender': 'male', 'city': 'Shanghai'}
```

### 2.5. 命名关键字参数
`*`

- `*`后面的参数被视为命名关键字参数。
- 命名关键字参数必须传入参数名
```python
def personinfo(name, age, *, gender, city):  # 只能传递gender和city参数
    print(name, age, gender, city)

personinfo('Steve', 22, gender='male', city='shanghai')
# Steve 22 male shanghai
```

### 2.6. 不定长参数

#### 2.6.1. 位置传递
- `args`收集参数,合并为元组

```python
def variable_length_parameter_position(*args):
    print(args)

variable_length_parameter_position(1, 2, 3, 4, 'sda', [2, 3, 4])
# (1, 2, 3, 4, 'sda', [2, 3, 4])
```

#### 2.6.2. 关键字传递
- 键=值
```python
def variable_length_parameter_keys(**kwargs):
    print(kwargs)

variable_length_parameter_keys(wo=5, ni=6, ta=7)
# {'wo': 5, 'ni': 6, 'ta': 7}
```

## 3. 类型注解: 对函数的参数和返回值进行指定类型和检查

### 3.1. 变量类型注解格式

`变量: 类型`

`变量 ... 		# type: ...`

#### 3.1.1. 基础容器类型注解

`变量名: 类型 = ...`

#### 3.1.2. `tuple、dict`详细注解

`变量名: 类型[类型, 类型, (...), ...] = ...`

### 3.2. 函数（方法）类型注解

```python
def 函数方法名(形参: 类型, ..., 形参: 类型) -> 返回值类型:
    ...
```

```python
def my_add(x: int, y: int = 8) -> int:
    return x + y

print(my_add(1)) #9
help(my_add)
```

### 3.3. `Union`类型
```python
from typing import Union

# Union[类型, 类型, ..., 类型]

my_list: list[Union[str, int]] = [1, 2, "str1", "str2"]

my_dict: dict[str, Union[str, int]] = {"name": "zhangsan", "age": 18}

# 函数注解也可...
```


## 4. `lambda`匿名函数
- 只能临时使用一次
### 4.1. 格式: `lambda 传入参数: 函数体(一行代码)`
- 只能写一行代码!

### 4.2. 调用方法

#### 4.2.1. 变量接收
```python
f = lambda x, y: x + y
print(f(2, 3)) # 5
```

#### 4.2.2. (lambda)(parameter)
```python
print((lambda x, y: x + y)(3, 4)) # 7
```

#### 4.2.3. 作参数
```python
my_list = ['wo si zs', 'a an i u y t', 'hui dss']
my_list.sort(key=lambda str: len(str.split()))
print(my_list)
# ['hui dss', 'wo si zs', 'a an i u y t']
```

#### 4.2.4. 作返回值
```python
def f(a, b, c):
    return lambda x: a * x ** 2 + b * x + c

g = f(2, 2, 1)

print(g(3))  # 25
```

## 5. 过滤函数 `filter(function, iterable)`

- `function`: 提供过滤规则的函数
- `iterable`: 可迭代对象

```python
def func(x):
    return x > 5

data = [4, 6, 7, 2, 9, 8, 0, 1, 11, 45, 2]
filtered = filter(func, data)
filtered_data = list(filtered)
print(filtered_data)
# [6, 7, 9, 8, 11, 45]
```

`lambda表达式写法`

```python
print(list(filter(lambda x: x > 5, [4, 6, 7, 2, 9, 8, 0, 1, 11, 45, 2])))
```

## 6. 映射函数`map(function, iterable)`

- `function`: 提供规则的函数对象
- `iterable`: 可迭代对象

```python
def func(x):
    return x * 2

data = [4, 6, 7, 2, 9, 8, 0, 1, 11, 45, 2]
mapped = map(func, data)
mapped_data = list(mapped)
print(mapped_data)
# [8, 12, 14, 4, 18, 16, 0, 2, 22, 90, 4]
```

`lambda表达式写法`

```python
print(list(map(lambda x: x * 2, [4, 6, 7, 2, 9, 8, 0, 1, 11, 45, 2])))

```