# Python异步编程

> 异步编程实现的目标是 解决单线程阻塞的问题 来提升软件的性能 线程 是系统的最小调度单位 运行时是没办法(干预的)  
>
> 异步调用的关键点在于**分流**和**回调执行起点**。分流就是在当前代码位置，将一部分代码加入到条件达成后未来的回调执行流中，而另一部分代码则在当前程序流继续执行。回调执行起点通常为一个条件达成后来自操作系统的通知或者程序内部的消息(事件)。该事件会出发一个**回调执行起点方法**，去逆向执行回调流中的各个方法。 

> asyncio 是用来编写 **并发** 代码的库，使用 **async/await** 语法。适用于IO密集型网络编程， 处理高并发，弥补GIL不能发挥多核的优势

PEP 3156 是Python 3.4 中引入异步I/O框架asyncio 的一个提案，提供了基于协程做异步I/O编写单线程并发代码的基础设施。随后在PEP492 中引入了 async/await语法 以及 PEP380中的yield from 语法，自此，Python有了原生的协程支持，**不再依赖外部第三方库**。

## 重要语义

**同步(Sync)**: 完成事务的逻辑，先执行第一个事务，如果阻塞了，会一直等待，直到这个事务完成，再执行第二个事务，顺序执行

**异步(Async)**: 在处理调用这个事务的之后，不会等待这个事务的处理结果，直接处理第二个事务去了，通过状态、通知、回调来通知调用者处理结果。

## 参考文档

- [asyncio 异步I/O](https://docs.python.org/zh-cn/3/library/asyncio.html)
- [PEP3156：asyncio提案](https://www.python.org/dev/peps/pep-3156/)
- [PEP492：async/await](https://www.python.org/dev/peps/pep-0492/)
- [PEP380：yield from](https://www.python.org/dev/peps/pep-0380/)

参考引用

高层级 API

- [协程与任务](https://docs.python.org/zh-cn/3/library/asyncio-task.html)
- [流](https://docs.python.org/zh-cn/3/library/asyncio-stream.html)
- [Synchronization Primitives](https://docs.python.org/zh-cn/3/library/asyncio-sync.html)
- [子进程](https://docs.python.org/zh-cn/3/library/asyncio-subprocess.html)
- [队列集](https://docs.python.org/zh-cn/3/library/asyncio-queue.html)
- [异常](https://docs.python.org/zh-cn/3/library/asyncio-exceptions.html)

低层级 API

- [事件循环](https://docs.python.org/zh-cn/3/library/asyncio-eventloop.html)
- [期程](https://docs.python.org/zh-cn/3/library/asyncio-future.html)
- [传输和协议](https://docs.python.org/zh-cn/3/library/asyncio-protocol.html)
- [策略](https://docs.python.org/zh-cn/3/library/asyncio-policy.html)
- [平台支持](https://docs.python.org/zh-cn/3/library/asyncio-platforms.html)

指南与教程

- [高级API索引](https://docs.python.org/zh-cn/3/library/asyncio-api-index.html)
- [底层API目录](https://docs.python.org/zh-cn/3/library/asyncio-llapi-index.html)
- [用 asyncio 开发](https://docs.python.org/zh-cn/3/library/asyncio-dev.html)

## 作用

asyncio 被用作多个提供高性能 Python 异步框架的基础，包括网络和网站服务，数据库连接库，分布式任务队列等等。

asyncio 往往是构建 IO 密集型和高层级 **结构化** 网络代码的最佳选择。

asyncio 提供一组 **高层级** API 用于:

- 并发地 [运行 Python 协程](https://docs.python.org/zh-cn/3/library/asyncio-task.html#coroutine) 并对其执行过程实现完全控制;
- 执行 [网络 IO 和 IPC](https://docs.python.org/zh-cn/3/library/asyncio-stream.html#asyncio-streams);
- 控制 [子进程](https://docs.python.org/zh-cn/3/library/asyncio-subprocess.html#asyncio-subprocess);
- 通过 [队列](https://docs.python.org/zh-cn/3/library/asyncio-queue.html#asyncio-queues) 实现分布式任务;
- [同步](https://docs.python.org/zh-cn/3/library/asyncio-sync.html#asyncio-sync) 并发代码;

此外，还有一些 **低层级** API 以支持 *库和框架的开发者* 实现:

- 创建和管理 [事件循环](https://docs.python.org/zh-cn/3/library/asyncio-eventloop.html#asyncio-event-loop)，以提供异步 API 用于 [`网络化`](https://docs.python.org/zh-cn/3/library/asyncio-eventloop.html#asyncio.loop.create_server), 运行 [`子进程`](https://docs.python.org/zh-cn/3/library/asyncio-eventloop.html#asyncio.loop.subprocess_exec)，处理 [`OS 信号`](https://docs.python.org/zh-cn/3/library/asyncio-eventloop.html#asyncio.loop.add_signal_handler) 等等;
- 使用 [transports](https://docs.python.org/zh-cn/3/library/asyncio-protocol.html#asyncio-transports-protocols) 实现高效率协议;
- 通过 async/await 语法 [桥接](https://docs.python.org/zh-cn/3/library/asyncio-future.html#asyncio-futures) 基于回调的库和代码。

## 概念

### 协程 -- coroutine

协程通过 async/await 语法进行声明，是编写异步应用的推荐方式。例如，以下代码段 (需要 Python 3.7+) 打印 "hello"，等待 1 秒，然后打印 "world":

```python
import asyncio
async def main():
	print("hello")
	await asyncio.sleep(1)
	print("world!)
if `__name__` = '`__main__`':
	aysncio.run(main())
      
```

```
hello
world
```

**注意: **简单地调用一个协程并不会将其加入执行日程, 而是返回一个协程对象

```
>>> main()
<coroutine object main at 0x1053bb7c8>
```

要真正运行一个协程，asyncio 提供了**三种主要机制**:

- [`asyncio.run()`](https://docs.python.org/zh-cn/3/library/asyncio-task.html#asyncio.run) 函数用来运行最高层级的入口点 "main()" 函数
- 等待一个协程。以下代码段会在等待 1 秒后打印 "hello"，然后 *再次* 等待 2 秒后打印 "world":

```python
import asyncio
import time


async def say_after(delay: float, what):
    await asyncio.sleep(delay)
    print(what)


async def main():
    print(f"started at{time.strftime('%X')}")

    await say_after(1,'hello')  # 其实就是可阻塞对象
    await say_after(2,'world')

    print(f"finished at{time.strftime('%X')}")

# 单线程异步, 作为单线程在运行
if __name__ == '__main__':
    asyncio.run(main())

```

```
started at14:59:51
hello
world
finished at14:59:54
```

-  [`asyncio.create_task()`](https://docs.python.org/zh-cn/3/library/asyncio-task.html#asyncio.create_task) 函数用来并发运行作为 asyncio [`任务`](https://docs.python.org/zh-cn/3/library/asyncio-task.html#asyncio.Task) 的多个协程。
    让我们修改以上示例，*并发* 运行两个 `say_after` 协程:

```python
import asyncio
import time


async def say_after(delay: float, what):
    await asyncio.sleep(delay)
    print(what)


async def main():
    print(f"started at{time.strftime('%X')}")
    task1 = asyncio.create_task(say_after(1,'hello'))
    task2 = asyncio.create_task(say_after(2,'world'))

    await task1  # 其实就是可阻塞对象
    await task2

    print(f"finished at{time.strftime('%X')}")

# 单线程异步, 作为单线程在运行
if __name__ == '__main__':
    asyncio.run(main())

```

```
注意, 预期的输出显示代码段的运行时间比之前快了1秒
started at15:05:43
hello
world
finished at15:05:45
```

 

### 可等待对象

如果一个对象可以在 [`await`](https://docs.python.org/zh-cn/3/reference/expressions.html#await) 语句中使用，那么它就是 **可等待** 对象。许多 asyncio API 都被设计为接受可等待对象。

*可等待* 对象有三种主要类型: **协程**, **任务** 和 **Future**.

#### **协程**

Python 协程属于 **可等待** 对象，因此可以在其他协程中被等待:

```python
import asyncio


async def nested():
    return 42


async def main():
    # 如果我们仅仅是调用nested()什么都不会发生
    # 协程对象被创建但是不是可等待的
    # 因此它将不会运行
    nested()
    
    print(await nested())

asyncio.run(main())

```

**重要：**在本文档中 **协程** 可以来表示两个紧密相关的概念：

- *协程函数*: 定义形式为 [`async def`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#async-def) 的函数;
- *协程对象*: 调用 *协程函数* 所返回的对象。

asyncio 也支持旧式的 [基于生成器的](https://docs.python.org/zh-cn/3/library/asyncio-task.html#asyncio-generator-based-coro) 协程。

#### **任务**

*任务* 被用来设置日程(协程的子任务)以便 *并发* 执行协程。

当一个协程通过 [`asyncio.create_task()`](https://docs.python.org/zh-cn/3/library/asyncio-task.html#asyncio.create_task) 等函数被打包为一个 *任务*，该协程将自动排入日程准备立即运行:

```python
import asyncio


async def nested():
    # await asyncio.sleep(1)
    print('Ting')
    return 42


async def main():
    task = asyncio.create_task(nested())
    await task


asyncio.run(nested())

```

#### **Future 对象**

[`Future`](https://docs.python.org/zh-cn/3/library/asyncio-future.html#asyncio.Future) 是一种特殊的 **低层级** 可等待对象，表示一个异步操作的 **最终结果**。

当一个 Future 对象 *被等待*，这意味着协程将保持等待直到该 Future 对象在其他地方操作完毕。

在 asyncio 中需要 Future 对象以便允许通过 async/await 使用基于回调的代码。

通常情况下 **没有必要** 在应用层级的代码中创建 Future 对象。

Future 对象有时会由库和某些 asyncio API 暴露给用户，用作可等待对象:

```python
async def main():
    await function_that_returns_a_future_object()

    # this is also valid:
    await asyncio.gather(
        function_that_returns_a_future_object(),
        some_python_coroutine()
    )
```

一个很好的返回对象的低层级函数的示例是 [`loop.run_in_executor()`](https://docs.python.org/zh-cn/3/library/asyncio-eventloop.html#asyncio.loop.run_in_executor)。

### 异步 -- async

属性:关键字 

作用: 用async/await 语法对函数进行声明, 表示该函数为协程函数

概念: 

```python
async def func():
  pass
```



### 等待 -- await

### 异步IO -- asyncio

- 

## 用法

### [运行 asyncio 程序](https://docs.python.org/zh-cn/3/library/asyncio-task.html#id4)

`asyncio.run(coro, *, debug=False)`

此函数运行传入的协程，负责管理 asyncio 事件循环并 **完结异步生成器**。

当有其他 asyncio 事件循环在同一线程中运行时，此函数不能被调用。

如果 *debug* 为 `True`，事件循环将以调试模式运行。

此函数总是会创建一个新的事件循环并在结束时关闭之。它应当被用作 asyncio 程序的主入口点，理想情况下应当只被调用一次。

**重要:** 此函数是在 Python 3.7 中加入 asyncio 模块，处于 [暂定基准状态](https://docs.python.org/zh-cn/3/glossary.html#term-provisional-api)。

### [创建任务](https://docs.python.org/zh-cn/3/library/asyncio-task.html#id5)

`asyncio.create_task(coro)`

将 *coro* [协程](https://docs.python.org/zh-cn/3/library/asyncio-task.html#coroutine) 打包为一个 [`Task`](https://docs.python.org/zh-cn/3/library/asyncio-task.html#asyncio.Task) 排入日程准备执行。返回 Task 对象。

该任务会在 [`get_running_loop()`](https://docs.python.org/zh-cn/3/library/asyncio-eventloop.html#asyncio.get_running_loop) 返回的循环中执行，如果当前线程没有在运行的循环则会引发 [`RuntimeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#RuntimeError)。

```
async def coro():
	pass
task = asyncio.create_task(coro())
```

### [休眠](https://docs.python.org/zh-cn/3/library/asyncio-task.html#id6)

*coroutine* asyncio.sleep(*delay*, *result=None*, *, loop=None)

阻塞 *delay* 指定的秒数。

如果指定了 *result*，则当协程完成时将其返回给调用者。

**作用：**`sleep()` 总是会挂起当前任务，以允许其他任务运行。

*loop* 参数已弃用，计划在 Python 3.10 中移除。

以下协程示例运行 5 秒，每秒显示一次当前日期:

```python
import asyncio
import datetime

async def display_date():
    loop = asyncio.get_running_loop()
    end_time = loop.time() + 5.0
    while True:
        print(datetime.datetime.now())
        if (loop.time() + 1.0) >= end_time:
            break
        await asyncio.sleep(1)

asyncio.run(display_date())
```

### [并发运行任务](https://docs.python.org/zh-cn/3/library/asyncio-task.html#id7)

*awaitable* asyncio.gather(*aws, oop=None, return_exceptions=False)

*并发* 运行 *aws* 序列中的 [可等待对象](https://docs.python.org/zh-cn/3/library/asyncio-task.html#asyncio-awaitables)。

**如果 aws 中的某个可等待对象为协程，它将自动作为一个任务加入日程。**

如果所有可等待对象都成功完成，结果将是一个由所有返回值聚合而成的列表。结果值的顺序与 *aws* 中可等待对象的顺序一致。

如果 *return_exceptions* 为 `False` (默认)，所引发的首个异常会立即传播给等待 `gather()` 的任务。*aws* 序列中的其他可等待对象 **不会被取消** 并将继续运行。

如果 *return_exceptions* 为 `True`，异常会和成功的结果一样处理，并聚合至结果列表。

如果 `gather()` *被取消*，所有被提交 (尚未完成) 的可等待对象也会 *被取消*。

如果 *aws* 序列中的任一 Task 或 Future 对象 *被取消*，它将被当作引发了 [`CancelledError`](https://docs.python.org/zh-cn/3/library/asyncio-exceptions.html#asyncio.CancelledError) 一样处理 -- 在此情况下 `gather()` 调用 **不会**被取消。这是为了防止一个已提交的 Task/Future 被取消导致其他 Tasks/Future 也被取消。

在 3.7 版更改: 如果 *gather* 本身被取消，则无论 *return_exceptions* 取值为何，消息都会被传播。