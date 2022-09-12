# 数据容器

<!-- TOC -->

- [1. 列表 `list` `[]`](#1-列表-list-)
    - [1.1. 下标索引](#11-下标索引)
    - [1.2. 常用操作](#12-常用操作)
        - [1.2.1. 下标相关](#121-下标相关)
            - [1.2.1.1. `list.index(element)` 查找某元素下标](#1211-listindexelement-查找某元素下标)
            - [1.2.1.2. `list[index] = value`](#1212-listindex--value)
            - [1.2.1.3. `list[start:end:step]` 切片](#1213-liststartendstep-切片)
        - [1.2.2. 增删改](#122-增删改)
            - [1.2.2.1. `list.insert(index, element)`](#1221-listinsertindex-element)
            - [1.2.2.2. `list.append(element)` 追加单个元素到尾部](#1222-listappendelement-追加单个元素到尾部)
            - [1.2.2.3. `list.extend(other data containers)` 追加一批元素(两个列表的合并)](#1223-listextendother-data-containers-追加一批元素两个列表的合并)
            - [1.2.2.4. `del list[index]` 删除元素（通过下标）](#1224-del-listindex-删除元素通过下标)
            - [1.2.2.5. `element = list.pop[下标]` 删除元素（通过下标）](#1225-element--listpop下标-删除元素通过下标)
            - [1.2.2.6. `list.remove(element)` 删除元素（通过元素，删除第一个找到的）](#1226-listremoveelement-删除元素通过元素删除第一个找到的)
            - [1.2.2.7. `list.clear()`](#1227-listclear)
        - [1.2.3. `list.count(element)` 统计列表中某元素](#123-listcountelement-统计列表中某元素)
        - [1.2.4. `len(list)` 返回列表长度](#124-lenlist-返回列表长度)
        - [1.2.5. 排序](#125-排序)
            - [1.2.5.1. `list.sort(reverse=True/False)` 会改变原列表](#1251-listsortreversetruefalse-会改变原列表)
            - [1.2.5.2. `sorted(list, reverse=True/False)` 不会改变原列表](#1252-sortedlist-reversetruefalse-不会改变原列表)
        - [1.2.6. `new_lsit = list.copy()`](#126-new_lsit--listcopy)
        - [1.2.7. `list.reverse()`](#127-listreverse)
    - [1.3. 列表解析](#13-列表解析)
        - [1.3.1. `expression for iter_val in iterable`](#131-expression-for-iter_val-in-iterable)
        - [1.3.2. `expression for iter_val in iterable if cond_expr`](#132-expression-for-iter_val-in-iterable-if-cond_expr)
    - [1.4. 列表特点](#14-列表特点)
- [2. 元组 `tuple` `()`](#2-元组-tuple-)
    - [2.1. 赋值注意](#21-赋值注意)
    - [2.2. 常用操作](#22-常用操作)
        - [2.2.1. `tuple.index(element)`](#221-tupleindexelement)
        - [2.2.2. `tuple.count()`](#222-tuplecount)
        - [2.2.3. `len(tuple)`](#223-lentuple)
        - [2.2.4. `max(tuple)`](#224-maxtuple)
        - [2.2.5. `min(tuple)`](#225-mintuple)
        - [2.2.6. `sum(tuple)`](#226-sumtuple)
        - [2.2.7. `tuple(list)` 将列表转换为元组](#227-tuplelist-将列表转换为元组)
        - [2.2.8. `del tuple`](#228-del-tuple)
        - [2.2.9. 合并直接加](#229-合并直接加)
    - [2.3. 元组特点](#23-元组特点)
- [3. 字符串 `str`](#3-字符串-str)
    - [3.1. 常用操作](#31-常用操作)
        - [3.1.1. `str.index(element)`](#311-strindexelement)
        - [3.1.2. `str.replace(str_in_str, new_str)`](#312-strreplacestr_in_str-new_str)
        - [3.1.3. `str.split(split_flag) -> list` 字符串分割](#313-strsplitsplit_flag---list-字符串分割)
        - [3.1.4. `str.strip()` 字符串的规整，去前后控制](#314-strstrip-字符串的规整去前后控制)
        - [3.1.5. `str.count(sub_str)`](#315-strcountsub_str)
        - [3.1.6. `len(str)`](#316-lenstr)
    - [3.2. 字符串特点](#32-字符串特点)
- [4. 序列的切片操作](#4-序列的切片操作)
- [5. 集合 `set` `{}`](#5-集合-set-)
    - [5.1. 常用操作](#51-常用操作)
        - [5.1.1. `set.add(element)`](#511-setaddelement)
        - [5.1.2. `set.remove(element)`](#512-setremoveelement)
        - [5.1.3. `set.pop(element) -> type(element)`](#513-setpopelement---typeelement)
        - [5.1.4. `set.clear()`](#514-setclear)
        - [5.1.5. `set_3 = set_1.difference(set_2)` 取差集](#515-set_3--set_1differenceset_2-取差集)
        - [5.1.6. ` set_1.difference_update(set_2)` 消除差集](#516--set_1difference_updateset_2-消除差集)
        - [5.1.7. `set_3 = set_1.union(set_2)` 合并](#517-set_3--set_1unionset_2-合并)
        - [5.1.8. `len(set)`](#518-lenset)
    - [5.2. 集合特点](#52-集合特点)
- [6. 字典 `dict` `{}`](#6-字典-dict-)
    - [6.1. 常用操作](#61-常用操作)
        - [6.1.1. 增加/更新/获取](#611-增加更新获取)
            - [6.1.1.1. `dict[key] = value` 更新/增加](#6111-dictkey--value-更新增加)
            - [6.1.1.2. `dict.setDefault(key, default=None)` 添加元素](#6112-dictsetdefaultkey-defaultnone-添加元素)
            - [6.1.1.3. `value = dict[key]` 获取键值](#6113-value--dictkey-获取键值)
            - [6.1.1.4. `value = dict.get(key)`获取键值](#6114-value--dictgetkey获取键值)
            - [6.1.1.5. `dict_1.update(dict_1)` 更新或增加](#6115-dict_1updatedict_1-更新或增加)
        - [6.1.2. 删除](#612-删除)
            - [6.1.2.1. `dict.pop(key) -> value`](#6121-dictpopkey---value)
            - [6.1.2.2. `del[dict[key]]`](#6122-deldictkey)
            - [6.1.2.3. `key, value = dict.popitems()`](#6123-key-value--dictpopitems)
        - [6.1.3. `dict.keys()` 获取全部的key](#613-dictkeys-获取全部的key)
        - [6.1.4. `values = dict.values()`获取全部的value](#614-values--dictvalues获取全部的value)
        - [6.1.5. `len(dict)`](#615-lendict)
        - [6.1.6. `dict.clear()` 清空](#616-dictclear-清空)
        - [6.1.7. `new_dict = dict.copy()` 深拷贝](#617-new_dict--dictcopy-深拷贝)
        - [6.1.8. 遍历](#618-遍历)
            - [6.1.8.1. 方式一](#6181-方式一)
            - [6.1.8.2. 方式二](#6182-方式二)
            - [6.1.8.3. 方式三](#6183-方式三)
        - [6.1.9. `new_dict = dict.fromkeys(list[])` 生成空键值字典](#619-new_dict--dictfromkeyslist-生成空键值字典)
    - [6.2. 字典特点](#62-字典特点)
- [7. 数据容器总结](#7-数据容器总结)
    - [7.1. 对比](#71-对比)
    - [7.2. 通用操作](#72-通用操作)
        - [7.2.1. `for`循环遍历](#721-for循环遍历)
        - [7.2.2. `max()`](#722-max)
        - [7.2.3. `min()`](#723-min)
        - [7.2.4. `len()`](#724-len)
        - [7.2.5. 转换](#725-转换)
            - [7.2.5.1. `list()`](#7251-list)
            - [7.2.5.2. `tuple()`](#7252-tuple)
            - [7.2.5.3. `str()`](#7253-str)
            - [7.2.5.4. `set()`](#7254-set)
        - [7.2.6. `sorted(序列, [reverse=True])`](#726-sorted序列-reversetrue)

<!-- /TOC -->

## 1. 列表 `list` `[]`

### 1.1. 下标索引 

`列表[下表索引]`
- 0  --> + : 从头开始
- -1 --> -x: 反向索引

### 1.2. 常用操作

#### 1.2.1. 下标相关

##### 1.2.1.1. `list.index(element)` 查找某元素下标

##### 1.2.1.2. `list[index] = value`

##### 1.2.1.3. `list[start:end:step]` 切片

#### 1.2.2. 增删改

##### 1.2.2.1. `list.insert(index, element)`

##### 1.2.2.2. `list.append(element)` 追加单个元素到尾部

##### 1.2.2.3. `list.extend(other data containers)` 追加一批元素(两个列表的合并)

```python
my_list = [1, 2, 3]
my_list.extend([2, 3, 4])
print(my_list) # [1, 2, 3, 2, 3, 4]
```

##### 1.2.2.4. `del list[index]` 删除元素（通过下标）

##### 1.2.2.5. `element = list.pop[下标]` 删除元素（通过下标）

```python
my_list = [1, 2, 3, 2, 3, 4]
del my_list[3]
e = my_list.pop(1)
print(e) # 2
print(my_list) # [1, 3, 3, 4]
```

##### 1.2.2.6. `list.remove(element)` 删除元素（通过元素，删除第一个找到的）

```python
my_list = [1, 3, 3, 4]
my_list.remove(3)
print(my_list) # [1, 3, 4]
```

##### 1.2.2.7. `list.clear()`

```python
my_list.clear()
print(my_list) # []
```

#### 1.2.3. `list.count(element)` 统计列表中某元素

```python
my_list = [1, 3, 3, 4, 3, 2, 3]
print(my_list.count(3))  # 4
```

#### 1.2.4. `len(list)` 返回列表长度

```python
my_list = [1, 3, 3, 4, 3, 2, 3]
print(len(my_list))  # 7
```

#### 1.2.5. 排序

##### 1.2.5.1. `list.sort(reverse=True/False)` 会改变原列表

```python
my_list = [1, 3, 3, 4, 3, 2, 3]
my_list.sort()
print(my_list)  # [1, 2, 3, 3, 3, 3, 4]
my_list.sort(reverse=True)
print(my_list)  # [1, 2, 3, 3, 3, 3, 4]
```

##### 1.2.5.2. `sorted(list, reverse=True/False)` 不会改变原列表

```python
my_list = [1, 3, 3, 4, 3, 2, 3]
new_list = sorted(my_list)
print(my_list) # [1, 3, 3, 4, 3, 2, 3]
print(new_list) # [1, 2, 3, 3, 3, 3, 4]
```

#### 1.2.6. `new_lsit = list.copy()` 

#### 1.2.7. `list.reverse()` 

### 1.3. 列表解析

#### 1.3.1. `expression for iter_val in iterable`

#### 1.3.2. `expression for iter_val in iterable if cond_expr`

```python
my_list = [-1, 2, 4, -4, 2, -5, 8]
print([i ** 2 for i in my_list])  # [1, 4, 16, 16, 4, 25, 64]
print([i + 1 for i in my_list if abs(i) > 3])  # [5, -3, -4, 9] 
```

### 1.4. 列表特点
- 支持嵌套
- 元素类型无限制
- 可容纳不同类型的多个数据
- 有序存储
- 允许重复
- 可修改

## 2. 元组 `tuple` `()`

`tuple[index]`
### 2.1. 赋值注意

- 给元组赋一个值需要加上逗号，即 `my_tuple = (1,)`
- 省略小括号的元组，`x_1, x_2, ... = v_1, v_2, ...`

### 2.2. 常用操作

#### 2.2.1. `tuple.index(element)` 

#### 2.2.2. `tuple.count()`

#### 2.2.3. `len(tuple)`

#### 2.2.4. `max(tuple)`

#### 2.2.5. `min(tuple)`

#### 2.2.6. `sum(tuple)`

#### 2.2.7. `tuple(list)` 将列表转换为元组

#### 2.2.8. `del tuple`

#### 2.2.9. 合并直接加

### 2.3. 元组特点
- **不可修改**
- 支持嵌套 

## 3. 字符串 `str`

`字符串[下表索引]`
- 0  --> + : 从头开始
- -1 --> -x: 反向索引

### 3.1. 常用操作

#### 3.1.1. `str.index(element)`

#### 3.1.2. `str.replace(str_in_str, new_str)`

#### 3.1.3. `str.split(split_flag) -> list` 字符串分割, 返回列表

#### 3.1.4. `str.strip()` 字符串的规整，去前后空格、换行符

```python
my_str = '    zeir sor  '
print(my_str.strip())
# zeir sor

my_str = '213 zeir sor 123312 '
print(my_str.strip("123 "))# 去除前后字符
# zeir sor 
```

- 不会改变原字符串

#### 3.1.5. `str.count(sub_str)`

#### 3.1.6. `len(str)`

### 3.2. 字符串特点

- **无法修改**
- 只能存储字符串
- 支持下标索引
- 允许重复字符串
- 支持for

## 4. 序列的切片操作

- **对列表、元组、字符串**

`[start:end:step]`

`[::-1] <=> reverse`

## 5. 集合 `set` `{}`

### 5.1. 常用操作

#### 5.1.1. `set.add(element)`

#### 5.1.2. `set.remove(element)`

#### 5.1.3. `set.pop(element) -> type(element)` 

#### 5.1.4. `set.clear()`

#### 5.1.5. `set_3 = set_1.difference(set_2)` 取差集

#### 5.1.6. ` set_1.difference_update(set_2)` 消除差集

```python
set_1 = {1, 2, 3, 4, 5}
set_2 = {3, 4, 6, 7}
set_1.difference_update(set_2)
print(set_1, set_2) #{1, 2, 5} {3, 4, 6, 7}
```

#### 5.1.7. `set_3 = set_1.union(set_2)` 合并

```python
set_1 = {1, 2, 3, 4, 5}
set_2 = {3, 4, 6, 7}
set_3 = set_1.union(set_2)
print(set_3)  # {1, 2, 3, 4, 5, 6, 7}
```

#### 5.1.8. `len(set)`

### 5.2. 集合特点

- 混装
- 无序
- 不可重复
- 可修改
- 可`for`

## 6. 字典 `dict` `{}`

`{key: value, key: value, key: value, key: value, ...}`

### 6.1. 常用操作

#### 6.1.1. 增加/更新/获取

##### 6.1.1.1. `dict[key] = value` 更新/增加

##### 6.1.1.2. `dict.setDefault(key, default=None)` 添加元素

```python
my_dict = {"wo": 5, "ni": 6, "ta": 7}
my_dict.setdefault("TA", 8)
print(my_dict)  # {'wo': 5, 'ni': 6, 'ta': 7, 'TA': 8}
```
- 如果添加的是重复元素会失效

##### 6.1.1.3. `value = dict[key]` 获取键值

##### 6.1.1.4. `value = dict.get(key)`获取键值

##### 6.1.1.5. `dict_1.update(dict_1)` 更新或增加

- 若`dict_2`中和`dict_1`重复的则更新`dict_1`
- 否则增加

```python
my_dict_1 = {"wo": 5, "ni": 6, "ta": 7}
my_dict_2 = {"wo": 999, "Ni": 27, "ta": 7}
my_dict_1.update(my_dict_2)
print(my_dict_1) # {'wo': 999, 'ni': 6, 'ta': 7, 'Ni': 27}
```

#### 6.1.2. 删除

##### 6.1.2.1. `dict.pop(key) -> value`

##### 6.1.2.2. `del[dict[key]]`

##### 6.1.2.3. `key, value = dict.popitems()`

```python
my_dict = {"wo": 5, "ni": 6, "ta": 7}
new_dic = my_dict.popitem()
print(new_dic) # ('ta', 7)
print(my_dict) # {'wo': 5, 'ni': 6}
```

#### 6.1.3. `dict.keys()` 获取全部的key

```python
my_dict = {"wo": 5, "ni": 6, "ta": 7}
keys = my_dict.keys()
print(keys) # dict_keys(['wo', 'ni', 'ta'])
```

#### 6.1.4. `values = dict.values()`获取全部的value

```python
my_dict = {"wo": 5, "ni": 6, "ta": 7}
values = my_dict.values()
print(values) # dict_values([5, 6, 7])
```

#### 6.1.5. `len(dict)`

#### 6.1.6. `dict.clear()` 清空

#### 6.1.7. `new_dict = dict.copy()` 深拷贝

#### 6.1.8. 遍历

##### 6.1.8.1. 方式一

```python
for key in keys:
    print(f"{key}: {my_dict[key]}")
```

##### 6.1.8.2. 方式二

```python
for key in my_dict:
    print(f"{key}: {my_dict[key]}")
```

##### 6.1.8.3. 方式三

```python
my_dict = {"wo": 5, "ni": 6, "ta": 7}
for get_item in my_dict.items():
    print(get_item)
# ('wo', 5)
# ('ni', 6)
# ('ta', 7)
```

#### 6.1.9. `new_dict = dict.fromkeys(list[])` 生成空键值字典
- 对空字典操作
```python
new_dic = {}.fromkeys(["Wo", "Ni", "Ta", "TA"])
print(new_dic) # {'Wo': None, 'Ni': None, 'Ta': None, 'TA': None}
```

- 对非空字典会抹掉原来的键值对
```python
my_dict = {"wo": 5, "ni": 6, "ta": 7}
my_dict = my_dict.fromkeys(["Wo", "Ni", "Ta", "TA"])
print(my_dict) # {'Wo': None, 'Ni': None, 'Ta': None, 'TA': None}
```

### 6.2. 字典特点
- 不可重复
- 可嵌套

## 7. 数据容器总结

### 7.1. 对比

| 数据容器 |           列表           |           元组           |   字符串   |       集合       |            字典            |
| :------: | :----------------------: | :----------------------: | :--------: | :--------------: | :------------------------: |
|  标识符  |           [ ]            |           ( )            |    " "     |       { }        |        {key: value}        |
| 元素类型 |           任意           |           任意           |   仅字符   |       任意       |  key:除字典, value: 任意   |
| 下标索引 |            √             |            √             |     √      |        ×         |             ×              |
| 重复元素 |            √             |            √             |     √      |        ×         |             ×              |
| 可修改性 |            √             |            ×             |     ×      |        √         |             √              |
| 数据有序 |            √             |            √             |     √      |        ×         |             ×              |
| 使用场景 | \|可修改、可重复的数据\| | 不可修改、可重复的数据\| | 一串字符\| | 不可重复的数据\| | 以key值检索value的数据记录 |

### 7.2. 通用操作
#### 7.2.1. `for`循环遍历
#### 7.2.2. `max()`
#### 7.2.3. `min()`
#### 7.2.4. `len()`
#### 7.2.5. 转换
##### 7.2.5.1. `list()`
##### 7.2.5.2. `tuple()`
##### 7.2.5.3. `str()`
##### 7.2.5.4. `set()`
#### 7.2.6. `sorted(序列, [reverse=True])`