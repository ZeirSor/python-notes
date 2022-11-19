# 异常
<!-- TOC -->

- [1. What ?](#1-what-)
- [2. 捕获异常(异常处理)](#2-捕获异常异常处理)
	- [2.1. 捕获常规异常](#21-捕获常规异常)
	- [2.2. 捕获指定异常](#22-捕获指定异常)
	- [2.3. 捕获多个异常](#23-捕获多个异常)
	- [2.4. 捕获所有异常](#24-捕获所有异常)
	- [2.5. 异常的`else`](#25-异常的else)
	- [2.6. 异常的`finally`](#26-异常的finally)
- [3. 异常具有传递性](#3-异常具有传递性)

<!-- /TOC -->
## 1. What ?
- 程序运行过程中出现了错误

## 2. 捕获异常(异常处理)

- 对 BUG 进行提醒, 整个程序继续运行

### 2.1. 捕获常规异常
- **基本语法**

```python
try: 
	可能发生错误的代码
except:
	如果出现异常执行的代码
```
例如
```python
try:
	f = open("test.txt", "r", encoding="UTF-8")
except:
	f = open("test.txt", "w", encoding="UTF-8")
```

### 2.2. 捕获指定异常
```pyhton
try: 
	print(name)
except NameError as e:
	print("name 变量名称未定义错误")
```
### 2.3. 捕获多个异常
```pyhton
try: 
	print(name)
except (NameError, ZeroDivisionError, ...) as e:
	print("name 变量名称未定义错误")
```
### 2.4. 捕获所有异常
```python
try: 
	...
except Exception as e:
	...
	print(e)
```

### 2.5. 异常的`else`

```python
try: 
	...
except Exception as e:
	...
	print(e)
else:
	没有出现异常要执行的代码
```

### 2.6. 异常的`finally`
- 无论是否出现异常都要执行的代码
```pthon
try: 
	...
except Exception as e:
	...
	print(e)
else:
	没有出现异常要执行的代码
finally:
	...
	f.close()
```

-   `try`里面遇到`return` , 会先往下执行`finally`, 然后再执行`return`

## 3. 异常具有传递性

## 4. 抛出异常

`raise XXXexception()`

```python
def run(handler):
    try:
        num = handler()
        print(num)
        return "成功"
    except Exception as e:
        return "错误"
    finally:
        print("END")

        print("结束")


        res = run(lambda: 123) 
        print(res)
```

```python
>>> 123
>>> END
>>> 成功
```

```python
def func():
    print(666)
    return "成功"

def run(handler):
    try:
        num = handler()
        print(num)
        return func()
    except Exception as e:
        return "错误"
    finally:
        print("END")

        print("结束")


        res = run(lambda: 123) 
        print(res)
```

```python
>>> 123
>>> 666
>>> END
>>> 成功
```
