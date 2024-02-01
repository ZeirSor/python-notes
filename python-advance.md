# python进阶技巧

## 筛选数据

### 列表筛选

```python
from random import randint

l = [randint(-10, 10) for _ in range(10)]

# 方法1: 使用列表推导式
result_1 = [_ for _ in l if _ >= 0]

# 方法2: 使用filter函数和lambda表达式
g = filter(lambda x: x >= 0, l)
result_2 = list(g)
```

### 字典筛选

```python
# 生成包含学生分数的字典
d = {f'student{i}': randint(50, 100) for i in range(1, 20)}

# 方法3: 使用字典推导式筛选分数大于等于90的学生
result_3 = {k: v for k, v in d.items() if v >= 90}

# 方法4: 使用filter函数和lambda表达式筛选分数大于等于90的学生，然后转为列表和字典
g = filter(lambda item: item[1] >= 90, d.items())
result_4_list = list(g)
result_4_dict = dict(result_4_list)
```

这些代码示例展示了使用列表推导式、filter函数以及字典推导式对数据进行筛选的方法。

-   在列表的情况下，可以使用列表推导式或filter函数；
-   而在字典的情况下，可以使用字典推导式或filter函数转为列表和字典的形式。



## 元组命名提高可读性

### 1. 使用常量表示索引

```python
NAME = 0
AGE = 1
SEX = 2
EMAIL = 3
```
这种方式通过常量的方式为元组的每个位置进行命名，提高了代码的可读性，但容易出错，因为没有直接将元组的结构体现出来。

### 2. 使用解构赋值

```python
NAME, AGE, SEX, EMAIL = range(4)
```
通过使用解构赋值，将每个元素分别赋值给对应的变量，使得代码更加清晰易懂，但对于大型的元组可能显得冗长。

### 3. 使用枚举

```python
from enum import IntEnum

class StudentEnum(IntEnum):
    NAME = 0
    AGE = 1
    SEX = 2
    EMAIL = 3
    
s = ('jim', 16, 'male', 'jim8721@gmail.com')
s[StudentEnum.NAME]
isinstance(StudentEnum.NAME, int) # True
```
使用枚举为元组的每个位置进行命名，枚举成员具有整数值，可以通过成员名访问，提高了可读性和代码的健壮性。

### 4. 使用命名元组

```python
from collections import namedtuple

Student =  namedtuple('Student', ['name', 'age', 'sex', 'email'])
s2 = Student('jim', 16, 'male', 'jim8721@gmail.com')
s2[0]  # 使用索引
s2.name  # 使用属性名
```
通过使用`namedtuple`创建命名元组，可以通过索引或属性名来访问元组的元素，提高了可读性和代码的简洁性。

总体而言，使用枚举或命名元组是更推荐的方式，因为它们提供了更好的可读性和代码健壮性。

### `namedtuple`

>   `namedtuple`是Python标准库中`collections`模块提供的一个工厂函数，用于创建具有命名字段的元组。这可以使得元组更易读、易用，并且能够通过字段名来访问元组的元素。以下是`namedtuple`的基本用法和示例：
>
>   ### 基本用法
>
>   ```python
>   from collections import namedtuple
>   
>   # 定义一个命名元组类型
>   Person = namedtuple('Person', ['name', 'age', 'gender'])
>   
>   # 创建命名元组的实例
>   person1 = Person(name='Alice', age=25, gender='female')
>   
>   # 访问命名元组的元素
>   print(person1.name)   # 输出: Alice
>   print(person1.age)    # 输出: 25
>   print(person1.gender) # 输出: female
>   ```
>
>   ### 使用位置参数创建
>
>   ```python
>   # 也可以使用位置参数创建命名元组的实例
>   person2 = Person('Bob', 30, 'male')
>   
>   # 访问命名元组的元素
>   print(person2.name)   # 输出: Bob
>   print(person2.age)    # 输出: 30
>   print(person2.gender) # 输出: male
>   ```
>
>   ### 特性和方法
>
>   - **_fields属性**: 返回所有字段名的元组。
>
>   ```python
>   print(Person._fields)  # 输出: ('name', 'age', 'gender')
>   ```
>
>   - **_make(iterable)**方法: 从可迭代对象创建一个命名元组的实例。
>
>   ```python
>   data = ['Charlie', 22, 'male']
>   person3 = Person._make(data)
>   print(person3)  # 输出: Person(name='Charlie', age=22, gender='male')
>   ```
>
>   - **_asdict()**方法: 将命名元组转换为字典。
>
>   ```python
>   person_dict = person1._asdict()
>   print(person_dict)
>   # 输出: {'name': 'Alice', 'age': 25, 'gender': 'female'}
>   ```
>
>   - **_replace()**方法: 替换命名元组的字段值并返回一个新的实例。
>
>   ```python
>   person_modified = person1._replace(age=26)
>   print(person_modified)
>   # 输出: Person(name='Alice', age=26, gender='female')
>   ```
>
>   `namedtuple`是一个非常方便的工具，尤其适用于需要一些结构化的数据，而又希望保持元组的轻量性和不可变性的场景。

## 根据字典值大小对项排序

### 1. 使用内置的`sorted`函数

```python
from random import randint

# 创建一个字典
d = {k: randint(60, 100) for k in 'abcdefgh'}

# 将字典项转为元组列表，按值降序排序
sorted_list_1 = sorted([(v, k) for k, v in d.items()], reverse=True)
```

### 2. 使用`zip`和`sorted`函数

```python
# 将字典值和键分别组成两个元组，再排序
sorted_list_2 = sorted(list(zip(d.values(), d.keys())))
```

### 3. 传递`sorted`函数的`key`参数

```python
# 按字典值排序，并保留原始次序
p = sorted(d.items(), key=lambda item: item[1], reverse=True)

# 使用enumerate为每个项添加次序
enumerated_list = list(enumerate(p, start=1))
```

### 4. 更新字典，添加次序

#### 方法 1：使用循环

```python
for i, (k, v) in enumerate(p, start=1):
    d[k] = (i, v)
    print(i, k, v)
```

#### 方法 2：使用字典推导式

```python
# 使用字典推导式更新字典，添加次序
updated_dict = {k: (i, v) for i, (k, v) in enumerate(p, start=1)}
```

以上代码演示了如何根据字典值的大小对字典项进行排序，并添加次序信息到原始字典。选择方法取决于你的需求和喜好。

### `zip`

在Python中，`zip`是一个内建函数，用于将多个可迭代对象打包成一个元组构成的新可迭代对象。具体来说，`zip`接受一系列可迭代对象作为参数，然后返回一个元组的迭代器，其中的每个元组包含了输入可迭代对象中相同位置的元素。以下是`zip`的基本用法和示例：

#### 基本用法

```python
# 创建几个可迭代对象
names = ['Alice', 'Bob', 'Charlie']
ages = [25, 30, 22]
scores = [95, 85, 90]

# 使用zip将它们打包成元组的迭代器
zipped_data = zip(names, ages, scores)

# 遍历打包后的数据
for item in zipped_data:
    print(item)
# 输出:
# ('Alice', 25, 95)
# ('Bob', 30, 85)
# ('Charlie', 22, 90)
```

#### 处理不等长的可迭代对象

如果传递给`zip`的可迭代对象的长度不一致，`zip`会以最短的可迭代对象为准，多余的部分将被忽略。

```python
names = ['Alice', 'Bob', 'Charlie']
ages = [25, 30]
zipped_data = zip(names, ages)

for item in zipped_data:
    print(item)
# 输出:
# ('Alice', 25)
# ('Bob', 30)
```

#### 解压缩

`zip`还可以用于解压缩，即将已经打包的可迭代对象拆分回原始的可迭代对象：

```python
# 已经打包的可迭代对象
zipped_data = [('Alice', 25), ('Bob', 30), ('Charlie', 22)]

# 使用zip解压缩
unzipped_names, unzipped_ages = zip(*zipped_data)

print(unzipped_names)  # 输出: ('Alice', 'Bob', 'Charlie')
print(unzipped_ages)   # 输出: (25, 30, 22)
```

`zip`是一个非常灵活和实用的工具，特别适用于同时迭代多个可迭代对象的场景。

### `*`运算

在Python中，`*`运算符有多个用途，取决于它的上下文。以下是`*`运算符的几种常见用法：

#### 1. 解包（Unpacking）

在函数调用或列表、元组等可迭代对象中，`*`可以用于解包。

##### 函数调用中的解包：

```python
def add_numbers(a, b, c):
    return a + b + c

numbers = [1, 2, 3]

result = add_numbers(*numbers)
print(result)  # 输出: 6
```

在函数调用时，`*`可以用来将列表或元组等可迭代对象解包为独立的参数传递给函数。

##### 列表解析中的解包：

```python
list_of_lists = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

flattened_list = [num for sublist in list_of_lists for num in sublist]
print(flattened_list)  # 输出: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

在列表解析中，`*`可以用来解包嵌套的可迭代对象。

#### 2. 扩展迭代（Extended Iterable Unpacking）

`*`还可以用于扩展迭代，即在迭代中接受不定数量的元素。

```python
first, *rest = [1, 2, 3, 4, 5]

print(first)  # 输出: 1
print(rest)   # 输出: [2, 3, 4, 5]
```

这里`*rest`表示将列表中的剩余元素打包为一个列表。

#### 3. 剩余参数（Arbitrary Argument Lists）

`*`也可以在函数定义中用于接收任意数量的位置参数。

```python
def sum_all(*args):
    return sum(args)

result = sum_all(1, 2, 3, 4, 5)
print(result)  # 输出: 15
```

在这个例子中，`*args`表示接受任意数量的位置参数，并将它们打包为一个元组。

#### 4. 关键字参数的解包

`**`可以用于解包关键字参数。

```python
def display_info(**info):
    for key, value in info.items():
        print(f"{key}: {value}")

user_info = {'name': 'Alice', 'age': 25, 'gender': 'female'}

display_info(**user_info)
# 输出:
# name: Alice
# age: 25
# gender: female
```

这里`**user_info`表示将字典的键值对解包为关键字参数。

总体而言，`*`在Python中具有很多灵活的用法，包括解包、扩展迭代、剩余参数等，使得代码更具表达力和灵活性。

### `生成器表达式`

生成器表达式是一种Python语法结构，用于创建生成器对象。它类似于列表推导式，但使用圆括号括起来，以生成一个迭代器而不是立即创建一个完整的列表。

生成器表达式的语法如下：

```python
(expression for item in iterable)
```

其中，`expression` 是对每个 `item` 的计算表达式，`item` 是从 `iterable` 中逐个取出的元素。

-   生成器表达式的工作方式是，每次请求下一个元素时，它会根据表达式计算并生成该元素，**而不会一次性生成所有元素。**
-   这种逐个生成的方式使得生成器表达式在处理大型数据集或需要逐个处理结果的场景中更加高效，因为它可以**节省内存并支持惰性计算**。

生成器表达式可以直接用于迭代，也可以作为参数传递给需要迭代器的函数或方法。它们与生成器函数（通过 `yield` 语句生成值的函数）具有相似的行为，但生成器表达式更为简洁，适合于简单的迭代场景。

下面是一个生成器表达式的示例，用于生成一个包含平方数的生成器对象：

```python
squares = (x ** 2 for x in range(1, 6))

for num in squares:
    print(num)
```

这个生成器表达式 `(x ** 2 for x in range(1, 6))` 会逐个生成 1 到 5 的平方数。在 `for` 循环中，我们可以按需迭代生成器对象，并打印每个生成的平方数。

总结而言，生成器表达式是一种创建生成器对象的简洁语法，它可以逐个生成结果，节省内存并支持惰性计算。它在处理大型数据集或需要逐个处理结果的场景中非常有用。

## 统计序列中元素的频度

### 方法 1: 使用字典统计

```python
from random import randint

data = [randint(0, 20) for _ in range(30)]

# 初始化字典，将每个元素的初始频度设为0
dic = dict.fromkeys(data, 0)

# 遍历序列，统计每个元素的频度
for x in data:
    dic[x] += 1

# 排序字典项，取前三个最频繁的元素
sorted_result_1 = sorted([(v, k) for k, v in dic.items()], reverse=True)[:3]
```

### 方法 2: 使用堆

```python
import heapq

# 使用堆获取前三个最频繁的元素
sorted_result_2 = heapq.nlargest(3, ((v, k) for k, v in dic.items()))
```

### 方法 3: 使用`collections`的`Counter`对象

```python
from collections import Counter

# 使用Counter对象统计元素频度
c = Counter(data)

# 获取前三个最频繁的元素及其频度
sorted_result_3 = c.most_common(3)
```

这三种方法分别使用了手动统计字典、堆和`Counter`对象来实现元素频度的统计。其中，`Counter`对象是专门为计数而设计的，它提供了简洁的接口，并且能够直接返回最常见的元素。根据实际需求，你可以选择最适合你的方法。

## 快速找到多个字典的公共键

### 方法 1: 使用循环和条件判断

```python
d1 = {k: randint(1, 4) for k in sample('abcdefgh', randint(3, 6))}
d2 = {k: randint(1, 4) for k in sample('abcdefgh', randint(3, 6))}
d3 = {k: randint(1, 4) for k in sample('abcdefgh', randint(3, 6))}

common_keys_1 = [k for k in d1 if k in d2 and k in d3]
print(common_keys_1)
```

### 方法 2: 使用列表推导式和all函数

```python
dl = [d1, d2, d3]
common_keys_2 = [k for k in dl[0] if all(map(lambda d: k in d, dl[1:]))]
print(common_keys_2)
```

### 方法 3: 使用集合的交集

```python
from functools import reduce

dl = [d1, d2, d3]
common_keys_3 = reduce(lambda a, b: a & b, map(dict.keys, dl))
print(list(common_keys_3))
```

这三种方法都是有效的，但方法3使用了集合的交集操作，可以更简洁地找到多个字典的公共键。根据实际需求和个人喜好，可以选择最适合的方法。

### `map`

`map()` 是 Python 内置函数之一，它用于对可迭代对象的每个元素应用一个指定的函数，返回一个迭代器（在 Python 3 中是一个迭代器对象，在 Python 2 中是一个列表）。

`map()` 的基本语法如下：

```python
map(function, iterable, ...)
```

- `function`: 对每个元素执行的函数。
- `iterable`: 一个或多个可迭代对象，可以是列表、元组等。

`map()` 将指定函数应用于每个可迭代对象的对应元素，返回一个包含结果的迭代器。如果传递了多个可迭代对象，`map()` 会以并行的方式对每个可迭代对象的元素进行处理。

以下是一个简单的示例，将一个列表中的每个元素都平方：

```python
numbers = [1, 2, 3, 4, 5]
squared_numbers = map(lambda x: x**2, numbers)
print(list(squared_numbers))
# 输出: [1, 4, 9, 16, 25]
```

在上述示例中，`map()` 使用了匿名函数（lambda）来计算每个元素的平方，并返回一个包含平方值的迭代器。

`map()` 函数在很多情况下都可以提高代码的简洁性和可读性，尤其是需要对可迭代对象的每个元素应用相同操作时。

### `all`

`all()` 是 Python 内置函数之一，用于判断可迭代对象中的所有元素是否都为真（True）。如果可迭代对象的所有元素都为真，则 `all()` 返回 `True`；如果可迭代对象中存在至少一个元素为假，则 `all()` 返回 `False`。

`all()` 的基本语法如下：

```python
all(iterable)
```

- `iterable`: 可迭代对象，例如列表、元组、集合等。

以下是一些示例：

-   示例 1：所有元素为真

```python
numbers = [2, 4, 6, 8, 10]
result = all(x % 2 == 0 for x in numbers)
print(result)
# 输出: True
```

-   示例 2：存在一个元素为假

```python
numbers = [2, 4, 6, 8, 9]
result = all(x % 2 == 0 for x in numbers)
print(result)
# 输出: False
```

-   示例 3：空列表

```python
empty_list = []
result = all(empty_list)
print(result)
# 输出: True
```

在示例 3 中，对空列表应用 `all()` 函数会返回 `True`。这是因为对于空列表，"所有元素都为真" 的定义是 "没有元素为假"。

`all()` 在某些场景中非常有用，例如在需要判断所有条件是否都满足时，或者在需要检查所有元素是否为真时。

### `reduce`

`reduce()` 是 Python 内置函数之一，它用于对可迭代对象中的元素进行累积操作，从而将序列归约为单个值。需要注意的是，在 Python 3 中，`reduce()` 函数被移至 `functools` 模块中。

`reduce()` 的基本语法如下：

```python
functools.reduce(function, iterable[, initializer])
```

- `function`: 用于累积的函数，它接受两个参数，即累积结果和下一个元素。
- `iterable`: 可迭代对象，例如列表、元组等。
- `initializer`: 可选参数，表示累积的初始值，如果提供了这个参数，`reduce()` 将从初始值开始进行累积。

以下是一个简单的示例，使用 `reduce()` 计算阶乘：

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

factorial = reduce(lambda x, y: x * y, numbers)
print(factorial)
# 输出: 120
```

在上述示例中，`reduce()` 使用了匿名函数（lambda）对列表中的元素进行累积，计算了 5 的阶乘。

以下是另一个示例，使用 `reduce()` 查找列表中的最大值：

```python
from functools import reduce

numbers = [4, 8, 1, 5, 10]

max_value = reduce(lambda x, y: x if x > y else y, numbers)
print(max_value)
# 输出: 10
```

`reduce()` 在某些情况下可以提高代码的简洁性，特别是在需要对可迭代对象中的元素进行累积操作时。

你的代码演示了使用 `OrderedDict` 来保持字典有序，并通过 `islice` 函数进行切片操作。以下是对你的代码的简要总结：

## 使用 `OrderedDict` 保持有序字典

```python
from collections import OrderedDict

od = OrderedDict()
od['c'] = 1
od['b'] = 2
od['a'] = 3

ordered_keys = list(od.keys())
print(ordered_keys)
# 输出: ['c', 'b', 'a']
```

在这个示例中，`OrderedDict` 保持了键的插入顺序。

## 使用 `islice` 进行字典切片

```python
from itertools import islice

# 示例1：对范围进行切片
sliced_range = list(islice(range(10), 3, 6))
print(sliced_range)
# 输出: [3, 4, 5]

# 示例2：对有序字典进行切片查询
def query_by_order(od, a, b=None):
    a -= 1
    if b is None:
        b = a + 1
    return list(islice(od, a, b))

od_result = query_by_order(od, 2, 3)
print(od_result)
# 输出: ['b']
```

`islice` 函数用于对可迭代对象进行切片操作。在示例2中，`query_by_order` 函数接受一个有序字典和两个参数 a 和 b，然后使用 `islice` 对有序字典进行切片查询。

这种方式可以在有序字典中灵活地进行切片查询，保持了字典的有序性。

## 双端队列：历史记录

`deque`，全称为“双向队列”（double-ended queue），是 Python 标准库 `collections` 模块中的一种数据类型。`deque` 是一个具有队列和栈的性质，支持从队列两端高效地添加和删除元素。相比于列表（list），`deque` 在头部和尾部的操作上更加高效，尤其是在大量数据的情况下。

### `deque` 的基本特点：

1. **双向操作：** `deque` 支持从两端高效地添加和删除元素，因此可以被用作队列（先进先出）或栈（先进后出）。

2. **固定长度：** 可以为 `deque` 指定一个最大长度，当 `deque` 达到最大长度时，新的元素添加会导致最老的元素被移除，保持了固定长度。

### `deque` 的基本用法：

```python
from collections import deque

# 创建一个空的deque
d = deque()

# 在右侧添加元素
d.append(1)
d.append(2)
d.append(3)

# 在左侧添加元素
d.appendleft(0)

# 移除右侧的元素
removed_item = d.pop()

# 移除左侧的元素
removed_item_left = d.popleft()

# 获取deque的长度
length = len(d)

# 打印deque
print(d)
```

-   使用 `deque` 实现历史记录

```python
from collections import deque
import random

# 生成一个 1 到 100 之间的随机数
random_number = random.randint(1, 100)

# 创建一个长度为5的deque，用于记录猜测历史
hq = deque([], 5)

while True:
    # 获取用户的猜测
    guess = input("猜一个 1 到 100 之间的整数：")

    if guess.isdigit():
        k = int(guess)
        hq.append(k)

        # 检查猜测是否正确
        if k == random_number:
            print("恭喜！猜对了！")
            break
        elif k < random_number:
            print("猜的数太小了，请再试一次。")
        else:
            print("猜的数太大了，请再试一次。")
    elif guess == "h?":
        print(list(hq))
```

-   使用 `deque` 实现循环队列

```python
from collections import deque

class CircularQueue:
    def __init__(self, capacity):
        self.capacity = capacity
        self.queue = deque(maxlen=capacity)

    def enqueue(self, item):
        self.queue.append(item)

    def dequeue(self):
        if len(self.queue) > 0:
            return self.queue.popleft()
        else:
            print("Queue is empty.")

    def display(self):
        print(list(self.queue))

# 创建循环队列，容量为3
cq = CircularQueue(3)

# 入队
cq.enqueue(1)
cq.enqueue(2)
cq.enqueue(3)

# 查看队列
cq.display()  # 输出: [1, 2, 3]

# 出队
cq.dequeue()

# 查看队列
cq.display()  # 输出: [2, 3]

# 入队
cq.enqueue(4)

# 查看队列
cq.display()  # 输出: [2, 3, 4]
```

在上述示例中，`CircularQueue` 类使用 `deque` 实现了一个循环队列，保持了固定长度，当队列满时，新的元素入队会导致最老的元素出队。这展示了 `deque` 的一个常见应用场景。
