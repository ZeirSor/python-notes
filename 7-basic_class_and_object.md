# 类和对象
<!-- TOC -->

- [1. 类的基本语法](#1-类的基本语法)
    - [1.1. 创建对象](#11-创建对象)
    - [1.2. 成员方法](#12-成员方法)
    - [1.3. 内置方法](#13-内置方法)
        - [1.3.1. `__init__`构造方法](#131-__init__构造方法)
        - [1.3.2. `__del__` 方法](#132-__del__-方法)
        - [1.3.3. `__str__`字符串方法](#133-__str__字符串方法)
        - [1.3.4. `__lt__`小于/大于比较方法](#134-__lt__小于大于比较方法)
        - [1.3.5. `__le__`小于等于/大于等于比较方法](#135-__le__小于等于大于等于比较方法)
        - [1.3.6. `__eq__`等于比较方法](#136-__eq__等于比较方法)
        - [1.3.7. `MRO`方法搜索顺序](#137-mro方法搜索顺序)
- [2. 封装](#2-封装)
    - [2.1. 私有成员变量](#21-私有成员变量)
    - [2.2. 私有成员方法](#22-私有成员方法)
- [3. 继承](#3-继承)
    - [3.1. 单继承](#31-单继承)
    - [3.2. 多继承](#32-多继承)
    - [3.3. 复写父类成员变量和成员方法](#33-复写父类成员变量和成员方法)
- [4. 多态](#4-多态)
- [5. 抽象类（接口）](#5-抽象类接口)
- [6. 静态方法](#6-静态方法)
- [7. 单例设计模式](#7-单例设计模式)
    - [7.1. `__new__`方法](#71-__new__方法)
    - [7.2. 单例代码实现](#72-单例代码实现)
    - [7.3. 只执行一次初始化方法](#73-只执行一次初始化方法)
    - [7.4. 重写`__new__`方法](#74-重写__new__方法)
- [8. 新式类和旧式（经典）类](#8-新式类和旧式经典类)
    - [8.1. 新式类](#81-新式类)
    - [8.2. 旧式类](#82-旧式类)

<!-- /TOC -->
## 1. 类的基本语法

```python
class 类名:
    成员变量
    ...
    
    成员方法
    ...
```

### 1.1. 创建对象

```python
对象 = 类名称()
```

### 1.2. 成员方法

```python
def 方法名(self, 形参1, ..., 形参n):
    方法体
```

### 1.3. 内置方法
#### 1.3.1. `__init__`构造方法
```python
def __init__(self, ...)
```

-   对象初始化
-   定义实例属性

#### 1.3.2. `__del__` 方法

- 自动调用

#### 1.3.3. `__str__`字符串方法

#### 1.3.4. `__lt__`小于/大于比较方法

```python
def __lt__(self, other):
	return self.xxx < other.xxx
```

#### 1.3.5. `__le__`小于等于/大于等于比较方法
```python
def __lt__(self, other):
	return self.xxx <= other.xxx
```
#### 1.3.6. `__eq__`等于比较方法
```python
def __lt__(self, other):
	return self.xxx == other.xxx
```
- 默认比较内存地址
- 重写比较属性

#### 1.3.7. `MRO`方法搜索顺序

`类名.__mro__`输出元组

## 2. 封装
属性+方法
### 2.1. 私有成员变量
`__变量名`

- 私有成员只能内部访问


### 2.2. 私有成员方法
`__方法名`

## 3. 继承

### 3.1. 单继承
```python
class 类名(父类名):
	...
```

### 3.2. 多继承
- 先继承优先
```python
class 类名(父类名1, 父类名2, ..., 父类名n):
	...
```

### 3.3. 复写父类成员变量和成员方法
- `super`关键字

## 4. 多态

```python
def 函数名/方法名(变量名: 类名):
    变量名.方法
```

## 5. 抽象类（接口）

 ```python
 class 类名:
     def 方法名(self):
         pass
    	...
 ```

## 6. 静态方法

-   即不访问实例属性也不访问类属性
-   既不调用实例方法也不调用类方法

```python
    @staticmethod
    def add(a: int, b: int) -> int:
        return a + b
```

## 7. 单例设计模式

-   每次执行`类名()`返回的对象, 内存地址是相同的
-   目的: 让类创建对象时, 让系统中只有唯一的一个实例

### 7.1. `__new__`方法

-   为对象分配空间
-   返回对象引用
-   创建对象时会自动调用

### 7.2. 单例代码实现

```python
class ClassDemo:
    instance = None
    def __new__(cls, *args, **kwargs):
        if cls.instance is None:
            cls.instance = super().__new__(cls)
        return cls.instance

print(ClassDemo())  # <__main__.ClassDemo object at 0x0000021EFB1D1760>
print(ClassDemo())  # <__main__.ClassDemo object at 0x0000021EFB1D1760>
```

### 7.3. 只执行一次初始化方法

-   定义一个类属性标记
-   判断标记

```python
    init_flag = False
    def __init__(self):
        if ClassDemo.init_flag:
            return
        print("execute init method")
        ClassDemo.init_flag = True
```



### 7.4. 重写`__new__`方法

-   调用父类`__new__`方法
-   接收对象引用并返回（否则不会调用`__init__`方法！）

```python
    def __new__(cls, *args, **kwargs):
        print("创建对象, 分配空间")

        instance =  super().__new__(cls)
        
        return instance
```

## 8. 新式类和旧式（经典）类

### 8.1. 新式类

-   以`Object`为基类的类, 推荐使用

### 8.2. 旧式类

-   不以`Object`为基类的类, 不推荐使用

## 9. 反射

反射，提供了一种更加灵活的方式让你可以实现去 对象 中操作成员（以字符串的形式去 `对象` 中进行成员的操作）。

```python
class Person(object):
    
    def __init__(self,name,wx):
        self.name = name
        self.wx = wx
	
    def show(self):
        message = "姓名{}，微信：{}".format(self.name,self.wx)
        
        
user_object = Person("武沛齐","wupeiqi666")


# 对象.成员 的格式去获取数据
user_object.name
user_object.wx
user_object.show()

# 对象.成员 的格式无设置数据
user_object.name = "吴培期"
```

```python
user = Person("武沛齐","wupeiqi666")

# getattr 获取成员
getattr(user,"name") # user.name
getattr(user,"wx")   # user.wx


method = getattr(user,"show") # user.show
method()
# 或
getattr(user,"show")()

# setattr 设置成员
setattr(user, "name", "吴培期") # user.name = "吴培期"
```

Python中提供了4个内置函数来支持反射：

- getattr，去对象中获取成员

```
  v1 = getattr(对象,"成员名称")
  v2 = getattr(对象,"成员名称", 不存在时的默认值)
```

- setattr，去对象中设置成员

```
  setattr(对象,"成员名称",值)
```

- hasattr，对象中是否包含成员

```
  v1 = hasattr(对象,"成员名称") # True/False
```

- delattr，删除对象中的成员

```
  delattr(对象,"成员名称")
```

以后如果再遇到 对象.成员 这种编写方式时，均可以基于反射来实现。

案例：

```python
class Account(object):

    def login(self):
        pass

    def register(self):
        pass

    def index(self):
        pass

    
def run(self):
    name = input("请输入要执行的方法名称：") # index register login xx run ..
    
    account_object = Account()
    method = getattr(account_object, name,None) # index = getattr(account_object,"index")
    
    if not method:
        print("输入错误")
        return 
    method()
```

### 4.1 一些皆对象

在Python中有这么句话：`一切皆对象`。 每个对象的内部都有自己维护的成员。

- 对象是对象

```python
class Person(object):

    def __init__(self,name,wx):
        self.name = name
        self.wx = wx

        def show(self):
            message = "姓名{}，微信：{}".format(self.name,self.wx)


            user_object = Person("武沛齐","wupeiqi666")
            user_object.name
```

- 类是对象

```python
class Person(object):
    title = "武沛齐"

    Person.title
    # Person类也是一个对象（平时不这么称呼）
```

- 模块是对象

```python
import re

re.match
# re模块也是一个对象（平时不这么称呼）。
```


由于反射支持以字符串的形式去对象中操作成员【等价于 对象.成员 】，所以，基于反射也可以对类、模块中的成员进行操作。

简单粗暴：只要看到 xx.oo 都可以用反射实现。

```python
class Person(object):
    title = "武沛齐"

v1 = Person.title
print(v1)
v2 = getattr(Person,"title")
print(v2)
```

```python
import re

v1 = re.match("\w+","dfjksdufjksd")
print(v1)

func = getattr(re,"match")
v2 = func("\w+","dfjksdufjksd")
print(v2)
```

### 4.2 import_module + 反射

在Python中如果想要导入一个模块，可以通过import语法导入；企业也可以通过字符串的形式导入。

示例一：

```python
# 导入模块
import random

v1 = random.randint(1,100)
```

```python
# 导入模块
from importlib import import_module

m = import_module("random")

v1 = m.randint(1,100)
```

示例二：

```python
# 导入模块exceptions
from requests import exceptions as m
```

```python
# 导入模块exceptions
from importlib import import_module
m = import_module("requests.exceptions")
```

示例三：

```python
# 导入模块exceptions，获取exceptions中的InvalidURL类。
from requests.exceptions import InvalidURL
```

```python
# 错误方式
from importlib import import_module
m = import_module("requests.exceptions.InvalidURL") # 报错，import_module只能导入到模块级别。
```

```python
# 导入模块
from importlib import import_module
m = import_module("requests.exceptions")
# 去模块中获取类
cls = m.InvalidURL
```

在很多项目的源码中都会有 `import_module` 和 `getattr` 配合实现根据字符串的形式导入模块并获取成员，例如：

```python
from importlib import import_module

path = "openpyxl.utils.exceptions.InvalidFileException"

module_path,class_name = path.rsplit(".",maxsplit=1) # "openpyxl.utils.exceptions"   "InvalidFileException"

module_object = import_module(module_path)

cls = getattr(module_object,class_name)

print(cls)
```

我们在开发中也可以基于这个来进行开发，提高代码的可扩展性，例如：请在项目中实现一个发送 短信、微信 的功能。

参考示例代码中的：auto_message 项目。
