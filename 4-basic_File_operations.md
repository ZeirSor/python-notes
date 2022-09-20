# 文件操作

<!-- TOC -->

- [1. 打开文件](#1-打开文件)
- [2. 读取文件](#2-读取文件)
  - [2.1. `FileObject.read(num)`](#21-fileobjectreadnum)
  - [2.2. `FileObject.readlines() -> list`](#22-fileobjectreadlines---list)
  - [2.3. `FileObject.readline()` 一行一行读取](#23-fileobjectreadline-一行一行读取)
  - [2.4. `for`循环读取文件](#24-for循环读取文件)
- [3. 关闭文件](#3-关闭文件)
- [4. `with open`语法](#4-with-open语法)
- [5. 文件写入](#5-文件写入)
- [6. 内容刷新](#6-内容刷新)

<!-- /TOC -->

## 1. 打开文件


`FileObject.open(name, mode, encoding)`

- `name`: 文件名的字符串/路径
- `mode`: 设置打开文件的模式: 只读(r)、写入(w)、追加(a)等
- `encoding`: 编码格式(常用UTF-8)

## 2. 读取文件

### 2.1. `FileObject.read(num)`

### 2.2. `FileObject.readlines() -> list` 

### 2.3. `FileObject.readline()` 一行一行读取

- 文件读取的时候文件对象有一个指针

### 2.4. `for`循环读取文件

```python
for line in open("test.txt", "r", encoding="UTF-8"):
    print(line)
```

## 3. 关闭文件
`FileObject.close()`

## 4. `with open`语法

- 可以再操作完成后自动关闭文件

```python
with open(name, mode, encoding) as FileObject:
	for line in FileObject:
		print(line)
```

- 统计子串次数

```python
f = open("test.txt", "r", encoding="UTF-8")
content = f.read() # str
count = content.count(sub_str)
print(count)
f.close()
```

```python
f = open("test.txt", "r", encoding="UTF-8")
count = 0
for line in f:
    line = line.strip(" \n , 、")  # 去除首尾空格和换行符
    words = line.split(" ")  # 按空格分割
    for word in words:
        if word == sub_str:
            count += 1
print(count)
f.close()
```

## 5. 文件写入
`FileObject.write()`
- 写入缓冲区, 要记得刷新
- 如果是`mode='w'`会覆盖原有内容
- `mode='a'`追加内容
## 6. 内容刷新
`FileObject.flush()`



