---
title: 计算机基础知识
date: 2019-08-19 15:20:58
tags: 
	- CS

cover: https://s2.ax1x.com/2019/08/19/m1oBJH.png

---

# 计算机网络

## 进程和线程的区别

一个程序至少有一个进程,一个进程至少有一个线程。

区别:
1、进程是资源分配的最小单位，进程是可以独立运行的一段程序；
   线程是程序执行的最小单位，是CPU调度和分派的基本单位。线程自己基本上不拥有系统资源，在运行时，只是暂用一些计数器、寄存器和栈 。线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间。
2、进程有自己独立地址空间，每启动一个进程，系统就会为它分配地址空间，建立数据表来维护代码段，堆栈段，数据段，而线程是共享进程中的数据的，使用相同的地址空间，但是CPU切换一个线程的花费远比进程要小。
3、线程之间通信方式更方便，同一进程下的线程共享全局变量等数据，而进程之间的通信方式需要以通信的方式进行，
4、多线程程序中只要有一个线程死掉了，整个进程也死掉了，而一个进程死掉了，并不会对另一个进程造成影响，因为进程有自己独立的地址空间。

## 多线程

- 多线程就是指一个进程中同时有多个执行路径正在执行

## 并发与并行
- 原则上一个CPU只能分配给一个进程，以便运行这个进程。通常使用的计算机中只有一个CPU，同时运行多个进程，就必须使用并发技术。
- **并发**指在操作系统中，一个时间段中有几个程序都已处于已启动运行到运行完毕之间，且这几个程序都是在同一个CPU上面，但任意时刻点上只有一个程序在CPU上运行。通常采用时间片轮转进程调度算法，在操作系统的管理下，所有正在运行的进程轮流使用CPU，每个进程允许占用CPU的时间非常短(比如10毫秒)。**但实际上在任何一个时间内有且仅有一个进程占有CPU。**
- **并行**指果一台计算机有多个CPU，如果进程数小于CPU数，则不同的进程可以分配给不同的CPU来运行，这样，多个进程就是真正同时运行的，这便是并行。
- 但如果进程数大于CPU数，则仍然需要使用**并发**技术。
- 在Windows中，进行CPU分配是以线程为单位的，一个进程可能由多个线程组成。操作系统将CPU的时间片分配给多个线程,每个线程在操作系统指定的时间片内完成(注意,这里的多个线程是分属于不同进程的)。
- 总线程数<=CPU数量时并行运行，总线程数>CPU数量时并发运行。并行运行的效率显然高于并发运行，所以在多CPU的计算机中，多任务的效率比较高。但是，如果在多CPU计算机中只运行一个进程(线程)，就不能发挥多CPU的优势。

--------------

## 死锁的概念、原因、解决方法
参考回答：
1、死锁是指在一组进程中的各个进程均占有不会释放的资源，但因互相申请被其他进程所占用不会释放的资源而处于的一种永久等待状态。
死锁的四个必要条件：

- 互斥条件(Mutual exclusion)：资源不能被共享，只能由一个进程使用。
- 请求与保持条件(Hold and wait)：已经得到资源的进程可以再次申请新的资源。
- 非剥夺条件(No pre-emption)：已经分配的资源不能从相应的进程中被强制地剥夺。
- 循环等待条件(Circular wait)：系统中若干进程组成环路，该环路中每个进程都在等待相邻进程正占用的资源。

java中产生死锁可能性的最根本原因是：
1）是多个线程涉及到多个锁，这些锁存在着交叉，所以可能会导致了一个锁依赖的闭环；
2）默认的锁申请操作是阻塞的。

如，线程在获得一个锁L1的情况下再去申请另外一个锁L2，也就是锁L1想要包含了锁L2，在获得了锁L1，并且没有释放锁L1的情况下，又去申请获得锁L2，这个是产生死锁的最根本原因。

2、避免死锁：

- 方案一：破坏死锁的循环等待条件。
- 方法二：破坏死锁的请求与保持条件，使用lock的特性，为获取锁操作设置超时时间。这样不会死锁（至少不会无尽的死锁）。
- 方法三：设置一个条件遍历与一个锁关联。该方法只用一把锁，没有chopstick类，将竞争从对筷子的争夺转换成了对状态的判断。仅当左右邻座都没有进餐时才可以进餐。提升了并发度。

-------------

## 多线程

最开始，线程只是用于分配单个处理器的处理时间的一种工具。但假如操作系统本身支持多个处理器，那么每个线程都可分配给一个不同的处理器，真正进入“并行运算”状态。从程序设计语言的角度看，多线程操作最有价值的特性之一就是程序员不必关心到底使用了多少个处理器。程序在逻辑意义上被分割为数个线程;假如机器本身安装了多个处理器，那么程序会运行得更快，毋需作出任何特殊的调校。根据前面的论述，大家可能感觉线程处理非常简单。但必须注意一个问题：共享资源!如果有多个线程同时运行，而且它们试图访问相同的资源，就会遇到一个问题。举个例子来说，两个线程不能将信息同时发送给一台打印机。为解决这个问题，对那些可共享的资源来说(比如打印机)，它们在使用期间必须进入锁定状态。所以一个线程可将资源锁定，在完成了它的任务后，再解开(释放)这个锁，使其他线程可以接着使用同样的资源。
多线程是为了同步完成多项任务，不是为了提高运行效率，而是为了提高资源使用效率来提高系统的效率。线程是在同一时间需要完成多项任务的时候实现的。

一个采用了多线程技术的应用程序可以更好地利用系统资源。其主要优势在于充分利用了CPU的空闲时间片，可以用尽可能少的时间来对用户的要求做出响应，使得进程的整体运行效率得到较大提高，同时增强了应用程序的灵活性。更为重要的是，由于同一进程的所有线程是共享同一内存，所以不需要特殊的数据传送机制，不需要建立共享存储区或共享文件，从而使得不同任务之间的协调操作与运行、数据的交互、资源的分配等问题更加易于解决。


--------------

# 数据库

## 索引

拿汉语字典的目录页（索引）打比方，我们可以按拼音、笔画、偏旁部首等排序的目录（索引）快速查找到需要的字。

> “索引是一个排序的列表，在这个列表中存储着索引的值和包含这个值的数据所在行的物理地址，在数据十分庞大的时候，索引可以大大加快查询的速度，这是因为使用索引后可以不用扫描全表来定位某行的数据，而是先通过索引表找到该行数据对应的物理地址然后访问相应的数据。”

- 优点：
	- 索引可以大大提高MySQL的检索速度。
	- （实际上，索引也是一张表，该表保存了主键与索引字段，并指向实体表的记录。）
- 缺点：
	- 过多的使用索引将会造成滥用。
	- 虽然索引大大提高了查询速度，同时却会降低更新表的速度，如对表进行INSERT、UPDATE和DELETE。因为更新表时，MySQL不仅要保存数据，还要保存一下索引文件。建立索引会占用磁盘空间的索引文件。

------------------------

# get和post的区别
https://baijiahao.baidu.com/s?id=1626599028653203490&wfr=spider&for=pc

# C++ 虚函数和纯虚函数的区别
https://www.runoob.com/w3cnote/cpp-virtual-functions.html

# C++ 面向对象三大特性 封装 继承 多态

# C++ 重载 、 重写（覆盖） 、重定义 的区别