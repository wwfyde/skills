# Go程序设计语言

> 参考文档
>
> 理论: <**Go程序设计语言**>	**官方文档**
>
> 实践:  **Go开发实战(极客时间)** 	**千锋Go语言**
>
> **尚硅谷** 
>
> 
>
> **参考官方文档结构**

## 重点概念

指针(pointer), go协程(go ), 接口, 结构, 包(package), 容器(container), 切片(slice)



goimports 



协程(goroutines) 

通道(channels) 

### 正交性

[引用链接](https://book.2cto.com/201304/21000.html)

程序设计语言的正交性意味着相对较小的基本结构集合，能够以较少的组合方式来构成语言的控制结构和数据结构。而且，基本结构的任一种可能组合都是合法且有意义的。例如数据类型，假设某语言有4种基本的数据类型(整型、单精度型、双精度型和字符型)和2种运算符(数组和指针)。如果2种运算符都能够作用于自身和4种基本的数据类型，就能够定义大量的数据结构。

一个语言特性是正交的，意味着它独立于程序中出现位置的上下文(“正交”来自于正交向量这一数学概念，正交向量相互独立)。正交性来源于基本结构间的对称关系。语言缺乏正交性将导致语言规则的特例。例如，在支持指针的程序设计语言中，应允许定义指针指向该语言定义的任何特定类型。但是，如果指针不允许指向数组，就无法定义许多潜在有用的用户自定义数据结构。

下面比较IBM大型机与VAX系列微型计算机的汇编语言的一个方面，来说明正交性在设计原理上的应用。考虑一个简单的情形：将两个内存或寄存器中的32位整数值相加，所得的和替换其中的一个值。IBM大型机用两条指令来实现这一操作，如

A Reg1, memory_cell

AR Reg1, Reg2

其中Regl和Reg2代表寄存器。指令的语义是

Reg1 ← contents(Reg1) + contents(memory_cell)

Reg1 ← contents(Reg1) + contents(Reg2)

在VAX中，32位整数值的加法指令是

ADDL operand_1, operand_2

其语义是

operand_2 ← contents(operand_1) + contents(operand_2)

其中，任一操作数都可以是寄存器或存储单元。

VAX的指令设计是正交的，因为一条指令既可以使用寄存器，也可以使用存储单元作为操作数。有两种方法指定操作数，而且能够以任意形式组合。IBM的设计不是正交的，在4种可能的操作数组合中，只有两种组合是合法的，而且这两种组合需要不同的指令A和AR。IBM的设计限制较多，因此可写性较差，例如，无法将两个值相加，并将结果存储在内存中。此外，由于上述限制以及额外的指令，IBM的设计学习起来也更难。

正交性与简单性直接相关：语言设计越正交，语言规则需要的特例就越少，特例越少意味着设计的规范程度越高，语言就越容易学习、[阅读](http://book.2cto.com/)和理解。任何学过大量英语的人可以证实，英语中的许多规则特例太难学了(例如，i总是在e前，除非在c后)。

作为高级语言中缺乏正交性的一个例子，考虑C语言中的以下规则和特例。虽然C语言有两种结构化的数据类型—数组与结构(struct)，但结构可从函数返回，而数组不行。结构的成员可以是除void和同样结构以外的任意数据类型，而数组元素可以是除void和函数以外的任意数据类型。函数参数是按值传递的，除非参数是数组，这时实际上是按引用传递的(因为在C程序中，不带下标的数组名会解释为数组第一个元素的地址)。

作为上下文相关的一个例子，考虑以下C语言的表达式：

a + b

这个表达式通常表示取出a和b的值并相加，但是如果a恰好是一个指针，则会影响b的值。例如，如果a指向一个占4字节的浮点值，那么b在与a相加之前，必须放大它的值—在这个例子中要乘以4。因此，a的类型会影响对b值的处理，即b的上下文会影响b的意义。

过多的正交也会产生问题。ALGOL 68语言(van Wijngaarden等，1969)可能是最具有正交性的程序设计语言了。ALGOL 68中的每一语言结构都有一个类型，这些类型没有任何限制，而且大多数结构都有值。这种自由组合可以产生极其复杂的结构，例如，只要结果是一个地址，就可以把条件语句、声明语句及其他各类语句一起放在赋值运算符的左边。这种极端的正交形式导致了不必要的复杂性。而且，由于语言需要大量的基本结构，高度的正交性将产生爆炸性的组合方式。因此，即使组合方式很简单，它们的整体数量也会导致语言的复杂性。

可见，语言的简单性至少部分归因于相对少量的基本结构的组合，以及正交原理的有限应用。

有人认为，函数式语言同时具有良好的简单性和正交性。函数式语言，如LISP，主要通过将函数作用于给定参数来执行计算。相反，命令式语言，如C、C++和[Java](https://www.2cto.com/kf/ware/Java/)，通常用变量和赋值语句来指定如何计算。函数式语言提供了最佳的整体简单性，因为它们能够用一种结构，即函数调用(函数调用能够以简单的方式与其他函数调用组合起来)来完成任何计算。正是这种简单优美使一些语言研究者将函数式语言作为复杂的非函数式语言(如C++)的主要替代语言。但其他因素，如效率，限制了函数式语言的更广泛应用。

## 学习技巧

根据最佳时间, 总结的一系列 策略, 和细节问题

- **学习新语言比较自然的方式, 是使用新语言写一些你已经可以用其他语言实现的程序.** 
- 优先学会系统调用和编写命令行程序
- 然后是网络编程





## Go语法

### 程序理解



### 库函数理解

Println是fmt中一个基本的输出函数, 它输出一个或多个用空格分隔的值, 结尾使用一个换行符, 这样看起来这些值是单行输出

## 语言特性

### 定义

**经典书籍**: Go是**编译型**的语言. Go的工具链将程序的源文件转变成机器相关的原生二进制指令. 这些工具可以通过单一的go命令配合其子命令进行使用. 

**百度百科**: Go(又称golang)是google开发的一种**静态强类**型, **编译**型, **并发**型,并具有**垃圾回收**功能的编程语言

- Go**原生支持Unicode**, 所以它可以处理所有国家的语言
- Go代码是**使用包来组织**的, 类似于其他语言中的库和模块.
- 变量可以在声明的时候初始化
  如果变量没有明确地初始化, 它将隐式地初始化为这个类型的空值
- Go不需要再语句(statement)或声明结尾使用分号, 除非多个语句或声明出现在同一行
  事实上, 跟在特定符号后面的换行符被转换为分号, 因此在什么地方进行换行会影响对Go代码的解析)
- 没有继承多态的⾯面向对象
- 强⼀一致类型
- 天然并发
- interface不不需要显式声明(Duck Typing)
- 没有异常处理理(Error is value)
- 基于⾸首字⺟母的可访问特性
- 不不⽤用的import或者变量量引起编译错误
- 完整⽽而卓越的标准库包
- Go内置runtime（作⽤用是性能监控、垃圾回收等）
- 具有静态编译语言的安全和性能, 又有动态语言开发和维护的高效率, 既有C静态语言程序的运行速度, 又能达到Python动态语言的快速开发。
- 引入了包的概念, 用于组织程序结构, go语言的一个文件u要归属一个包, 二不能单独存在, *一个go文件需要在一个包内, 声明所属包*
- 不能多行写成一行, 否则会报错
- 定义的`变量`或是`import 包`如果未使用, 编译时将会报错
- 块注释不允许有嵌套, 一般推荐使用行注释来注释方法和语句

一、垃圾回收　

　　1、内存自动回收。

　　2、只需要创建，不需要释放

二、天然并发：

　　1、语言层支持并发，对比python，少了GIL锁。

　　2、goroute，轻量级线程。

　　3、基于CSP模型实现

 

三、channel管道

　　1、管道，类似unix/linux中的pipe

　　2、多个goroute之间通过channel进行通信

　　3、支持任何类型

## 程序原理

> 执行原理	组织结构	

## 应用场景

开发大型系统

## 优势

特性足够简单

具备垃圾回收机制

编译速度快

可读性较好, 方便维护

### 1、学习曲线容易易

Go语⾔言语法简单，包含了了类C语法。因为Go语⾔言容易易学习，所以⼀一个普通
的⼤大学⽣生花⼏几个星期就能写出来可以上⼿手的、⾼高性能的应⽤用。在国内⼤大家都追求
快，这也是为什什么国内Go流⾏行行的原因之⼀一。

### 2、效率：快速的编译时间，开发效率和运⾏行行效率⾼高

开发过程中相较于 Java 和 C++呆滞的编译速度，Go 的快速编译时间是⼀一
个主要的效率优势。Go拥有接近C的运⾏行行效率和接近PHP的开发效率。

### 3、出身名⻔门、⾎血统纯正

之所以说Go出身名⻔门，从Go语⾔言的创造者就可⻅见端倪，Go语⾔言绝对⾎血统纯
正。其次Go语⾔言出⾃自Google公司，Google在业界的知名度和实⼒力力⾃自然不不⽤用多
说。Google公司聚集了了⼀一批⽜牛⼈人，在各种编程语⾔言称雄争霸的局⾯面下推出新的
编程语⾔言，⾃自然有它的战略略考虑。⽽而且从Go语⾔言的发展态势来看，Google对它
这个新的宠⼉儿还是很看重的，Go⾃自然有⼀一个良好的发展前途。

### 4、⾃自由⾼高效：组合的思想、⽆无侵⼊入式的接⼝口

Go语⾔言可以说是开发效率和运⾏行行效率⼆二者的完美融合，天⽣生的并发编程⽀支
持。Go语⾔言⽀支持当前所有的编程范式，包括过程式编程、⾯面向对象编程、⾯面向
接⼝口编程、函数式编程。程序员们可以各取所需、⾃自由组合、想怎么玩就怎么
玩。

### 5、强⼤大的标准库

这包括互联⽹网应⽤用、系统编程和⽹网络编程。Go⾥里里⾯面的标准库基本上已经是
⾮非常稳定了了，特别是我这⾥里里提到的三个，⽹网络层、系统层的库⾮非常实⽤用。
6、部署⽅方便便：⼆二进制⽂文件，Copy部署
这⼀一点是很多⼈人选择Go的最⼤大理理由，因为部署太⽅方便便了了，所以现在也有很
多⼈人⽤用Go开发运维程序。

### 7、简单的并发

Go 是⼀一种⾮非常⾼高效的语⾔言，⾼高度⽀支持并发性。Go是为⼤大数据、微服务、并
发⽽而⽣生的⼀一种编程语⾔言。
Go 作为⼀一⻔门语⾔言致⼒力力于使事情简单化。它并未引⼊入很多新概念，⽽而是聚
焦于打造⼀一⻔门简单的语⾔言，它使⽤用起来异常快速并且简单。其唯⼀一的创新之
处是 goroutines 和通道。Goroutines 是 Go ⾯面向线程的轻量量级⽅方法，⽽而通
道是 goroutines 之间通信的优先⽅方式。
创建 Goroutines 的成本很低，只需⼏几千个字节的额外内存，正由于此，
才使得同时运⾏行行数百个甚⾄至数千个 goroutines 成为可能。可以借助通道实
现 goroutines 之间的通信。Goroutines 以及基于通道的并发性⽅方法使其⾮非
常容易易使⽤用所有可⽤用的 CPU 内核，并处理理并发的 IO。相较于
Python/Java，在⼀一个 goroutine 上运⾏行行⼀一个函数需要最⼩小的代码。

### 8、稳定性

Go拥有强⼤大的编译检查、严格的编码规范和完整的软件⽣生命周期⼯工具，具
有很强的稳定性，稳定压倒⼀一切。那么为什什么Go相⽐比于其他程序会更更稳定呢？
这是因为Go提供了了软件⽣生命周期（开发、测试、部署、维护等等）的各个环节
的⼯工具，如go tool、gofmt、go test。

### 三）、Go语⾔言的核⼼心特性和优势

Go主要有静态语言、函数多返回值、天⽣并发、内置GC（⾃自动垃圾回收）、安全性高、语法简单、编译快速这⼏几个⽅方⾯面的特性。这些特性决定了了Go的三个高富帅特性：运行快、开发快和部署快。

静态类型语⾔言是指在编译时变量量的数据类型即可确定的语⾔言，要求在使⽤用变量量之前必须声明数据类型（具有类型推导能⼒力力的现代语⾔言可能能够部分减轻这个要求）；

动态类型语⾔言是在运⾏行行时确定数据类型的语⾔言，变量量使⽤用之前不不需要类型声明，通常变量量的类型是被赋值的那个值的类型。

Go语⾔言是⽬目前项⽬目转型⾸首选的语言，也是软件⼯工程师转型⾸首选的语言，是添加技术栈的⾸首选语⾔言。Go常常是⼀一种为转型⽽量身定制的语⾔言。



### （四）、Go语⾔言能开发什什么？

1、服务器器编程，以前你如果使⽤用C或者C++做的那些事情，⽤用Go来做很合适，例如处理日志、数据打包、虚拟机处理、⽂件系统等。
2、分布式系统、数据库代理理器器、中间件等，例例如Etcd。
3、⽹络编程，这⼀一块⽬目前应用最广，包括Web应用、API应用、下载应用，⽽且Go内置的net/http包基本上把我们平常⽤用到的⽹网络功能都实现了了。
4、数据库操作
5、开发云平台，⽬目前国外很多云平台在采⽤用Go开发

### 运行方式

go run hello-world.go

go build >> ./hello-world

> 经过编译后的程序, 可以不用进行任何其他处理, 随时执行



## 编程规范

### 注释

### 标识符

Go语言中, 使用大小写来决定标识符(变量, 常量, 类型, 接口, 结构, 函数)是否可以被外部包所调用

以一个大写字母开头, 那么使用这种形式的标识符的对象就可以被外部包的代码所使用(使用时程序需要先导入这个包), 如同⾯向对象语言中的 public。

如果以小写字母开头，则对包外是不可⻅的，但是他们在整个包的内部是可⻅并且可用的，像⾯向对象语言中的 private. 

`{` 符号必须和关键字func在同一行, 不能独自成行, 对于 `x + y` 表达式, 换行符必可以在 `+` 操作符后面, 但是不能在 `+` 前面

Go对于代码的格式化要求非常严格. gofmt工具将diamante以标准格式重写, `go fmt` 命令其实使用了 `gofmt` 工具来格式化指定包里的所有文件或者当前文件夹中的文件(默认). 



## 关键字和保留字

## GO程序结构

```go
//通常在该位置对包进行描述, 
//对于main包, 注释是一个或多个完整的句子, 用来对这个程序进行整体概括
//当前程序的包名
package main

//导入其他包
import "fmt"

//常量定义
const PI = 3.14

//全局变量声明和赋值
var name = "Asa"

//一般类型声明
type newType int

// 结构声明
type my struct()

//接口声明
type golang interface()

//由main()函数作为程序的入口
func main(){
	fmt.Print("Hello, 世界!\n")
}



```

## GO项目结构

[参考文档-官方](https://golang.org/doc/gopath_code.html)

仓库, 模块, 包, 源文件(source file), 语句, 表达式, 单词

Go programs are organized into packages. A package is a collection of source files in the same directory that are compiled together. Functions, types, variables, and constants defined in one source file are visible to all other source files within the same package.

A repository contains one or more modules. A module is a collection of related Go packages that are released together. A Go repository typically contains only one module, located at the root of the repository. A file named `go.mod` there declares the module path: the import path prefix for all packages within the module. The module contains the packages in the directory containing its `go.mod` file as well as subdirectories of that directory, up to the next subdirectory containing another `go.mod` file (if any).

Note that you don't need to publish your code to a remote repository before you can build it. A module can be defined locally without belonging to a repository. However, it's a good habit to organize your code as if you will publish it someday.

Each module's path not only serves as an import path prefix for its packages, but also indicates where the `go` command should look to download it. For example, in order to download the module `golang.org/x/tools`, the `go` command would consult the repository indicated by `https://golang.org/x/tools` (described more [here](https://golang.org/cmd/go/#hdr-Relative_import_paths)).

An import path is a string used to import a package. A package's import path is its module path joined with its subdirectory within the module. For example, the module `github.com/google/go-cmp` contains a package in the directory `cmp/`. That package's import path is `github.com/google/go-cmp/cmp`. Packages in the standard library do not have a module path prefix.



## Go文件结构组成

Go 程序是通过 package 来组织的

变量

变量是计算机语言中储存数据的抽象概念。变量量的功能是存储数据。变量通过变量量名访问；

变量的本质是计算机分配的⼀一⼩小块内存，专门用于存放指定数据，在程序运⾏过程中该数值可以发⽣改变；
变量的存储往具有瞬时性，或者说是临时存储，当程序运⾏结束，存放该数据的内存就会释放，⽽该变量就会消失；

Go 语言的变量名由字⺟、数字、下划线组成，首个字符不能为数字;

**Go语法规定，定义的局部变量若没有被调⽤则编译错误。**
命名 : 驼峰命名⻛格，不建议用下划线连接多个单词。

### 七、出于性能考虑的最佳实践和建议

1. 尽可能的使⽤ `:=` 去初始化声明⼀个变量（在函数内部）；
2. 尽可能的使⽤`字符代替字符串`；
3. 尽可能的使⽤`切⽚`代替数组；
4. 尽可能的使⽤数组和切⽚代替map；
5. 如果只想获取切⽚中某项值，不需要值的索引，尽可能的使⽤`for range`去遍历切⽚，这⽐必须查询切⽚中的每个元素要快⼀些；
6. 当数组元素是`稀疏`的（例如有很多0值或者空值nil），使⽤map会降低内
    存消耗；
7. 初始化map时指定其容量；
8. 当定义⼀个⽅法时，使⽤`指针类型`作为⽅法的接收者；
9. 在代码中使⽤`常量`或者标志提取常量的值；
10. 尽可能在需要分配⼤量内存时使⽤`缓存`；
11. 使⽤`缓存模板`。





# Go语言编程风格

> Go语言对于代码的格式化要求非常严格
>
> gofmt是用来格式化代码分官方工具

1. go不需要再语句或声明后面使用分号结尾, 除非有多个语句或声明出现在同一行(*这种写法也不被推荐*)。
2. 事实上, 跟在特定符号后面的换行符被转换为分号`;`, 在什么地方进行换行会影响对Go代码的执行;
3. "`{`"符号必须和关键字func在同一行, <u>不能独自成行</u>;
4. ` ⏎`符需要谨慎使用不能出现在 `+` 等操作符之前;

# **语言参考**

> [官方文档](https://golang.org/ref/spec)

`''` 单引号表示元字符(asci, rune), `""`双引号表示字符串, `` ` 反引号表示多行字符串

## 注解 - Notation

> 语言文法说明
>
> [参考文档](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)

`=` 定义 defination

`|` 替代 alternation

`()` 分组 grouping

`[]` 可选 option

`{}` 重复 repetition

## 词法元素-Lexical elements

## 关键字-Keywords

> [defer, recover, panic](https://blog.golang.org/defer-panic-and-recover)

### defer

> A defer statement defers the execution of a function until the surrounding function returns.
>
> The deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns.

defer会在ruturn后执行

```go
defer fmt.Println("1")  // 函数返回后调用
return 0


```

### 

## 常量 - Constants

## 变量 - Variables

> 内存中的一块存储空间, 内存地址的索引或别名, 可以通过变量访问变量所存储的变量值, 取到变量实际存储的数据
>
> 每初始化一个变量都会新开辟一块内存空间

## 类型 - Types

## 属性 - Properties

> Properties of types and values

## 表达式 - Expressions

## 语句 - Statements

## 内置函数 - Built-in functions





### make



### new





### panic-抛出

> 应用场景, 处理非预期的错误时, 抛出错误, 相当于一个抛出一个故障, 尤其是无法正常处理的错误.
>
> 类似定义一个错误对象



### recover

> 从go协程的异常控制流中收回控制权, 重新控制

代码片段执行完成, 或函数返回后操作

## 包 - Packages

> **关于导包**: 按照约定，包名与导入路径的最后一个元素一致。例如，"math/rand" 包中的源码均以
>
> package rand 语句开始。 初始化和执行 - Program initialization and execution
>
> go程序是由package组成的, 程序从 package main运行起

```text
Every Go program is made up of packages.

Programs start running in package main.

By convention, the package name is the same as the last element of the import path. 
```



Go代码是使用**包**(package)来组织的, 包类似于其他语言中的库和模块. 一个包由一个多个`.go`源文件组成, 放在一个文件夹中, 该文件夹的名字描述了包的作用. 每一个源文件的开始都用package声明,package main 指明了这个文件属于哪个包. 后面跟着导入其他包的列表, 然后是存储在文件中的程序声明.



声明给一个程序实体命名，并且设定其部分或全部属性。有4个主要的声明:（var）、常量（ const）类型（type）和函数（fun）。本章讨论变量和类型，常量放在第3章讨论，函数放在第5章讨论。
Go程序存储在一个或多个以·go为后缀的文件里。每一个文件以 package声明开头，表明文件属于哪个包。 package声明后面是import声明，然后是包级别的类型、变量、常量、函数的声明，不区分顺序。

名为 `main` 的包比较特殊, 它用来定义一个独立的可执行程序, 而不是库.  

*注意可执行程序和库的区别, 可执行程序一定有main包, 库一般不需要main包, 工程项目文件中不一定有main包, 因为不一定需要时一个可执行程序文件*

在 `main` 包中, main函数也是特殊的, 不管在什么程序中, main做什么事情, 它总是程序开始执行的地方. 

<u>main函数不能有返回值</u>

当然, main通常调用其他包中的函数来做更所的事情.

导包时必须是精确的, 不能缺失, 也不可以存在不需要的包, 这样都会造成编译失败

`import` 声明必须跟在 `package` 声明之后, 

然后是 : `function` 或 `variable` 或 `instant` 或 `type` 声明:(fun, var, inst, type)声明

*包的形式通常是指一个文件夹, 最顶层的文件夹, 这和Python的叫法类似* 每一个源文件的开始都用**package**声明, 指明这个源文件属于哪个包。



## 函数 - Functions

> 函数执行完成后, 程序控制和返回值都返回给调用者. 

函数声明 

```go
func name(para1,para2){
    statements
    return
}

func 函数名(参数1,参数2){
    函数体
    return
}
```

## 切片 - Slice

```go 
os.Args[0:len(os.Args)]
```



## 错误 - errors

## 运算符-Operators

> [官网链接](https://golang.org/ref/spec#Operators)

#   符号词法

> 更多参考[语言参考](https://golang.org/ref/spec)

## `_` - 下划线: 空标识符

空标识符可以用在任何语法需要变量名但是程序逻辑不需要的地方, 例如丢弃每次迭代产生的无用索引。

## `==` 比较

对于引用类型, 例如指针和通道, 操作符`==`检查的是引用相等性, 即他们是否指向相同的元素



## `[]` 切片 ??

## `...`可变长度标识

## `<-`通信操作符

## `#` 输出

# 流程控制

## 变量声明

```go
//下面的定义是等价的
s := ""
var s string
var s = ""  
var s string = ""  // 显式的变量类型, 在类型一致的情形下是冗余信息, 不一致情形下是必须的
```

## if语句

## for 语句

```go
// for condition clause
for a<b {
  ...
}
// for clause
for i := 0; i<5; i++ {
  ...
}

// for range
for _, arg := range os.Args[1:] {
  ...
}


```



## select 语句

```go
select {
    case <- ch1:
        // ...
    case <- ch2:
        // ...
    case <- ch3:
        // ...
    default:
        // ...
}
```



## defer语句

# 基本概念

## 零散记录

- 程序-**program**: 计算机指令(,动作, 过程, 流程的集合), 通常指源代码编译生成的二进制文件.
- 源文件-**source file**: 编写程序的源代码文件
- 操作数-**operands**: 运算符作用于的实体, 操作对象, 运算对象
- 语法块-**syntactic block**: 大括号围起来的一个语句序列, 比如一个循环体或函数体.
- 词法块-**lexical block**: 没有被显式包含在大括号中的声明代码. 包, 文件, for语句等
- 全局块-**global block**: 包含了全部源代码的词法块.
- 模块-**module**:
    - A module is a collection of [Go packages](https://golang.org/ref/spec#Packages) stored in a file tree with a `go.mod` file at its root. The `go.mod` file defines the module’s *module path*, which is also the import path used for the root directory, and its *dependency requirements*, which are the other modules needed for a successful build. Each dependency requirement is written as a module path and a specific [semantic version](http://semver.org/).
- 包-**package**: 
- 环境变量:
    - GOROOT:Go 语言的当前安装目录
    - GOPATH(Deprecated):工作区目录
        - the location of workspace
- 导入路径(import path): 唯一标识包(package)的字符串



## Go指针 - pointer

> 指针, 也称"引用", 指针变量

Go指针的指是变量的地址。在一些语言中(比如C), 指针是没有约束的。其他语言中, 指针被称为"引用", 并且除了到处传递之外, 它不能做其他的事情。

Go做了一个折中, 指针显式课件。 使用 `&` 操作符可以获取一个变量的地址, 使用 `*` 操作符可以获取指针引用的变量的值, 但是指针不支持算术运算。

```go
// 关于指针的例子说明

// 使用函数改变变量的值 
package main
import "fmt"

func changeValue(p int) {
  p = 10
}
func main() {
  var a int = 1
  changeValue(a)  //形参会在函数每调用一次时初始化并新开辟一个内存地址, 
  
  fmt.Println(a)  // 这个时候a的值应该为1  并未修改成功
}
```

```go
package main
import "fmt"

func changeValue(p *int) {
  *p = 10
}
func main() {
  var a int = 1
  changeValue(&a)  //形参会在函数每调用一次时初始化并新开辟一个内存地址, 
  
  fmt.Println(a)  // a = 10 修改成功
}
```

*形参会初始化一个新的内存地址, 而指针则是直接操控内存地址, 但是初始化了一个新的指针变量*

## 控制流

for, if,  switch



## 命名类型

```go
type Point struct {
  X, Y int
}

var p Point
```



## 方法-method

一个关联了命名类型的函数称为方法

## 接口-interface

接口可以用相同的方式处理不同的具体类型的抽象类型, 它基于这些类型所包含的方法, 而不是类型的描述或实现

## 注释

在声明任何韩式钱, 写一段注释来说明它的行为是一个很好的风格。这个约定很重要, 因为它们可以被go doc 和godoc工具定位和作为文档显示。



# 常见需求

使用go开发命令行程序 

```bash
cd $GOPATH/src/

mkdir hello
code hello/hello-world.go

go install hello  # 包路径就是 命令名称

```

# Go Tools

go build 

go install 



# Go modules

- Go模块开发步骤:
    - 创建一个新的模块
        - creating a new module
    - 增加一个依赖
        - adding a dependency
    - 升级依赖
        - upgrading dependencies
    - 在新的主要版本中增加一个依赖
        - Adding a dependency on a new major version.
    - 升级一个依赖到一个新的主要版本中
        - upgrading a denpendency to a new major version.
    - 移除不使用的依赖
        - removing unused dependencies.



# 最佳实践



> What types of software do you develop with Go?
>
> 36%		Websites
>
> 31%		Utilities (small apps for small tasks)
>
> 26%		IT Infrastructure
>
> 24%		Libraries / Frameworks
>
> 20%		System Software
>
> 14%		Database / Data Storage
>
> 12%		Programming Tools
>
> 6%		Business Intelligence / Data Science / Machine Learning
>
> 
>
> ---
>
> 
>
> DevOps and Infrastructure development are some of the most popular uses for Go. 

使用 go fmt *.go 格式化代码/ 或者 ctrl + alt + L

用go编写命令行程序的感觉真是太爽了! 一次编译,多处运行

## Go Router

> 路由
>
> gorilla / mux    39%
>
> Standard library  30%

## 重要特性

go runtime / channels docker microservice

## 如何正确编写Go代码

前提:

合理使用 go packages 和 go commands

### 代码组织

工作空间: go的工作环境, 相当于 python的虚拟环境一样 

- 将所有代码组织到一个单独的工作空间(workspace)
- 一个工作空间包含许多版本控制仓库;
- 每个仓库包含一个或多个包;
- 每个包由单独的目录和源文件来构成;*[ 一个目录作为一个包? ]*
- 包的目录路径决定了导入路径

注意与其他开发环境的区别: 每个工程有一个分离的工作空间, 工作空间与版本控制仓库的紧密相连. 

**工作空间**: 目录层级是两个目录`src` 和 `bin` 作为根目录

`src` contains Go source files and `bin` contains executable commands;

```bash
bin/
    hello                          # command executable
    outyet                         # command executable
src/
    github.com/golang/example/
        .git/                      # Git repository metadata
	hello/
	    hello.go               # command source
	outyet/
	    main.go                # command source
	    main_test.go           # test source
	stringutil/
	    reverse.go             # package source
	    reverse_test.go        # test source
    golang.org/x/image/
        .git/                      # Git repository metadata
	bmp/
	    reader.go              # package source
	    writer.go              # package source
    ... (many more repositories and packages omitted) ...
```

`GOPATH` 环境变量 : 

```bash
# 查询GOPATH 是否存在
echo $GOPATH

# 将go命令集添加到根目录
export PATH=$PATH:$(go env GOPATH)/bin
```



### 代码测试

### 导入远程包

# **代码调试**



# 常见问题1

- `i++` 等价于 `i += 1` 等价于 `i = i + 1` 这是一个语句, 而不是表达式 不同于其他C族语言, 因此 `j = i++` 是错误的写法
- Go 不允许存在无用的临时变量。*声明未使用, 不需要的变量*
- 大多数Go程序员喜欢搭配使用range和_来写循环程序, 因为索引是隐式的, 不容易换错。
- 使用显式的初始化来说明初始化变量的重要性, 使用隐式的初始化来表名初始化变量不重要
- <u>按照惯例, 包的名字和导入路径的最后一个元素一致</u>



# 常见问题2

## go module 与 GOPATH

# 底层原理

## Go垃圾回收机制

三色标记法



## GMP模型- Go调度器

> [参考文献1](https://zhuanlan.zhihu.com/p/352964026)
>
> [参考文献2](https://www.cnblogs.com/luozhiyun/p/14426737.html)
>
> [官方文档](https://golang.org/src/runtime/proc.go)
>
> [中文书籍-Go语言设计与实现](https://draveness.me/golang/docs/part3-runtime/ch06-concurrency/golang-goroutine/)
>
> go scheduler

<u>Go 语言的调度器通过使用与 CPU 数量相等的线程以减少线程频繁切换的内存开销，同时在每一个线程上执行额外开销更低的 Goroutine 来降低操作系统和硬件的负载。</u>

真非协作的抢占式调度器:

M 内核线程, 工作线程

G: 协程单元

```text
G - goroutine. 一个待执行的任务
M - worker thread, or machine. 内核线程, 工作线程, 操作系统线程, 有内核调度和管理.
P - processor, a resource that is required to execute Go code.
     M must have an associated P to execute Go code[...].
     处理器, 运行在线程上的本地调度器.
```

goroutine和调度器都依赖于内核线程.

Go调度器: 分配准备就绪的Goroutine到工作线程中.

P: 处理器, 执行Go代码所需要的资源, 

M的数量一般为CPU的核心数, M需要与P关联使用以执行Go代码. M可能被阻塞, 或者在一个系统调用中不保含或没有关联的P.



工作线程暂停或解除暂停. 我们需要在 保持足够多的工作线程以利用可用的并行硬件资源 和 暂停过多(excessive)的运行中的工作线程以节省CPU资源和电量 中保持平衡. 

这并不容易, 有以下两个原因:  

1, 调度器状态是刻意分布式的(P工作队列)

2, 为了理想的线程管理我们需要知道接下来的线程(当一个新的G准备好时, 不应该暂停工作线程).

**饥饿状态**: 活跃的, 旋转的线程, 等待分配任务, 发现可执行的线程后立即执行线程.

当前的办法: 

```text
We unpark an additional thread when we ready a goroutine if (1) there is an
idle P and there are no "spinning" worker threads.
```



如果有一个闲置的P且没有一个旋转的(spinning, 活跃)工作线程(重复检查状态, 没有挂起, 活跃的)时, 在准备好一个G后启动一个附加的线程

<u>如果存在闲置的P并且没有活跃的M时, 当一个G准备好后启动一个附加的线程M.</u>



```text
A worker thread is considered spinning if it is out of local work and did not find work in global run queue/netpoller; the spinning state is denoted in m.spinning and in sched.nmspinning.
```

如果任务完成后且没有发现全局运行队列/轮询, M进入活跃状态(饥饿状态).这个饥饿状态表示为 `m.spinning`. 



```text
Threads unparked this way are also considered spinning; we don't do goroutine
handoff so such threads are out of work initially.

Spinning threads do some
spinning looking for work in per-P run queues before parking. 
```

启动的线程也被考虑为饥饿状态的, 不执行(传递)G时的M最初是没有工作的.

活跃的M在暂停前轮询执行P运行队列中的任务.



```text
If a spinning thread finds work it takes itself out of the spinning state and proceeds to execution. If it does not find work it takes itself out of the spinning state
and then parks.
```

如果饥饿线程M发现任务时, M进入非饥饿状态并继续任务. 如果没有发现任务, M进入饥饿状态并暂停.



```text
If there is at least one spinning thread (sched.nmspinning>1), we don't unpark new threads when readying goroutines. To compensate for that, if the last spinning thread finds work and stops spinning, it must unpark a new spinning thread.

This approach smooths out unjustified spikes of thread unparking, but at the same time guarantees eventual maximal CPU parallelism utilization.
```

如果有至少一个饥饿线程M, 在出现准备就绪的G时不需要启动新的(用户态)线程M. 作为补偿, 如果最后一个饥饿线程开始工作并停止饥饿时,  需要启动一个新的饥饿线程.



这种方法不但消除了不合理的线程M断开, 并且同时保证了最大化CPU资源利用.



```text
The main implementation complication is that we need to be very careful during
spinning->non-spinning thread transition. This transition can race with submission of a new goroutine, and either one part or another needs to unpark another worker thread. If they both fail to do that, we can end up with semi-persistent CPU underutilization. The general pattern for goroutine readying is: submit a goroutine to local work queue, #StoreLoad-style memory barrier, check sched.nmspinning.

The general pattern for spinning->non-spinning transition is: decrement nmspinning, #StoreLoad-style memory barrier, check all per-P work queues for new work.

Note that all this complexity does not apply to global run queue as we are not sloppy about thread unparking when submitting to global queue. Also see comments
for nmspinning manipulation.
```

主要的实现复杂性是, 在线程M从饥饿状态到非饥饿状态转变(transition)时我们需要非常小心. 这种转变可能在提交一个新的协程时产生竞争, 其中一个部分或另一个部分需要启动一个新的工作线程M. 如果两者都失败了, 可能会出现半持续性的CPU利用率不足.  当一个G准备就绪时的通常做法是: 提交一个G到局部任务队列——存储加载式的内存屏障，检查sched_nmspinning, 检查M的饥饿状态.



线程M的饥饿状态转移时的通常做法是:  饥饿状态减量/缩减——存储加载式的内存屏障, 检查M的饥饿状态. 



需要注意的是, 这种复杂性不适用于全局运行队列. 当提交全局运行队列时, 我们不会轻易的启动线程. 

也可以参考饥饿状态操作的注解.



### G-Goroutine

Goroutine 是 Go 语言调度器中待执行的任务，它在运行时调度器中的地位与线程在操作系统中差不多，但是它占用了更小的内存空间，也降低了上下文切换的开销。

Goroutine 只存在于 Go 语言的运行时，它是 Go 语言在用户态提供的线程，作为一种粒度更细的资源调度单元，如果使用得当能够在高并发的场景下更高效地利用机器的 CPU。



### M-Machine

Go 语言并发模型中的 M 是操作系统线程。调度器最多可以创建 10000 个线程，但是其中大多数的线程都不会执行用户代码（可能陷入系统调用），最多只会有 `GOMAXPROCS` 个活跃线程能够正常运行。



### P-Processor

调度器中的处理器 P 是线程和 Goroutine 的中间层，它能提供线程需要的上下文环境，也会负责调度线程上的等待队列，通过处理器 P 的调度，每一个内核线程都能够执行多个 Goroutine，它能在 Goroutine 进行一些 I/O 操作时及时让出计算资源，提高线程的利用率。



因为调度器在启动时就会创建 `GOMAXPROCS` 个处理器，所以 Go 语言程序的处理器数量一定会等于 `GOMAXPROCS`，这些处理器会绑定到不同的内核线程上。

### 调度器启动



1. 当 `next` 为 `true` 时，将 Goroutine 设置到处理器的 `runnext` 作为下一个处理器执行的任务；
2. 当 `next` 为 `false` 并且本地运行队列还有剩余空间时，将 Goroutine 加入处理器持有的本地运行队列；
3. 当处理器的本地运行队列已经没有剩余空间时就会把本地队列中的一部分 Goroutine 和待加入的 Goroutine 通过 [`runtime.runqputslow`](https://draveness.me/golang/tree/runtime.runqputslow) 添加到调度器持有的全局运行队列上；

处理器本地的运行队列是一个使用数组构成的环形链表，它最多可以存储 256 个待执行任务。

![golang-runnable-queue](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210426193643.png)

简单总结一下，Go 语言有两个运行队列，其中一个是处理器本地的运行队列，另一个是调度器持有的全局运行队列，只有在本地运行队列没有剩余空间时才会使用全局队列。

### 调度循环

[`runtime.schedule`](https://draveness.me/golang/tree/runtime.schedule) 函数会从下面几个地方查找待执行的 Goroutine：

1. 为了保证公平，当全局运行队列中有待执行的 Goroutine 时，通过 `schedtick` 保证有一定几率会从全局的运行队列中查找对应的 Goroutine；
2. 从处理器本地的运行队列中查找待执行的 Goroutine；
3. 如果前两种方法都没有找到 Goroutine，会通过 [`runtime.findrunnable`](https://draveness.me/golang/tree/runtime.findrunnable) 进行阻塞地查找 Goroutine；

[`runtime.findrunnable`](https://draveness.me/golang/tree/runtime.findrunnable) 的实现非常复杂，这个 300 多行的函数通过以下的过程获取可运行的 Goroutine：

1. 从本地运行队列、全局运行队列中查找；
2. 从网络轮询器中查找是否有 Goroutine 等待运行；
3. 通过 [`runtime.runqsteal`](https://draveness.me/golang/tree/runtime.runqsteal) 尝试从其他随机的处理器中窃取待运行的 Goroutine，该函数还可能窃取处理器的计时器；

因为函数的实现过于复杂，上述的执行过程是经过简化的，总而言之，当前函数一定会返回一个可执行的 Goroutine，如果当前不存在就会阻塞等待。

### 触发调度





# **Go标准库**

## os

提供一些函数和变量, 以与平台无关的方式和操作系统打交道

### os.Args



## fmt

> 格式化工具

### fmt.Printf

> f: format, 输出格式化字符串

用于格式化输出, 第一个参数是格式化指示字符串. 转义字符被称为verb

默认不写换行符

按照约定: `log.Printf`和 `fmt.Errorf` 之类的格式化函数以f结尾, 使用和 `fmt.Printf` 相同的格式化规则; 而那些以 ln结尾的函数则使用%v的方式来格式化参数, 并在最好追加换行符。

通常`Printf`的格式化字符串含有多个%谓词, 这要求提供相同数目的操作数, 

### fmt.Println

> ln: line, 输出一行, 并具有换行符



## strings

> 类似于Python中的字符串的方法
>
> 提供了许多函数, 用于查找(search)、替换(replace)、比较(compare、修整(trim)、切分(split)与连接(join)字符串

### strings.Join

## bufio

简便和高效地处理输入和输出。

## bytes

## unicode

> 判断文字符号(rune)的特性类型, 并返回布尔值

## strconv

> 主要用于转换布尔值、整数、浮点数为与之对应的字符串形式, 或者把字符串转换为布尔值、整数、浮点数, 另外还有为字符串添加/去除引号的函数.

# 核心知识

- goroutine
- channel
- mutex
- syncmap
- gin
- grpc
- 并发编程
- 分布式架构

# Go程序设计语言

> 与其他编程语言一样, Go语言中的大程序都从小的基本组件构建而来: 变量存储值; 简单表达式通过加和减等操作合并成大的; 基本类型通过数组和结构体进行聚合; 表达式通过if和for等控制语句来决定执行顺序; 语句被组织成函数用于隔离和复用; 函数被组织成源文件和包. 

## 程序结构-Program Structure

> program structure
>
> the basic structural elements of a Go Program. 



### 名称-Names

> variables -> aggregates -> expressions -> statements -> functions -> source files -> packages. 



Go的 **关键字(keywords)** 不能用作名称:

```go
			                 25 keywords of Go

break:
case:
chan:
const:
continue:

default:
defer:  // 推延
else:
fallthrough
for:

func:
go:
goto:
if:
import:

interface:
map:
package:
range:
return:

select:
struct:
switch:
type:
var:

```



以下的 **预声明(predeclared)** 的常量、类型和函数 虽然不是预留的, 可以在声明中使用它们, 但是重声明有发生冲突的风险: 

```go

// 常量 constants

true false iota nil

// 类型 types
int int8 int16 int32 int64
uint uint8 uint16 uint32 uint64
float32 float64 complex128 complex64
bool byte rune string error

// 函数 functions
make len cap new append copy close delete 
complex real imag
panic recover

```

如果一个实体在函数中声明, 它只在函数 **局部(local)** 有效. 如果声明在函数外, 它将对包里面的所有源文件可见. 

实体第一个字母的大小写决定其可见性是否跨包. 如果名称已大写字母开头, 它是 **导出(exported)** 的, 意味着它对保外是可见和可访问的, 可以被自己包之外的其他程序所引用, 如 `fmt.Printf`. 包名本身总是由小写字母组成. 

名称的长度使没有限制的, Go的编程风格倾向于使用短名称. 当名称的作用域越大就使用越长且更有意义的名称. 

风格上Go 程序员更喜欢采用 "**驼峰式(camel case)**" 的风格——更喜欢使用大写字母而不是下划线, 比如: `QuoteRuneToASCII`, `parseRequestLine`, 遇到缩写类型时则是 `htmlEscape`, `escapeHTML`, `HTMLEscape`, 但不会是`escapeHtml`. 

### 声明-Declarations

> 变量声明, 常量声明, 类型声明, 函数声明. 
>
> 局部变量声明, 全局变量声明, 多变量声明

Go程序存储在一个或多个以 `.go` 为后缀的文件里. 每个文件以package声明开头 



```go
var a int  // 仅声明, 默认值为零值

var a int = 10  

var a = 100 // 可用 但不推荐
// 多变量声明

var a, b int = 10, 20
var (
	a int = 100
  b string = "abcd"
)

a := 10 // 推荐, 只能使用在函数体内 
```



### 变量-Variables

```go
// var 变量名 类型 = 表达式
var name type = expression
```

类型和表达式部分可以省略一个，但是不能都省略。

如果类型省略，它的类型将由初始化表达式决定；如果表达式省略，其初始值对应于类型的零值--对于数字是`0`，对于布尔值是`false`，对于字符串是`""`，对于接口和引用类型（slice，指针pointer、map、通道channel、函数function）是`nil`，对于一个像数组或结构体这样的复合类型，零值是其所有元素或成员的零值。
零值机制(zero-value mechanism)保障所有的变量是良好定义的， 

Go里面不存在未初始化变量. 这种机制简化了代码, 并且不需要额外工作就能感知边界条件的行为. 

输出空字符串, 而不是一些错误或不可预料的行为. Go程序员经常花费精力来使复杂类型的零值有意义, 以便变量一开始就处于一个可用状态. 

初始值设定可以是字面量值或者任意的表达式. 包级别的初始化在main开始之前进行, 局部变量初始化和声明一样在函数执行期间进行.

变量可以通过调用返回多个值的函数进行初始化: 

```go
var f, err = os.Open(name)  // os.Open返回一个文件和一个错误
```

#### 短变量声明

**短变量声明(short variable declaration)**: 用于声明和初始化局部变量. name的类型由 `expression` 的类型决定.

局部变量的声明和初始化中主要使用短变量声明. var 声明通常是为那些跟初始化表达式类型不一致的局部变量保留的, 或者用于后面才对变量赋值以及变量初始值不重要的情况. 

<u>短变量声明无法应用于全局变量声明, 只能应用于函数体内</u>

```go
name := expression
i := 100
var boiling float64 = 100 // 一个float64类型的变量
var names []string	
i, j := 0, 1  // 变量声明和初始化
i, j = j, i  // 变量赋值
```

`:=`表示声明, `=`表示赋值

一个容易被忽略但重要的地方是: 短变量声明不需要声明所有在左边的变量. 

如果一些变量在同一个词法块中声明, name对于那些变量, 短声明的行为等于赋值. 

短变量声明最少声明一个新变量, 否则代码编译无法通过. 

```go
in, err := os.Open(infile)
out, err:= os.Create(outfile)  // 此次err相当于赋值
in, err:= os.Create(outfile)  // 因为in, err均已存在, 所以编译会报错
```

#### 指针

**指针(pointer)**: 存储变量的地址(address). 

指针的值是一个变量的地址. 一个指针指示值所保存的位置. 不是所有的值都有地址, 但是<u>所有变量都有值</u>. 

<u>使用指针可以在无须知道变量名字的情况下, 间接(indirectly)读取或更新变量的值.</u>

```go
x := 1
p := &x  // p 是整型指针, 指向x
fmt.Println(*p)
fmt.Println(p)
*p = 2 // 修改指针指向变量的指 x = 2, 该语句修改了变量x的值
fmt.Println(x)
fmt.Println(p)

var x int  // x是整型变量
p := &x  // p是整型指针, p指向x, &x表达式的指是指针, *p表达式的值是一个整型变量
```

每个聚合类型(aggregate type)的组成(component, 组件)——结构体的成员(field)或数组中的元素(element)都是变量, 所以也有一个地址. 

指针类型的零值是`nil`.

函数返回局部变量的地址是非常安全. 每次调用后返回的局部变量值是不同的. 

```go
var p = f()
func f() *int {
  v := 1
  return &v
}

fmt.Println(f() == f())  // "false"
```

因为一个指针包含变量的地址, 所以传递一个指针参数给函数, 能够让函数更新间接传递的变量值

每次使用变量的地址或复制一个指针, 我们就创建了新的 **别名(aliases)** 或者方式来标记同一个变量. 指针别名允许我们用不同的变量的名字来访问变量. 

```go
func incr(p *int) int {  // *int 整型指针类型
  *p++ 
  return *p
}

v := 1
incr(&v)  // 副作用: side effect
fmt.Println(incr(&v)
```

#### new函数

```go
p := new(int)  // p的类型是 *int, 指向未命名的int变量
fmt.Println(*p)  // "0"
*p = 2  // 把未命名的int设置为2
fmt.Println(*p)  // 2
```

使用new创建的变量和取其地址的普通局部变量没有什么不同, 只是不需要引入(和声明)一个虚拟的名字, 通过new(T)就可以直接在表达式中使用.

每一次调用new返回一个具有唯一地址的不同变量:

```go
p := new(int)
q := new(int)

fmt.Println( p == q)  // "false"
```

new 是一个预声明的函数, 不是一个关键字, 可以对其进行重声明. 

#### 变量的生命周期

生命周期指在程序执行过程中变量存在的时间段. 

包级别变量的生命周期是整个程序的执行时间.

局部变量有一个动态的生命周期: 每次执行声明语句时创建一个新的实体, 变量抑制生存到它变得不可访问(unreachable), 这时它占用的存储空间被回收. 

<u>函数的参数和返回值也是局部变量,</u> 它们在其闭包函数被调用的时候创建. 

在没有指针或其他方式的引用可以找到变量时, 变量变得不可访问.

变量的生命周期是通过它是否可以到达Kauai确定的, 局部变量可在包含它的循环的一次迭代之外继续存活. 即使包含它的循环已经返回, 它的存在还可能延续. 

编译器可以选择使用堆或栈上的空间来分配.

逃逸(escape)

每次变量逃逸都需要一次额外的内存分配过程. 

垃圾回收对于写出正确的程序有巨大的帮助, 但是免不了考虑内存的负担. 不需要显式分配和释放内存, 但是变量的生命周期是写出高效程序所必须清楚的. 

在长生命周期对象中保持短生命周期对象不必要的指针, 会导致短生命周期里的对象难以被回收. 

### 赋值-Assignments

赋值语句用来更新变量所指的值.

```go
x = 1  // 有名称的变量
*p = true  // 间接变量
person.name = "bob"  // 结构体成员
count[x] = count[x] * scale  // 数组或slice或map的元素
count[x] *= scale
v++  // v = v + 1
v--
```

#### 多重赋值(tuple assignment)

多个变量被一次赋值. 

```go
x, y = y, x
a[i], a[j] = a[j], a[i]
f, err = os.Open("foo.txt")  // 函数调用返回两个值
```

#### 可赋值性assignability

显式的(explicit), 隐式的(implicit)

不管是隐式赋值还是显式赋值, 如果变量和值得类型相同, 则该赋值语句就是合法的(legal). 

可赋值性根据类型不同有着不同的规则, 我们将会引入新类型的时候解释相应的规则. 一般的规则是:

<u>类型必须精准匹配, nil可以被赋值给任何接口变量或引用类型</u>

两个值使用 `==` 和 `!=` 进行比较与可赋值性相关

可比较性(comparability)

### 类型声明-Type Declarations

变量或表达式的类型定义了这些值应有的特性. (具有的操作属性或操作方法))

任何程序中, 都有一些变量使用相同的表示方式, 但有着不同的含义. int 可能是 索引, 时间戳, 月份或者文件描述.

因此对于基础类型可以就进一步的类型标识

`type` 声明定义一个新的 **命名类型(named type)** , 它和某个已有类型使用同样的 **底层类型(underlying type)**. 命名类型提供了一种方式来区分底层类型的不同或不兼容使用.

命名类型的底层类型决定了它的结构和表达式, 以及它支持的内部操作集合, 这些内部操作与直接使用底层类型的情况相同.

```go
// type name underlying-type
// type 类型名 底层类型
type Celsius float64
type Fahrenheit float64
func CTFc(c Celsius) Fahrenheit {return Fahrenheit(c*9/5 + 32)
```

类型转换 Fahrenheit(t) 表示类型转换不是函数调用. 

类型转换不改变类型值的表现形式(represention), 仅改变类型. 如果x对于类型T是可赋值的, 类型转换也是允许的, 但是通常是不必要的. 

<u> 不同的命名类型没办法比较, 编辑器或编译器会报错</u>

```go
func (c Celsius) String() string {return fmt.Sprintf("%g℃", c)}  // 声明一个接口方法??
```



### 包和文件-Packages and Files

<u>在Go语言中包的作用和其他语言中的库或模块作用类似, 用于支持模块化、封装、编译隔离和重用.</u>

一个包的源代码存在一个或多个以.go结尾的文件中, 它所在的目录名的尾部就是导入路径.

每一个包给它的声明提供独立的命名空间(name space)

当导入包时, 它的成员通过诸如`tempconv.CToF`等方式被引用.



#### 导入import

修饰标识符

导入路径, 包名(导入路径的) 包名可以是不唯一的

```go
// 导入标准库
import "fmt"
//导入本地库, 相对路径导入


//防止冲突, 为包设置短名字(short name)别名
mrand "math/rand"
// 导入网络库


```



#### 包初始化

包的初始化从包级别变量开始, 这些变量按照声明顺序初始化, 在依赖已解析完毕的情况下, 根据依赖顺序进行. 

```go
var a = b + c  // 最后把a初始化为3
var b = f()  // 通过调用f接着把b初始化为2
var c = 1  // 首先初始化为1 
func f() int { return c + 1}
```

如果包由多个.go文件组成, 初始化按照编译器收到文件的顺序进行: go工具会在调用编译器前将.go文件进行排序. 

包的初始化按照在程序中导入的顺序来进行, 依赖顺序优先, 每次初始化一个包. 

初始化过程是自下向上的, main包最好初始化



### 作用域-Scope

声明将名字和程序实体关联起来, 如一个函数或一个变量. 

声明的作用域(scope)是指用到声明时所声明名字的源代码片段. 

不要将作用域(scop)和生命周期(lifetime)混淆. 

声明的作用域是声明在程序文本中出现的区域, 它是一个编译时(compile-time)属性.

变量的生命周期是变量在程序执行期间能被程序的其他部分所引用的起止时间, 它是一个运行时(run- time)属性. 

一个声明的词法块决定声明的作用域大小. int、len和true等内置类型、函数或常量在全局块中声明并且对整个程序可见. 

控制流标签(break, continue, goto)的作用域是整个外层的函数(entire enclosing function).

一个程序可以包含多个同名的声明, 前提是他们在不同的词法块中.

当编译器(compiler)遇到一个名字的引用时, 将从最内层的封闭词法块到全局块寻找其声明. 如果没有找到, 它会报"undeclared name"错误; 出现同名声明时, 内层声明会覆盖外层声明, 使得外层声明变得不可访问. 

<u>在包级别, 声明的顺序和它们的作用域没关系, 所以一个声明可以引用它自己活着跟在它后面的其他声明, 使我们可以声明递归或相互递归的类型和函数.</u>

## 基础数据类型-Basic Data Types

> basic data types

<u>在Go中, 每种数据类型都有自己特定的大小, 对正负号的支持也各异.</u>

计算机的底层全是位(bit), 而实际操作则是基于大小固定的单元中的数值, 称为字(word).

Go的数据类型分四大类: 基础类型(base type), 聚合类型(aggregate type), 引用类型(reference type)和接口类型(interface type)

### 整型-Integers

> unsigned integers 无符号整型, uint

int, int8, int16, int32, int64

uint, uint8, uint16, uint32, uint64

int, 和uint等于该平台上运算效率最高的值, 一般32位或64 位

`rune`类型时`int32`的同义词, `uint8`是`byte`的同义词

uintptr 其大小不明确但足以保存指针, 很少用, 仅仅用于底层编程.

int和int32是不同类型

<u>相较于uint一般习惯上更长用int</u>

<u>通常将某种类型的值转换为另一种, 需要显示转换</u>

算术运算符和逻辑运算符需要操作数的类型必须相同

```go
// Go的二元操作符, 按优先级降序排序
// 二元运算符分五大优先级, 并满足左结合律
// 算术运算符
*		/		%		<<		>> 	&		&^
+		-		|		^

// 比较运算符
==		!=		<		<=		>		>=

// 逻辑运算符
&&

||

```

取模运算符%仅仅用于整数

```go
var apples int32 = 1
var oranges int64 = 2

var f = int(apples) + int(oranges)   // 进行显式地类型转换
```

浮点数转换成整型, 会舍弃小数部分, 正值向下取整, 负值向上取整

Go语言二进制没办法直接表示, 输出则用%b

### 浮点数-(Floating-Point Numbers)

Go具有两种大小的浮点数: `float32`和`float64`. 绝大多数情况下都应该优先使用`float64`

小数点前的数字可以省略(.707), 后面的也可以省去(1.)

### 复数-Complex Numbers

### 布尔值-Booleans

### 字符串=Strings

字符串是不可变的(immutable)字节序列, 它可以包含任意数据, 包括0值字节

Go中内置的len函数返回字符串的字节数(并符号的数目)



不可变意味着两个字符串能安全地共用同一段底层内存，使得复制任何长度字符串的开销都低廉。类似地，字符串s及其子串（如s［7:）可以安全地共用数据，因此子串生成操作的开销低廉。这两种情况下都没有分配新内存。图3-4展示了一个字符串及其两个子字符串的内存布局，它们共用底层字节数组。*切片时并不会新开辟一块内存*

```go
// 字符串字面量
// 特殊字符需要用到转义序列
"hello, 世界!"


// 原生字符串字面量
// 转义序列不起作用
`Go is a tool for managing Go source code.
Usage:
		go command [arguments]
...`
```

Unicode 字符集Go语言中的字符(assigns)被称为 文字符号(rune)

UTF-8编码方式: UTF-8以字节为单位对Unicode码点作边长编码, 用1-4个字节表示字符.

`[]bytes(s)`操作会分配新的字节数组, 拷贝填入s含有的字节, 并生成一个slice引用, 指向整个数组. 

```go
// 字符串和数字相互转换

x := 123
y := fmt.Sprintf("%d", x)
fmt.Println(y, strcovn.Itoa(x))
fmt.Println(sreconv.FormatInt(int64(x), 2))  // "1111011" 
```



### 常量

常量是一种表达式, 可以保证在编译在编译阶段就计算出表达式的值, 并不需要等到运行时, 从而使编译器得以知晓其值. 所有常量本质上都属于基本类型: 布尔型, 字符串或数字.

常量的用法和变量相似, 但是其值恒定不变, 以防止程序在运行过程中对其进行修改, 比如圆周率π.

```go
// 声明常量
const pi = 3.1415

// 声明一系列常量
const (
	e = 2.71828
  pi = 3.1415
)

// 数学运算, 逻辑运算后的常量
const timeout = 5 * time.Minute

// 声明具名常量
const time.Duration
const math.Pi

// 声明相同值的常量 不推荐

const (
	a = 1
  b
  c = 2
  d
)   // b=a=1, d=c=2

// 常量生成器iota 枚举类型
// iota 从0 开始取值逐项加1
type Weekday int
const (
	Sunday Weekday = iota
  Monday
  Tuesday
  Wednesday
  THursday
  Friday
  Saturday
)


```

无类型常量

<u>只有常量才可以是无类型的.</u> 

## 复合数据类型-Composite Types

> composite types

数组和结构体都是聚合类型, 它们的值是由内存中的一组变量构成.数组的元素具有相同的类型, 而结构体中的元素数据类型则可以不同. 数组和结构体的长度都是固定的.

slice和map都是动态数据结构, 它们的长度在元素添加到结构中时可以动态增长. 

### 数组-Arrays

Go语言中很少使用数组, 很多场景都是使用slice.

数组组中的每个元素是通过索引来访问的.

```go
// 声明方式
var a [arrayLength]Type
var a [3]int  // [0, 0, 0]
fmt.Println(a[0])
fmt.Println(a[len(a)-1])

var q [3]int = [3]int{1, 2, 3}
var r [3]int = [3]int{1, 2}
fmt.Println(r[2])  // "0"

q := [...]int{1, 2, 3}  // 根据初始化数组元素个数决定数组的长度


// 根据索引创建值
type Currency int
	const (
		USD Currency = iota
		EUR
		GBP
		RMB
	)
symbol := [...]string{USD: "$", EUR: "€", GBP:"£", RMB: "¥"}
r := [...]int{99:3}  // 这种语法还不太熟悉我 
fmt.Println(symbol[RMB], reflect.TypeOf(symbol))
```

数组的长度是数组类型的一部分, 不同的长度的数组的数组类型时不一样的. 数组的长度必须是常量表达式.

当调用一个人函数的时候, 每个传入的参数都会创建一个副本, 然后赋值给对应的函数变量, 所以函数接受的是一个副本, 而不是原始的参数. 这种传递方式传递大的数组会很低效, 并且不会影响原始数组.这种情况下, Go把数组和其他类型都看成值传递. 而在其他的语言中, 数组是隐式地使用引用传递.



### 切片-Slices

slice表示一个拥有相同类型元素的可变长度的序列; 它看上像没有长度的数组类型.

slice是一种轻量级的数据结构, 可以用来访问数组的部分或者全部的元素, 而这个数组称为slice的**底层数组(underlying array)**.

slice有三个属性: 指针、长度(len:length)和容量(cap:capacity). 

长度: slice中的元素个数.

容量: 从slice的起始元素到底层数组的最后一个元素间的个数. 

一个底层数组可以对应多个slice, 这些slice可以引用数组的任何位置, 彼此之间的元素还可以重叠. 

指针指向数组的第一个可以从slice中访问的元素, 这个元素并一定是数组的第一个元素.

内置函数len和cap用来返回slice的长度和容量. 

<u>不同于python的切片的是, Go中不能使用复数引用, 而应该是cap(s)-i:cap(s)的方式进行切片</u>

```go
// 基本语法
var s []T

months[i:j] 
months[1:]
month[:]  // 引用数组month的所有元素


// 数组与切片的区别
a := [...]int{0, 1, 2, 3, 4, 5}  // 数组, 固定长度
s := []int{0, 1, 2, 3, 4, 5}  // slice 指向数组的slice

s == nil  // 这是被允许的比较操作, 检查s 是否为空

```

slice操作符s[i:j] (0≤i≤j≤cap(s))创建了一个新的slice, 这个新的slice引用了序列

<u>因为slice包含了指向数组元素的指针, 所以将一个slice传递给函数的时候, 可以在函数内部修改底层数组的元素.</u>

换而言之, 创建一份数组的slice等于为数组创建了一个别名.

slice特性: 无法像数组一样做比较. 不能用 `==` , 进行比较时一般需要自己编写函数.

```go
// 使用make函数创建slice
// 其实make创建了一个无名数组, 并返回了它的一个slice;
make([]T, len)  // 长度和容量相等
make([]T, len, cap)



// append函数示例
var runes []rune
for _, r := range "Hello, 世界!" {
		runes = append(runes, r)
}

runes2 := []rune("hello, 世界!")  // 这种方式也可

```

每次slice容量改变都意味着一次底层数组重新分配和元素复制.

虽然底层数组的元素是间接引用的, 但是slice的指针, 长度和容量不是. slice并不是多引用类型. 

```go
type IntSlice struct {
  ptr	*int
  len, cap int
}
```



### 映射-Maps

散列表(Hash)是设计精妙、用途广泛的数据结构之一. 它数一个拥有键值对元素的无序集合. 集合中健的值是唯一的, 键对应的值可以通过键来获取、更新或移除. 无论这个散列表有多大, 这些操作基本上是通过常量时间的键比较就可以完成.

在Go语言中, map是散列表的引用,  map的类型是`map[K]V`. map中所有的键都拥有相同的数据类型, 同事所有的值也都拥有相同的数据类型, 但键的类型和值得类型不一定相同.

<u>比较浮点数的相等性是不明智的选择.</u>

```go
// 使用make创建map
args := make(map[string]int)

// 使用map字面量创建map
args := map[string]int{
  "a": 1, 
  "b": 2, 
}

// 等价于
args := make(map[string]int)
args["a"] = 1
args["b"] = 2

// 移除map的元素
delete(args, "a")  


// 遍历map 元素的顺序不固定
for key, value := range args {
  fmt.Println(key, value)
}

// 按顺序排序map元素的方
// 使用数组来排序map的键, 然后通过数组中的键来获取值.
import "sort"

var names string
names := make([]string, 0 len(args))  // 这种方式更高效
for name := range args {
  names := append(names, name)
}
sort.Strings(names)
for _, name := range names {
  fmt.Println(name, args[name])
}

var args map[string]int

fmt.Println(args == nil)  //"true"
fmt.Println(len(args) == 0)  // "true"


arg, ok := args["a"]
 
```

使用delete删除map的元素时, 即使键不存在, 操作也是安全的

<u>map元素不是一个变量, 不能获取他的地址</u>

我们无法获取元素的地址的一个原因是map的增长可能导致已有元素被重新散列到新的存储位置, 这样就可能使得获取的地址无效. 

map类型的零值是nil, 没有引用, 引用任何散列表.

和slice一样, map不可比较, 唯一合法的比较就是和nil比较. 

Go没有提供集合类型

map的值类型本身可以是复合数据类型如map或slice.

### 结构体-Struct

结构体是将零个或多个任意类型的命名变量组合在一起的聚合数据类型. 每个变量都叫作结构体的成员.

结构体的每个成员变量(fileds)必须是唯一的

```go
// 结构体声明
type Employee struct {
  ID		int
  Name, Address	string  // 相同且连续的成员变量可以的写法
  DoB			time.Time
  Position		string
  Salary		int
  ManagerID		int
}

var demo Employee

demo.ID = 12345
fmt.Println(demo, reflect.TypeOf(demo))
pointer := &demo.ID
*pointer = 99
fmt.Println(demo.ID)

var employeeOfTheMonth *Employee = &demo
fmt.Println(employeeOfTheMonth.ID)  // 通过指正访问结构体的成员变量
struct{}  //空结构体
```

成员变得顺序对于结构体同一性很重要. 在组合成员变量(Name, Address)时一般按照具体相关性来.

聚合类型(结构体, 数组)不可以包含类型自己. 但是可以包含该类型(S)的指正类型类型(*S)

结构体零值由结构成员的零值组成. 

没有任何成员变量的结构体称为**空结构体(struct{})**

#### 结构体字面量

```go
// 结构体字面量
type Point struct{X, Y int}  // 方式一 不常用
p := Point{1, 2}  // 必须按顺序, 且每给字段都需要指定值
// 上述声明方式的结构体扩展和维护性较差
type  T struct{a, b int}  // a b 不可导出

// 方式二 通过指定部分或全部成员变量的名称和值来初始化结构体
anim := gif.GIF{LoopCount: nframes}
p := Point{Y:2}  可以不指定值, 也可以不按顺序制定

type Vertex struct {
	X, Y int
}

var (
	v1 = Vertex{1, 2}  // has type Vertex
	v2 = Vertex{X: 1}  // Y:0 is implicit
	v3 = Vertex{}      // X:0 and Y:0
	p  = &Vertex{1, 2} // has type *Vertex
)
```

结构体类型的值可以作为参数传递给函数或者作为函数的返回值.

```go
func Scale( p Point, factor int) Point {
  return Point(p.X * factor, p.Y * factor)
}
```

出于效率考虑, 大型的结构体通常都使用结构体指针的方式直接传递给函数或者从函数中返回

```go
func Bonus( e *Employee, percent int) int {
  return e.Salary * percent / 100
}
// 传递指针比直接传递值更有效率
```

由于通常结构体都通过指针的方式使用, 因此可以使用一种简单的方式来创建、初始化一个类型struct类型的变量并获取它的地址: 

```go
pp := &Point{1, 2}

// 等价于
pp := new(Point)  // 新建指针
*pp = Point{1, 2}

```



#### 结构体比较

<u>如果结构体的所有成员变量都可以比较, 那么这个结构体是可比较的.</u>

可比较的结构体类型都可以作为map的键的类型.

```go
// == != 
type address struct {
  hostname string
  port int
}
hits := make(map[address]int)
hits[address{"golang.org", 443}]++
```

#### 结构体嵌套和匿名成员

> struct embedding and anonymous fields

Go允许我们定义不带名称的结构体成员, 只需要指定类型即可, 这种结构体成员称作匿名成员. 这个结构体成员的类型必须是一个命名类型或指向命名类型的指针.

```go
type Circle struct {
  Point  // Point Point
  Radius int
}

var c Circle
c.X = 8
c.Y = 8
c.Radius = 5

// 结构体字面量初始化
c = Circle{Point{8, 8}, 5}
c = Circle{Point: Point{8, 8}, 5)
```

任何命名类型或指向命名类型的指针都可以在结构体中嵌套使用

因为“匿名成员”拥有隐式的名字，所以你不能在一个结构体里面定义两个相同类型的匿名成员，否则会引起冲突。由于匿名成员的名字是由它们的类型决定的，因此它们的可导出性也是由它们的类型决定的。在上面的例子中， Point和Circle这两个匿名成员是可导出的。即使这两个结构体是不可导出的（point和circle），我们仍然可以使用快捷方式:`w.x=8//等价于w.circle.point.x =8` 但是注释中那种显式指定中间匿名成员的方式在声明circle和point的包之外是不允许的，因为它们是不可导出的。

到目前为止，我们所看到关于结构体嵌套的使用，仅仅是关于点号访问匿名成员内部变量的语法糖。后面我们将了解到匿名成员不一定是结构体类型，任何佥名类型或者指向命名类型的指针都可以。不过话说回来，嵌套一个没有子成员的类型有什么用呢？

以快捷方式访问匿名成员的内部变量同样适用于访问匿名成员的内部方法。因此，外围的结构体类型获取的不仅是匿名成员的内部变量，还有相关的方法。这个机制就是从简单类型对象组合成复杂的复合类型的主要方式。在Go中.

<u>在Go中, 组合(composition)是面向对象编程方式的核心.</u>

### JSON



JSON的数组用来编码Go里面的数组和slice.

JSON的对象用来编码Go里面的map(键为字符串类型)和结构体.

只有可导出的成员可以转换为JSON字段, 所以Go结构体里面的所有成员都应该首字母大写. 

字段标签

```go
//json : js to go

```

解析json时, JSON字段的名称关联到Go结构体成员的名称是忽略大小写的

### 文本和HTML模板

`text/template` 和 `html/template`, 提供了一种机制, 可以将程序变量的值带入到文本或者HTML模板中. 

模板是一个字符串或者文件, 操作: `{{...}} `. 操作可以引发其他行为. 每个操作在模板语言里都对应一个表达式, 提供的简单但强大的功能包括: 输出值, 选择结构体成员, 调用函数和方法, 描述控制逻辑, 实例化其他的模板等. 

## 函数-Functions

函数包含连续的执行语句, 可以在代码中通过调用函数来执行它们. 

函数能够将一个复杂的工作切分成多个更小的模块, 使得多人协作变得更加容易.

函数对它的使用者隐藏了实现细节.

### 函数声明

```go
// 函数声明语法
func name(parameter-list) (result-list) {
    body
}

// 多返回值函数
func val() (int, int) {
    return 3, 7
}

func add(x int, y int) int {return x + y}  // 返回表达式
func sub(x, y int) (z int) { z = x - y return}  // 返回值命名
func first(x int, _ int) int { return x}  // 未使用参数
func zero(int, int) int {return 0}
```

如果一个函数既省略返回列表也没有任何返回值, 那么设计这个函数的目的是调用函数之后的附加效果.

当函数存在返回列表是, 必须显式地以return语句结束.

返回值也可以像形参一样命名. 这个时候, 每个命名的返回值会声明为一个局部变量, 并根据变量类型初始化为相应的零值.

函数的类型称作 **签名(signature)** . 当两个函数拥有相同的形参列表和返回列表时, 认为这两个函数的类型或签名是相同的. 形参和返回值的名字不影响函数类型, 采用简写同样也不影响函数类型. 

每一次调用函数都需要提供实参来对应函数的每一个形参, 包括参数的调用顺序也必须一致. 

Go语言语言没有默认参数值的概念也不能指定实参名, 所以除了用于文档说明之外, 形参和返回值的命名不会对调用方有任何影响. 

实参是按值传递的, 所以函数接收道德是每个实参的副本; 修改函数的形参变量并不会影响到调用者提供的实参. 

使用引用类型如: 指针、slice、map、function或channel作为实参时, 可能会间接修改实参变量.

偶尔会看到有些函数的声明没有函数体, 那说明这个函数使用了除Go以外的语言实现. 这样的声明定义了该函数的签名signature.

```go
package main
func Sin(x float64) float64  // 使用汇编语言实现
```

### 递归-Recursion

函数可以使用递归调用(调用函数本身), 这意味着函数可以直接或间接地调用自己. 

递归是一种实用技术, 可以处理许多带有递归特性的数据结构. 

### 多返回值

### 错误-Error

### 函数变量

### 匿名函数

### 变长函数

### 延迟函数调用

### 宕机

### 恢复

## 方法-Methods

```go
// 函数调用与方法调用

p := Point(1, 2)
q := Point(4, 6)
fmt.Println(Distance(p, q))  // 函数调用
fmt.Println(p.Distance(q))  // 方法调用
```

### 方法声明

方法的声明和普通函数的声明类似, 只是在函数名字前面多了一个参数. 

这个参数把这个方法绑定到这个参数对应的类型上.









## 接口-Interfaces

接口类型时对其他类型行为的概括与抽象. 通过使用接口, 我们可以写出更加灵活和通用的函数, 这些函数不用绑定在一个特定的类型实现上. 

Go语言的接口是隐式实现的(类似Python的魔术方法, 或JavaScript的直接量, 只要满足特定范式即可, 而不是显式地声明接口). 换句话说, 对于一个具体的类型, 无须声明它实现了哪些接口, 只要提供接口所必须的方法即可.

这种设计让你无须改变已有类型的实现, 就可以为这些类型创建新的接口, 对于那些不能修改包的类型, 这一点特别有用.

> 接口类型的基本机制类型价值. 
>
> 标准库中集中重要的接口.
>
> 类型断言, 类型分支
>
> 实现另一种类型的通用化

### 接口即约定(contract)

之前介绍的类型都是具体类型(concrete types). 具体类型指定了它所含数据的精确布局(值表示方法, 操作方法), 还暴露了基于这个精确布局的内部操作. 

具体类型还会通过其他方法来提供额外的能力.

总之如果你知道了一个具体类型的数据, 那么你就精确地知道了它是什么以及它能干什么. 

Go语言中还有另外一种类型称为 **接口类型(interface type)**. 接口是一种 **抽象类型(abstract type)**, 它并没有暴露所含数据的布局或者内部结构, 当然也没有那些数据的基本操作, 它所提供的仅仅是一些方法而已.

```go
// fmt.Printf把结果发到标准输出standard output(标准输出其实是一个文件)
// fmt.Sprintf返回一个string类型的值. 将对象转换为字符串, 作为一种格式输出
package fmts
fmt Fprintf(w io.Writer, format string, args ...interface{}) (int err)
```



```go
package io

// Writer接口封装了基础的写入方法
type Writer interface {
    /*
    Write从p像底层数据流写入len(p)个字节的数据
    返回实际写入的字节数(0<= n <= len(p)
    如果没有写完, 那么会返回遇到的错误
    在Write返回 n < len(p)时, err必须为非nil
    Write 不允许修改p的数据, 即使是临时修改
    */
    
    // 实现时不允许残留p的引用
    Write(p []byte) (n int, err error) 
    
}
```

io.Writer接口定义了Fprintf和调用者之间的约定.

### 接口类型

一个接口类型定义了一套方法, 如果一个具体类型要实现该接口, 那么必须实现接口类型定义中的所有方法.

```go
package io

type Reader interface {
    Read(p []byte) (n int, err error)
}

type Closer interface {
    Close() error
}

// 组合已有接口得到新的接口

type ReadWriter interface {
    Reader
    Writer
}

//嵌入式接口
type ReaderWriterCloser interface {
    Reader
    Writer
    Closer
}
```

### 实现接口

如果一个类型实现了一个接口要求的所有方法, 那么这个类型实现了这个接口. 

Go程序员通常说一个具体类型"是一个"(is-a)特定的接口类型, 这其实代表着该具体类型实现了该接口.

## 协程和通道-goroutine and channel

> 开销更小的并发能力.
>
> 并发编程: concurrent programming
>
> 顺序编程: sequentialpProgramming
>
> 协程的本质是用户态线程

**并发编程表现为程序由若干个自主的活动单元组成**, 它从来没有像今天这样重要. 

Web服务器可以一次处理数千个请求.平板电脑和手机应用在渲染用户界面的同时, 后端还同步进行着计算和处理网络请求. 

甚至传统的批处理任务——读取数据、计算、将结果输出——也使用并发来隐藏I/O操作的延迟, 充分利用现代的多核计算机, 内核的个数每年变多, 但是速度没什么变化.

Go具有两种并发编程风格

第一种, 协程和通道, 通信顺序进程(Communicating Sequential Process, CSP), CSP是一个并发的模式, 在不同的执行体(goroutine)之间传递值, 但是**变量本身局限于单一的执行体**.

第二种, 共享内存多线程(shared memory multithreading)的传统模型.

即使Go对并发的支持是其很大的长处, 并发编程本质上也比顺序编程要困难一些, 从顺序编程获取的直觉让我们加倍地迷茫.

### goroutine

> goroutine具有并发性, 同时运行.

在Go里, 每一个并发执行的活动称为goroutine. 

当一个程序启动时, 只有一个goroutine来调用main函数, 称它为主goroutine. 新的goroutine通过go语句进行创建.

语法上, 一个go语句是在普通的函数或者方法调用前加上go关键字前缀. 

```go
f()  // 调用 f(); 等待它返回
go f()  // 新建一个调用f()的goroutine, 不用等待
```

除了从main返回或者退出程序之外, 没有程序化的方法让一个goroutine来停止另一个, 但是有办法和goroutine通信来要求它自己停止. 

### channel

goroutine是Go程序并发的执行体, channel就是它们之间的连接. 

通道是可以让一个goroutine发送特定值到另一个goroutine的通信机制. 

每一个channel是一个具体类型的导管, 叫作channel的元素类型. 一个有int类型的通道写为 `chan int`.

和map一样, channel是一个使用make创建的数据结构的引用. 通道的零值是nil. 同种类型的channel可以使用==进行比较

```go
// 使用内置的make函数来创建一个channel
ch := make(chan int)
```

通道有两个主要操作: 发送(send) 和接收(receive), 两者统称为通信(communications).

send语句从一个goroutine传输一个值到另一个在执行接收表达式的goroutine. 两个操作都是用 `<-` 操作符书写

```go
ch <- x  // 发送语句
x = <- ch  // 赋值语句中的接收表达式
<- ch  // 接收语句, 丢弃结果
close(ch)  // 关闭通道, 不再能够通过ch传递值
```

通道支持第三个操作: 关闭(close), 它设置了一个标志位来指示值当前已经发送完毕, 这个channel后面就没有值了; 关闭后的发送操作将导致宕机.



使用简单的make调用创建的channel叫无缓冲通道(unbufferd channel), 但make还可以接受第二个可选参数, 一个表示通道容量的整数

```go
ch = make(chan int)
ch = make(chan int, 0)
ch = make(chan int, 3)  // 容量为3的缓存通道
```

#### 无缓存通道

无缓存通道上的发送操作将会阻塞, 直到另一个goroutine在对应的通道上执行接收操作, 这时值传送完成, 两个goroutine都可以继续执行. 

相反, 如果接收操作先执行, 接收方goroutine将阻塞, 直到另一个goroutine在同一个channel上发送一个值.



<u>使用无缓冲通道进行的通信导致发送和接收goroutine同步化(synchronize)</u>, 无缓冲通道也称为同步(synchronous)通道. 当一个值在无缓冲通道上传递时, 接收值后发送方goroutine才被再次唤醒. 

通过channel发送消息有两个重要的方面需要考虑. 每条消息有一个值, 但有时候通信本身以及通信发生的时间也很重. 当我们强调这方面的时候, 把消息叫作**事件(event)**. 当事件没有携带额外的信息时, 它单纯的目的是进行同步. 

> 通常使用 bool 或 int类型的通道

#### 管道-pipeline

> 一个抽象概念

通过可以用来连接goroutine, 这样一个的输出是另一个的输入. 这个链路叫管道(pipeline)

3个goroutine由两个channel连接成一个三级管道(three-stage pipeline)

通道关闭后, 任何后续的发送操作将会导致应用崩溃. 当关闭的通道被读完后, 所有后续的接收操作顺畅进行, 只是获取到的是零值. 

#### 单向通道类型

#### 缓冲通道

缓冲通道有一个元素队列, 队列的最大长度在创建的时候通过make的容量参数来设置.

缓冲通道上的发送操作在队列的尾部插入一个元素, 接收操作从队列的头部移除一个元素. 

如果通道满了, 发送操作会阻塞所在的goroutine直到另一个goroutine对它进行接收操作来流出空间.

反过来, 如果通道是空的, 执行接收操作的goroutine阻塞, 直到另一个goroutine在通道上发送数据. 

```go
// 当channel为空时可以无阻塞地发送三个值
ch = make(chan string, 3)
ch <- "A"
ch <- "B"
ch <- "C"

fmt.Println(<- ch)  // "A"
fmt.Println(cap(ch))  // 获取通道容量
fmt.Println(len(ch))  // 获取通道长度
```

#### 使用select多路复用

> multiplexing with select

```go
select {
    case <- ch1:
        // ...
    case <- ch2:
        // ...
    case <- ch3:
        // ...
    default:
        // ...
}
```



## 并发-concurrence

> 并发编程的重要难题和陷阱
>
> 使用共享变量实现并发 concurrency with shared memory

### 竞态-race conditions

在串行程序(sequential program)中(即一个程序只有一个goroutine), 程序中各个步骤的执行顺序由程序逻辑来决定. 比如, 在一系列语句中, 第一句在第二句之前执行, 以此类推.

当一个程序有两个或以上goroutine时, 每个goroutine内部的各个步骤是顺序执行的, 但我们无法知道各自事件中的x和y的顺序. 如果我们无法确定事件x和事件y的先后顺序, 那么这两个事件就是**并发的(concurrent)**.



一个能在串行程序中正确工作的函数如果在并发调用时仍然能够正确工作, 那么这个函数是并发安全(concurrency-safe)的, 在这里并发调用时指, 在没有额外同步机制的情况下, 从两个或者多个goroutine同时调用这个函数. 

这个概念也可以推广到其他函数, 比如方法或者作用域特定类型的一些操作. 如果一个类型的所有可访问方法(methods)和操作(operations)都是并发安全时, 则称之为并发安全的类型. 



导出的包级别的函数通常可以认为是并发安全的. 因为包级别的变量无法限制在一个goroutine呢, 所以那些修改这些变量的函数就必须采用互斥机制(mutual exclusion).

**竞态是指在多个goroutine按某些交错顺序执行时程序无法给出正确的结果.**

竞态对于程序是致命的, 因为它们可能潜伏在程序中, 出现频率也很低, 有可能仅在高负载环境或在使用特定的编译器、平台和架构时才出现. 这些都让竞态很难再现和分析.  

### 互斥锁: sync.Mutex

### 读写互斥锁: sync.RWMutex

```go
var mu sync.RWMutex

var balance int
func  Balance() int {
    mu.RLock()  // 读锁
    defer mu.RUnlock()
    return balance
}
```

### 内存同步

现代计算机一般都会有多个处理器, 每个处理器都有内存的本地缓存. 为了提高效率, 对内存的写入是缓存在每个处理器中的, 只在有必要时才刷回内存. 

### 延迟初始化: sync.Once

### 竞态检测器

### goroutine与线程



## 包和go工具-Packages and go tools

通过包来实现代码的复用

包索引 http://godoc.org

>
>
>使用go工具下载、构件、运行样例程序.

任何包管理系统的目的都是通过对关联的特性进行分类, 组织成便于理解和修改的单元, 使其与程序的其他包保持独立, 从而有助于设计和维护大型程序. 

模块化允许包在不同的项目中共享、复用, 在组织中发布, 或者在全世界范围内使用.

每个包定义了一个不同的命名空间作为它的标识符. 每个名字关联一个具体的包, 它让我们在为类型、函数等选取短小而且清晰地名字的同时, 不与程序的其他部分冲突.

包通过控制名字是否导出使其对外可见来提供封装能力(encapsulation). 

go工作空间组织

```
GOPATH/
	src/  源文件
	bin/  二进制文件, 可执行程序
	pkg/  构件工具存储编译后的包的位置
```



## 测试-tests

> "我强烈地意识到我余生的很大一部分时间都将用来寻找我程序中的错误. "
>
> ### Which testing frameworks do you use regularly?
>
> built-in testing  44%  最多

<u>处理程序错误的两种常见方法: 第一种, 软件发布之前的例行同行评审; 第二种, 编写测试.</u>

测试时自动化测试的简称, 编写简单的程序来确保程序(产品代码)在该测试中针对特定输入产生预期的输出. 

这些测试通常要么是经过精心设计之后用来检测某种功能, 要么是随机性的, 用来扩大测试的覆盖面. 

Go的测试方法看上去相对比较低级. 它依赖于命令`go test`和一些能用`go test`运行的测试函数编写约定. 

实际上, 编写测试代码和编写原始程序并没有什么不同. 我们编写聚焦于任务的部分功能的简单函数. 

我们必须谨防**条件边界**, 思考**数据结构**, 并且合理地设计如何**根据合适的输入得到输出**. 这和编写常规的Go代码没有区别, 这不需要新的注解(notations)、约定(conventions)和工具(tools). 

### go test 工具

`_test.go`结尾的文件不是go build命令编译的目标, 而是`go test`的编译目标.



在 `*_test.go` 文件中, 三种函数需要特殊对待, 即 **功能测试函数**, **基准测试函数** 和 **示例函数** .

**功能测试函数**: 以`Test`前缀命名的函数, 用来检测一些程序逻辑的正确性, `go test` 运行测试函数, 并报告结果是 `PASS` 还是 `FAIL` . 

**基准测试函数**: 以 `Benchmark` 开头, 用来测试某些操作的性能, `go test` 汇报操作得物平均执行时间.

**示例函数**: 以`Example` 开头, 用来提供机器检查过的文档. 



<u>`go test` 工具扫描 `*_test.go` 文件来寻找特殊函数, 并生成一个临时的main包来调用它们, 然后编译和运行, 并汇报结果, 最后清空临时文件.</u> 

### Test 函数

每一个测试文件必须导入 testing 包. 这些函数的函数签名如下:

```go
func TestName(t *testing.T) {
    // ...
}

func TestSin(t *testing.T) { /* ... */ }  // Test后的后缀名必须首字母大写
```

 <u>功能测试函数必须以Test开头, 可选的后缀名称必须以大写字母开头</u>



## 反射-reflection

## 低级编程

# Go面试题

> 参看xmind文档

