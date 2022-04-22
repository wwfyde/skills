# Python最佳实践



[软件工程](软件工程.md)





# 实现配置容器的几种方式

> 实现配置对象的几种方式
>
> 实现配置文件的几种方式

## ConfigManager

> 配置管理器



## 多配置读取

> 实现一种机制, 优先从文件,等地方读取

## 数据库对象

> 数据字典的形式

## 文件

### `ini`文件中

### `json`文件中

### `yaml`文件中 推荐



## python对象

> 存在于python对象中, 通过机制修改Python对象中的值:
>
> 涉及到几种场景: 
>
> 暂时修改
>
> 运行时有效
>
> 持久化修改

### 变量对象

> 直接存放于模块中

### 字典对象

### 元组对象

### 列表对象



## 内存对象

### 运行时对象

### redis对象

## 环境变量

> 动态的值, 会影响系统运行状态的值, 在系统运行开始时到结束前(运行时)有效.
>
> 对于不同的运行时来讲, 环境变量的值可能是不同的. 环境变量可以被运行时进程读取和修改, 以影响程序的运行状态. 
>
> python环境变量会依赖于系统变量
>
> os依赖于sys
>
> 

```python
import os

# 获取系统环境变量
env = os.environ  # 返回一个字典
env = os.environb  # 字节串的字典

# 获取单个系统环境变量
value = os.getenv('name')

# 设置环境变量
env['key'] = value
os.environ['key'] = value
os.putenv('name', 'value')


```





# 代码组织技巧

> 代码逻辑结构

## 自上而下

> 先实现主干流程, 再实现枝叶流程
>
> 主流程, 子流程

```python
def main():
    data = read_input_file('data.csv')
    report = generate_report(data)
    write_report(report)

def write_report(report):
    pass

def generate_report(data):
    pass

def read_input_file(filename):
    pass

# Application entry point -> call main()
if __name__ == '__main__':
	main()
```





## 自下而上

> 先实现具体细节, 在组装成完整作品

```python
def read_input_file(filename):
    pass

def generate_report(data):
    pass

def write_report(report):
    pass
def main ()
	data = read_input_file('data.csv')
	report = generate_report(data)
	write_report(report)

# Application entry point -> call main()
if __name__ == '__main__':
	main()
```



# 面向对象核心思想

## 类的应用场景



# REST API最佳实践

# 错误处理

> except Exception

```python
# 获取错误类型
try:
    a = 5/0
except Excepttion as exc:
    print(f"{repr(exc)}")  # 使用repr函数
    print(f"{type(exc)}")  # 使用type
```

# 加密和签名