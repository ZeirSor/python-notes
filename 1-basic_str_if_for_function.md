<!-- TOC -->

- [1. 字符串格式化补充写法](#1-字符串格式化补充写法)
- [2. 输入](#2-输入)
- [3. 输出](#3-输出)
  - [3.1. 默认换行](#31-默认换行)
  - [3.2. 不换行`end = ''`](#32-不换行end--)
- [4. 判断补充(：)](#4-判断补充)
  - [4.1. 获取随机数](#41-获取随机数)
- [5. 循环语句（：）](#5-循环语句)
  - [5.1. `while`](#51-while)
  - [5.2. `for`](#52-for)
- [6. `range`语句](#6-range语句)
- [7. 函数](#7-函数)
  - [7.1. 函数参数](#71-函数参数)
    - [7.1.1. 位置参数](#711-位置参数)
    - [7.1.2. 默认参数](#712-默认参数)
    - [7.1.3. 可变参数](#713-可变参数)
    - [7.1.4. 关键字参数](#714-关键字参数)
    - [7.1.5. 命名关键字参数](#715-命名关键字参数)
  - [7.2. 对函数的参数和返回值进行指定类型和检查](#72-对函数的参数和返回值进行指定类型和检查)
  - [7.3. 函数说明文档](#73-函数说明文档)
  - [7.4. 有全局变量和局部变量](#74-有全局变量和局部变量)
    - [7.4.1. `global`关键字](#741-global关键字)
  - [7.5. 无返回值则类型为`None`](#75-无返回值则类型为none)

<!-- /TOC -->
## 1. 字符串格式化补充写法

`f"{str}"`

```python
name = 'zs'
age = '18'
id = '120211'

res = f"I am {name}, I am {age}, my id is {id}"
print(res)
```

## 2. 输入

`input("提示语句")`语句

```python
print(f"who are you : {input()}")
```

## 3. 输出
`print`
### 3.1. 默认换行
### 3.2. 不换行`end = ''`


## 4. 判断补充(：)

`elif`语句

### 4.1. 获取随机数

```python
import random
# 左开右闭
num = random.randint(1, 10)
```
## 5. 循环语句（：）
### 5.1. `while`
### 5.2. `for`
```python
for 临时变量 in 待处理数据集:
	执行代码
```
- 尽管是临时变量，跳出for循环后依然可以访问
- 从规范上来讲不建议访问
## 6. `range`语句
`range(num)`从0开始

`range(start, end)`左闭右开

`range(start, end, step)`步长

## 7. 函数

### 7.1. 函数参数

#### 7.1.1. 位置参数
普通，略
#### 7.1.2. 默认参数
`参数名=默认值`
```python
def add(x, y=3):
    return x + y

print(add(1))  # 4
print((add(1, 5)))  # 6
```
- 默认参数必须在最右端
- 定义默认参数时一定要使用**不可变对象**
#### 7.1.3. 可变参数
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

#### 7.1.4. 关键字参数
`**kw`
- 关键字参数则是以dict形式传递。 
- 关键字参数传递的是参数名:参数值键值对。
- 只能放在最右边的参数
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

#### 7.1.5. 命名关键字参数
`*`
- `*`后面的参数被视为命名关键字参数。
- 命名关键字参数必须传入参数名
```python
def personinfo(name, age, *, gender, city):  # 只能传递gender和city参数
    print(name, age, gender, city)

personinfo('Steve', 22, gender='male', city='shanghai')
# Steve 22 male shanghai
```

### 7.2. 对函数的参数和返回值进行指定类型和检查
```python
def my_add(x: int, y: int = 8) -> int:
    return x + y

print(my_add(1)) #9
help(my_add)
```


### 7.3. 函数说明文档

```python
def func(x, y):
	"""
	函数说明
	:param x: 参数x的说明
    :param y: 参数y的说明
    :return: 返回值的说明
	"""
```

### 7.4. 有全局变量和局部变量
#### 7.4.1. `global`关键字
- 函数体内修改全局变量，跳出函数体后失效
### 7.5. 无返回值则类型为`None`

