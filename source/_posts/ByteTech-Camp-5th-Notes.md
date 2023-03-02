---
title: 第五届字节跳动青训营伴学笔记
date: 2023-03-01 23:22:40
author: 参加了字节青训营的 aldlss
categories:
- 心得
tags: 
- 青训营
- Go
updated: 2023-03-01 23:25:20
description: 备份一下
---

这个是今年寒假参加字节青训营的时候写的伴学笔记，共有 4 篇。原发布于掘金社区，现全部汇总并备份到这里。

<!-- more -->
***

# Go 语言基础语法特点及感想

之前也写过一些别的语言，因此就写一些 Go 语言语法里个人感觉比较有特点的地方吧。

## 基础语法

### 变量和常量

声明变量有两种方法

1. 使用 `var` 声明： 
```go
var a int = 1
//声明 a 为 int 类型并赋值为 1
```

类型可推断的情况下可以不写出变量类型

使用 `:=` 声明并赋值：
```go
a := 1
//声明 a 并赋值为 1
```

常量可自动推断变量类型：
```go
const a := 1
```
但这不代表其是可变类型，若不同语句推断出的类型有冲突，还是会报错的

### 条件判断

`if` 判断的表达式不用加小括号，必须在同一行写大括号，然后换行写语句：
```go
if 9%2 == 0 {
    fmt.Println("9 is even")
}
else {
    fmt.Println("9 is odd")
}
```

### 循环

只有 `for` 语句，没有 `while`，不过 `for` 有多种用法：
1. 经典用法：
```go
for i := 1; i < 10; i++ {
    fmt.Println(i)
}
```

2. 类似 `while` 的用法：
```go
for i <= 10 {
    fmt.Println(i)
    i += 2
}
```

3. 类似 `while(true)` 的用法：
```go
for {
    fmt.Println("Loop")
}
```
同样的，没有小括号

### switch

C++里，写 `switch` 最折磨的就是每次 `case` 之后都需要使用 `break`，因为不需要 `break` 的情况实在是远少于需要的情况。

也许正是因此，Go 语言的 `switch` 是默认自带 `break` 的，不需要每次都写 `break` 了，如果真有不 `break` 的需求，也可以通过在 `case` 语句的最后加上 `fallthrough` 来使之能执行到后面的语句。大概是刚好相反了。

同时，使用上也有少许区别，如下：
```go
switch val1 {
    case val2:
        ...
    case val3:
        ...
    default:
        ...
}
```

值 val1 不需要括号括起来，val2 val3 不一定必须是常量，也可以是变量，甚至可以是表达式，但必须与 val1 的类型一致，或结果一致。有一种用法，就是省略 val1 而在 val2 val3 写表达式，不过这种写法其实也就是把 val1 的值默认为 true 然后省略了而已。没错，val1 也可以为常量。

### 数组

同样也是长度固定的，不过声明方法有所不同，中括号放在类型前面：
```go
var a [7]int
```

### 切片

可以认为是可变长度的数组，可以使用 `make` 生成并指定一个初始长度：
```go
s := make([]string, 7)
```
也可以用类似生成数组的方法生成：
```go
s := []string{"S", "a", "t", "o", "r", "i"}
```
同时，由于使用函数伸缩切片长度时可能会更改原指针的位置，所以必须要接收函数的返回值作为新的切片指针。

访问切片可以像 Python 一样使用 `s[a:b]` 的方法，但是与 Python 不同的是不能使用负值。

值得注意的是，切片的变量类型是 `[]Type`，与数组的区别大概就是中括号里有没有填入数字吧。

### map

有些类似于 C++ 的 map，不同的是其内部是无序的，既不是按键值排序，也不是按插入顺序排序。

其可以用 make 生成，也可以使用 `map[Type]Type{}` 生成并初始化。声明 map 的这个写法我其实挺喜欢的，比较直观。

### range

主要用于遍历，和 `for` 结合起来使用大概类似于 `foreach` 的感觉：
```go
for i, num := range nums {
    fmt.Println(i, num)
}
```
同样，`range` 后不需要使用小括号，看起来 Go 似乎似乎很少在语法上用到小括号的样子（？

### 函数

```go
func add(a int, b int) (int, error) {
    return a + b, nil
}
```
函数要以关键字 `func` 开头，同时返回值放到后面。值得注意的是，Go 原生支持返回多个值，而一般编写时，往往函数会返回两个值，第一个值是函数的结果，第二个值用于判断函数是否正常运行。

值得注意的是，在 Go 中，函数并不支持重载。

### 指针

类似 C，但用途有限，可用于需要修改修改函数传递的参数时。

### 结构体

```go
type user struct {
    name     string
    password string
}
```
以 `type` 开头，不过声明结构体主要是在 `struct` 以及后面，`type` 其实发挥着将声明的 `struct` 命名为 user 的作用（可以这么理解）。有意思的是，Go 似乎会强制结构体内变量的类型声明对齐，这样确实整洁不少。

### 结构体方法

```go
func (u user) check(password string) bool {
    return u.password == password
}
```
跟声明函数类似，不过在 `func` 与函数名之间添加了结构体的的信息，这种分离结构体方法和属性的操作我觉得还是挺不错的。

不错的是，如果把 `(u user)` 改为 `(u *user)`，那么在使用时就会自动将结构体指针传入，也就可以更改结构体的值了，这点还是比较智能的。

### 错误处理

之前说过，函数值一般会返回两个值：
```go
val, err := function(a)
if err != nil {
    fmt.Println(err)
    return
} 
```
所以一般就用如上语句判断是否有错误产生，只要 `err` 为 `nil`，一切都会好起来的。由于基本上每执行个函数都需要进行这样的判断，所以到后期，这种重复的判断错误的语句数量其实是非常可观的。

### 字符串操作

我的评价是，看文档。

### 字符串格式化

三个用法
```go
fmt.Printf("值:%v 较详细的值:%+v 很详细的值:%#v",val,val,val)
```
使用 `%v` 可以不用管传入的是什么值，当然若是想用 `%d` `%f` 也可以

### JSON 处理

可以结构体和 JSON 互转，不过结构体内的每个公开字段的首字母需要为大写。不过也可以用在字段后跟 `` `json:"xxx"` `` 的 tag 使之在 JSON 中用其他写法

### 时间处理

谨记 `2006-01-02 15:04:05`

### 数字解析

具体函数在 `strconv` 中，我的评价还是看文档。

### 进程信息

```go
fmt.Println(os.Getenv["PATH"])
os.Setenv("name", "Satori")
exec.Command("command","arg1","arg2")
```
具体如上，感觉还是挺简单方便的

## 实战案例

### 猜谜游戏

主要是学习基本的输入输出以及判断

### 抓包

不得不说，看完只有感叹： Go 进行网络操作确实方便啊。

也通过讲解知道了两个不错的工具：[curlconverter](https://curlconverter.com/)、[JSON转Golang Struct
](https://oktools.net/json2go)

### SOCKS5 代理

没想到这么快就快进到感觉很高级的功能了，不过侧面也说明 Go 语言进行网络操作是很方便的。

主要是需要进行鉴权 `auth` 和 连接 `connect` 的操作，然后就是对报文的处理也比较需要耐心。

***

# 进程、线程和协程，并发和并行

今天是工程实践，讲了我觉得是 Go 语言最重要的特性 `goroutine`。
想要明白这究竟是个什么，我想还是有必要了解下面这些东西的。

## 进程、线程、协程

说起来，现在一共有三个程，进程、线程、协程。

### 进程

进程还是比较好区分的，一般来说，双击打开一个应用，就是启动了一个进程，而这个在这个进程内部一般也只能创建线程，除非调用系统相关函数进行操作。而进程之间也是内存不共享的，基本上要做到进程间通信是没有那么方便的

### 线程

线程是包含在进程里的，它才是进程中的实际运作单位。我们平常写 C++ 之类的语言，main 函数一般就是属于一个主进程。而我们创建的 thread，就是主线程所创建的子线程。

线程的好处在于同一个进程的线程之间是可以共享内存的，因此可以比较方便地进行数据传输，至于由此引起的数据竞争的问题，那就是后话了。

如果主线程要结束了，那么子线程也是必定需要结束的。这就告诉我们在退出主线程之前想想子线程的事情有没有做完，没做完还是老老实实等吧。比起主线程死亡带着其他的子线程跟着暴毙，还是优雅点地退出比较好。

### 协程

goroutine 就属于协程。协程的话，我之前一度以为这是 Go 语言创造出来的一个概念，因为在 Go 之外基本没怎么听说过。后来才知道原来是我孤陋寡闻了，协程的概念在很早之前就有了，而且即使是这十几年来协程也不是由 Go 语言首先应用的。

不过我觉得就对协程的喜爱程度来说，可能无语言能出 Go 其右了，只需要一个 `go`，便能创建出一个协程。它对于协程喜爱至深，以至于程序启动的 main 函数，其实也是一个协程，甚至是主协程！

虽然协程经常被说是轻量级的线程，但我觉得“线程”这两个字总不免会让人觉得各个协程之间是并行的，然而实际上它们是在同一个线程里并发执行的。

## 并发和并行

下面说说并发和并行的区别

关于并发和并行的区别，我认为下面这张图还是能比较好地说明的：

![1](https://fastly.jsdelivr.net/gh/Ayaloia/ImgHosting/picQQ%E5%9B%BE%E7%89%8720230117011906.png)

图中，上方的是并发，下方的是并行。

可以把每行队列看做是一个单独的任务，咖啡机则是 CPU 核心（实际上并不完全准确，但也可以这么认为），一般也就是对应着一个线程。

并发就是多个任务同时要使用一个线程。但一个时间点只能有一个任务被线程执行，所以在别的任务暂时不需要执行的时候，就可以把资源抢过来执行自己的任务；而并行则是多个任务各自享有一个线程，它们的任务是同时执行的，不会和其他任务有执行的冲突。也正是因此，也就只有多核处理器才会真正有并行的能力，否则一般也都只是并发。

之前看到别人说过的一句话：“并发是一个时间段上有多个任务执行，并行则是一个时间点有多个任务执行。”我颇以为妙。


至于更深层次的内容，以及其他的内容，有大佬不仅写得比我好，也写得比我多，所以我就结合我的认识只写了这一点。因此如果这篇笔记能对你有帮助的话，我就很高兴了。

***

# Go 三件套及作用，ORM、RPC 讲解

今天直播课讲了 Go 三件套，不过比起知道怎么使用框架，我觉得知道框架的应用场景更重要。

## Gorm

Gorm 是什么？它在 Github 上的介绍是这样说的："The fantastic ORM library for Golang"，即 Go 语言的优秀 ORM 库。

那么问题又来了，什么是 ORM？

ORM 全称 "Object Relational Mapping"，翻译过来就是“对象关系映射”。“对象”指的是什么？没错，就是我们经常所说的面向对象编程里的对象。关系是什么？我认为就是关系型数据库。那么 ORM 的作用就可以理解为是在代码里的对象和关系型数据库里的数据之间打通了一个通道，方便我们将它们之间互相转换。

可能我说得有点不清楚，接下来我讲一下有 ORM 和没有 ORM 的操作上的区别，可能会比较好理解。

我们知道，一般使用例如 SQLite、MySQL 之类的关系型数据库进行增删改查等操作时，不可避免的就是要编写 SQL 语句。而说到 SQL，毕竟再怎么说，它也是一种编程语言，而且还和我们平常学的高级语言不太一样。也就是说，需要一定的学习成本。

而在使用的时候，我们还需要编写一段字符串，然后把这段字符串，输入到数据库中。不知道各位有没有过这样的感觉，不过我是觉得这样以字符串输入命令的方式很虚渺，而且有时候因为没有编辑器的提示也很没底。这还是不谈一不注意就会有 SQL 注入攻击等其他问题的情况了。

这就导致了无论是在编写上使用上，直接使用 SQL 都有一定难度。而就在这时候，ORM，出现了。通过 ORM，我们只需要调用框架给出的方法，就可以不用自己编写 SQL 语句，像写平常的代码一样轻松实现增删改查等的功能。而且只要按规定使用，就可以避免许多因不注意或者根本不知道而导致的问题和漏洞。

当然，ORM 的优势不止这个。

我们知道，面向对象是属于软件工程里的范畴，而关系数据库则是从数学理论发展而来的，两者之间原本是并无关系的。因此如果我们要把一个对象转化为能储存在数据库里的数据，或是把数据库里的数据提取为对象，总是不免要做一番繁琐的转换操作，费时又费力。

而 ORM 则帮助我们解决了这个问题，只需要传入对象，ORM 就可以经过处理之后将相应的数据插入到数据库中，亦或是将查询的结果经过包装后直接返回创建好的对象给我们，方便又快捷。

下图简单说明了上面所提到的 ORM 的部分功能：

![ORM](https://fastly.jsdelivr.net/gh/Ayaloia/ImgHosting/picORM.drawio.png)

当然，ORM 的优势不只在于这些，不过这里就大概说这么多了。

至于 Gorm，我想如果了解了 ORM 是干什么的了话，那么上手应该也会容易吧。

## Kitex

Kitex 是什么？它在 GitHub 上的介绍是这样说的："Go RPC framework with high-performance and strong-extensibility for building micro-services"，一个由于构建微服务的具有高性能和强扩展性的 Go RPC 框架。

那么问题双来了，什么是 RPC？

RPC 全称 "Remote Procedure Call"，即远程过程调用。通过这个技术能够让我们调用网络另一端服务器的函数就像本地调用一样方便。

它是怎么做到这点的呢？简单来说，就是把要调用的函数的相关参数序列化成相应的格式发送给服务器另一端的被调用方，被调用方再反序列化接收到的数据，得到参数后经过函数得到结果，再把结果以同样的方式返还给被调用方。只要这个过程足够丝滑，那么就可以感觉像调用本地函数一样了。

整个过程可参考下图：

![RPC](https://fastly.jsdelivr.net/gh/Ayaloia/ImgHosting/pic28d77e43b38d4f73b68568bd5d3ebc69.png)

同样的，我们再讲一下 RPC 相对于本地调用的一些区别或优势。

其中一点就是 RPC 技术使得同一个工程中使用多个语言变得更加容易，因为传输参数毕竟用的是某种网络协议（这点后面会提到），由于格式统一，那么自然是可以跨语言的，就像 JSON 一样，唯一的问题可能就是得多造轮子。不过如果这样能够充分发挥到某种语言的优势或是写到自己心爱的语言，这点问题或许不大。更何况还有 RPC 框架的存在呢。

RPC 框架是什么？可以看到上图，虽说整个过程就是 RPC，但若是想实现它的话还得经过处理数据和网络通信等操作，还是有点麻烦。那么有没有一种轮子，可以让我们使用起来就像直接从第 1 步到了第 11 步，帮我们把中间的过程都包办下来了呢？答案是肯定的，这种轮子就叫做 RPC 框架，它帮助我们包办了其中第 2 步一直到第 10 步的内容，Kitex 和 gRPC 都是属于 RPC 框架的一种。

嗯，看起来好像明晰了，但真正使用起来的时候又会有其他的问题，拿 gRPC 举例（其他框架也是类似的），可能看着看着文档就又迷惑了：什么是 protobuf ？.proto 文件又是什么啊？这个 IDL 语言又是怎么回事？别急，且让我慢慢道来。

可以想象到的是，RPC 技术的难点主要就在于数据的封装与收发，我们只谈封装这部分，用 JSON 格式固然可以，但有没有更好的方法呢？或者说，能不能再造个轮子呢？Protobuf 就应运而生。

Protobuf 全称为 Protocol Buffers，它更像是一种机制或者标准。按我的理解来说，它与 JSON、XML 等格式的作用是一样的，都是用来交换数据。不过我觉得 protobuf 与它们的区别之一就在于它更偏向于在运行时交换数据使用，而不太适合储存持久化数据。为什么这么说？这就要说说它的运作机制了。

首先我们得明确 .proto 文件是什么？它是用来描述收发数据的数据结构以及要调用的函数，有了这个文件，我们就可以确定我们要调用的远程函数的函数声明，以及它所需要的一些参数和相应的数据结构的定义；而远端也可以由此确定要调用的函数以及参数的值，并确定返回值的定义。其实，也许有个更好的说法，就是接口，这个文件定义了一个或者多个接口。而编写这个文件的语言，就叫做 "IDL"，即“接口描述语言”。

值得注意的是，IDL 并不是某个特定的语言，它和 HDL（硬件描述语言）一样，是一类语言的统称。不同的框架用的序列化数据的方式不同，使用的接口描述文件也不同，因此使用的 IDL 也会不同。不过也有像 Kitex 这种支持多种传输格式的框架。

最后，gRPC 框架就会根据 .proto 文件来序列化相应的信息，并传输，接收方同样使用 gRPC 框架来接收，并也通过 .proto 文件来反序列化来得到发送的信息。

相信聪明的你也注意到了，双方是都需要安装有 gRPC 框架，这样岂不是说如果跨语言还得要跨语言轮子？以及双方在本地都要有同样的 .proto 文件，这样要注意同步文件岂不是也很麻烦？我只能说，还真是。不过 gRPC 的轮子谷歌以及造了不少了，覆盖了不少语言，实在不行还有像 Kitex 这种支持多种格式的框架。再没有的话，那还是换框架或者换语言吧，虽说可以自己造，网上也有公开的原理，不过总归还是不妥。而至于同步文件的问题，gRPC 姑且还算有一些防范的机制，具体大家还是可以看看文档。

相信看下来，也能对 RPC 以及相关的术语有所了解了。总的来说，RPC 确实比较方便，但也不是万能的，仍存在着一些限制，切不可无脑使用。

## Hertz

这个就不多说了，就是类似于 Python 里的 Django 和 Flask 这样子的一个框架。不过确实也有为微服务优化过，能为一组路由注册中间件感觉也挺方便的。说到这个中间件吧……我觉得说得有点玄乎，但实际上可能无意间就用到过很多了，比如我觉得其实这个鉴权操作，大概可以算是个中间件吧。

***

# 高质量编程与性能调优

今天讲的是高质量编程和性能调优部分，虽然讲的是 Go 语言的，但我觉得其中的很多思想都是全语言通用的。

## 高质量编程

何为高质量编程，就是使编写的代码能够达到正确可靠，简洁清晰的程度。它有三个简要的原则：

+ 简单性
+ 可读性
+ 生产力

多的理论也不谈，我觉得还是谈谈实践下来该怎么做吧。

### 编码规范

#### 代码格式

这个说起来难也不难，最重要的就是养成习惯。虽然说 Go 语言有自带的语言格式化工具，好像还是强制的，同一份代码绝不会格式化得不一样。不过这里还是说一下普遍认可的编写格式，毕竟也不是所有的语言或者 IDE 都能自动格式化。

一个非常重要就是加空格，空格的加发也很有讲究，我直到现在也没有研究完，这里就说几个我注意到的：

+ 在运算符的前后添加。比如 `c=a+b`，我们写成 `c = a + b`，会更加好一点。

+ 在逗号、冒号、分号后添加。一个经典的例子就是调用函数的时候，把 `swap(a,b)` 写成 `swap(a, b)`，这样当参数多的时候也不会出现参数挤在一起的情况，更加好分辨。

+ 在一些关键词后添加。比如 `for` `while` `if` 这种后面往往还会跟一个表达式的。

+ 在大括号前添加。这个适用于像 Go 语言这种不换行起大括号的写法，当然如果换行了那肯定没必要了。

+ 还有一个比较随性的点就是，如果觉得写得挤了，那就加个空格

另一个值得注意的就是换行，不过换行的学问倒是比较少，而且一般也有比较明确的约定和习惯。唯一一个值得注意的就是在链式调用或者其他情况的时候，如果一行写得特别长，那么适度换行也是有益于身心健康的。

#### 注释

我对注释比较惭愧，我是深受注释恩泽的，但是写注释的经验确实不多。Go 语言的注释似乎真的仅仅只有 `//` 而已，感觉相对其他语言差着点了。视频也说的不错，注释应该做的有如下四点：
    
+ 解释代码作用
+ 解释代码如何做的
+ 解释代码实现的原因
+ 解释代码什么情况会出错
    
这个说的确实有参考价值，下面讲一下我编写中我认为必须写注释的地方：

+ 函数对外的接口。这个是必须的，不然使用者云里雾里就不好了。按照比较基本的说法来说，有几点是要说的。一个是概述，简要讲讲这个函数的作用，原理也可以讲讲。另一个是参数，主要就是说明参数的意义和用法。还有就是如果有返回值的话可以把返回值的意思也说清楚。

+ 类对外的属性，要把每个属性的作用和意义都说清楚。
    
再其他的地方比如一些比较难理解的实现逻辑、用到了魔数之类的地方，也当然是要补充一下的。我是觉得注释有总比没有好，还是先考虑有没有再考虑写得好不好吧。

#### 命名规范

这个是我比较纠结的地方，经常有起名困难症。按照 Go 语言的要求，还是尽量简短点为好。不过我之前命名的时候也都比较喜欢长命名来着，顺带一提，我是小驼峰党，小驼峰是真的好看呐，有时候甚至会怀疑自己是不是为了看小驼峰而故意起两个词的名字……

不过我记得其中有一点说的挺好的，就是声明的变量离使用的地方越远，命名就要越清晰。以及要根据上下文信息来适当减少或者加长变量名，防止意义重复或者意思缺失。

#### 控制流程

一个是如果一个 `if` 分支最后是 `return`，则可以省去 `else` 不写。虽然以前写的时候隐隐约约有能 `retrun` 就 `return`，缩减缩进的想法，但我还以为是奇淫巧技，不入流的。没想到原来是正确的代码编写规范。

另一个受益匪浅的原则就是，尽量保持代码路径为最小缩进。也就是说，尽量先判断错误然后 `return`，把正确的语句留在下面，最后做到结尾是返回成功运行的值就最好了。这样一般都能优化代码结构，把缩进减到比较小的程度。我曾经听过一个说法就是：如果你的代码的缩进超过了两层以上，就说明的你的代码需要进行进一步的重构和提取了。

#### 错误和异常处理

+ 构造错误链
+ 错误包含和获取
+ 使用 `panic` 和 `recover` 对严重错误进行处理。Go 没有 try/catch 语句，因此 `panic` 和 `recover` 语句组合可以大概实现同样的功能。注：`panic` 能用尽量少用。`recover` 在当前 goroutine 的被 defer 的函数中生效

### 性能优化

主要是一些 tricks：

+ 使用 `Benchmark` 获得性能优化方向或者建议

+ 切片的切片使用的是原切片，注意因此导致的内存释放问题，可以使用 `copy`

+ `slice` 和 `map` 等构建时预分配内存会更快，即提前指定大小。

+ 字符串拼接用 `string.Buider` 更快，具体原理是其底层实现是 `[]byte`，返回时直接将 `[]byte` 转换为字符串

+ 空结构体 `struct{}` 不占内存，需要占位时用它更省内存，

+ 对某个数进行原子操作时，使用 `atomic` 包内的函数而不是使用锁会更快。具体原理是锁是系统调用， `atomic` 操作是硬件实现，效率更高。锁更适合保护一段逻辑。

## 性能调优

### 性能调优原则

+ 依靠数据而不是猜测
+ 要抓住最大瓶颈而不是细枝末节
+ 不能过早优化
+ 也不能过度优化。

### 性能分析工具 pprof

非常强力，而且可以数据可视化。

### 业务性能调优

具体可以从以下方面入手：

+ 业务服务优化。代码结构优化，整体逻辑简化。

+ 基础库优化。对于使用得多的基础库，要进行合理使用，或者更换更高效的库。

+ Go 语言优化。更换编译器，或者使用优化更深的编译参数。有点像 C++ 编译的时候 O1、O2 优化这样的感觉

***

# 其他

以上就是四篇的内容，其中很多都是与 Go 有关的，毕竟这个应该也是这次的主推。这里还有一份关于[「青训营 X 码上掘金」主题创作](https://juejin.cn/post/7174987894283894845)的主题 3 的我的解法的代码，题解原本想写的，但是当时回学校没时间，就摆了（
下面就贴出代码（不得不说好像它这个平台对 C++ 等语言不是很友好，甚至我跑不起来= =）：

```cpp
//
// Created by aldlss on 2023/2/13.
//

#include <cstdio>
#include <cmath>
int n, k, ans;
int main() {
    scanf("%d%d", &n, &k);
    // 家在后面只能步行往回走
    if(n >= k) {
        ans = n - k;
        printf("Need %d minute%s.", ans, ans==1?"":"s");
        return 0;
    }
    int onFootK, onFootStep, byBusStep, byBusK;
    do {
        printf("k: %d\n", k);
        byBusK = k / 2;
        if(k & 1) {
            onFootK = k - 1;
            if(byBusK < n) {
                byBusK += 1;
            }
            ans += 1;
        }
        else {
            onFootK = k;
        }
        onFootStep = onFootK - n;
        byBusStep = abs(byBusK - n) + 1;
        if (byBusK > n) {
            ans += 1;
            k = byBusK;
        }
        else {
            ans += std::min(byBusStep, onFootStep);
            break;
        }
    } while (true);
    printf("Need %d minute%s.", ans, ans==1?"":"s");
    return 0;
}
```

至于题解，本想说挖个坑的，但是一想到后面肯定不会填的，不如就直接说不写了吧（
![寄！](https://fastly.jsdelivr.net/gh/Ayaloia/ImgHosting/pic%E5%AF%84QQ%E5%9B%BE%E7%89%8720230301234428.jpg)_题解应该是寄了_

***

当然搞这个青训营收获最大的还是跟着写了一个项目，学会了项目架构以及其他一些东西，感觉受益匪浅。这个项目的方面届时我应该会专门写一篇出来记录一下，应该是不会咕的。其实也还有其他很多想写的，但都没来得及写，大概也都是不会咕的吧（