# 操作系统

## 基本概念

计算机的硬件(或称为冯-诺伊曼模型)组成：
- 主机部分：运算器、存储器、控制器
- 外设部分：输入设备、输出设备

![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/other/operatingsystem/nuoyiman.png)

没有配置软件的计算机成为**裸机**，裸机仅仅构成了计算机系统的硬件基础。\
计算机硬件、软件以及软件的各个部分是一种层次关系。硬件在最底层，其上层是操作系统。通过操作系统供的资源管理功能和方便用户使用的各种功能，把裸机改造成功能更加强大、使用更方便的机器(通常称为虚拟机)。
> 各种实用程序和应用程序在操作系统之上，这些程序都在均以操作系统作为支撑，并向用户提供各种服务。

操作系统是裸机上的第一层软件，是对硬件功能的首次扩充。
引入操作系统的目的：
- 提供一个**计算机用户和计算机硬件系统之间的接口**，使计算机易于使用。
- **有效的控制和管理计算机系统中的中硬件和软件资源**，使之得到更有效的利用。
- 合理地**组织计算机系统的工作流程**，以改善系统性能。

![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/other/operatingsystem/os-level.png)

操作系统的特征：
1. 并发性：
   - 并行性：指两个或多个事件在同一时刻发生。宏观上在一段时间内有多道程序同时运行，但单处理器其实是交替运行，故微观上是交替执行。
   - 并发性：指两个或多个事件在同一事件间隔内发生。如哲学家思考和用餐是可以同时进行的，即两个任务并行执行。
2. 共享性。资源共享是指系统中的硬件和软件不再为某个程序所独占，而是供多个用户共同使用的。
   - 互斥共享：系统中可供共享的某些资源，一段时间内只能供一个作业使用。如打印机、队列等。
   - 同时访问：系统中另一类资源如磁盘、可重入代码，可以供多个作业同时访问。
    > 并发和共享是操作系统最基本的特征，二者互为存在的条件。一方面，资源共享是以程序并发执行为条件的。另一方面，若系统不能对共享资源进行有效管理，会影响到程序的并发执行。
3. 虚拟性：操作系统中，虚拟指的是一个物理上的实体变为若干个逻辑上的对应物，前者是实际存在的，而后者是虚拟的。
4. 异步性

操作系统基本功能 // TODO
1. 处理器管理
2. 存储器管理
3. 设备管理
4. 文件管理
5. 用户接口

### 核心态与用户态
为了避免操作系统及其关键数据(如PCB等)收到用户程序有意或无意的破坏，通常将处理器的执行状态分为两种：核心态和用户态。

- 核心态(管态、系统态)：是操作系统管理程序执行时机器所处的状态。具有较高的权限，能执行包括特权指令等一切的指令，能访问所有寄存器和存储区。
- 用户态(目态)：是用户程序执行时机器所处的状态，具有较低特权的执行状态，它只能执行规定的指令，只能访问指定的寄存器和存储区。
> 特权指令：只能由操作系统内核部分使用，不允许用户直接使用的指令，如I/O指令、设置中断屏蔽指令、清内存指令、存储保护指令和设置时钟指令。

用户态程序不能直接调用核心态程序，而是通过执行访问核心态的命令，引起中断，由中断系统传入操作系统相关的程序，例如在系统调用时，由用户态转核心态。

内核的指令操作工作在核心态，主要以下几个方面：
1. 时钟管理。向用户提供标准的系统时间。通过时钟中断的管理，可以实现进程的切换，如时间片轮转调度。
2. 中断机制。中断机制中，只有一小部分属于内核，负责保护和恢复中断现场的信息，转移控制权到相关的处理程序中。(键盘鼠标的输入、进程的管理和调度、设备驱动、文件访问)
3. 原语。原语是一些关闭中断的公用小程序。
   - 处于操作系统最底层，是最接近硬件的部分。
   - 程序执行具有原子性。
   - 这些程序的运行时间较短，调用频繁。
4. 系统控制的数据结构及处理。如进程控制块、缓存区、内存分配表。

系统调用(System call):系统调用把用户程序的请求传到内核，调用相应的内核函数完成所需的处理，并将处理结果返回给对应的应用程序。
> 操作系统提供的系统调用通常包括：进程管理、文件系统控制(文件读写操作和文件系统操作)、系统控制、内存管理、网络控制、socket控制、用户管理及进程间通信(信号、消息、管道、信号量和共享内存)
![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/other/operatingsystem/core-change.png)


### 体系结构
模块组合结构

层次结构

微内核结构

## 进程管理

### 进程
进程：在计算机操作系统中，进程是资源分配的基本单元，也是独立运行的基本单元。

进程特征：
1. 动态性：进程是程序在处理器上的一次执行过程，过程是动态的。
2. 并发性：多个进程在内存同时存在，并可以并发执行。
3. 独立性：进程是资源分配的基本单元，也是独立运行的基本单元。
4. 异步性
5. 结构特征：为了描述和记录进程的运动变化过程，为每个进程分配一个进程控制快(PCB,process control block)，每个进程都由程序段、数据段和一个进程控制块组成。

进程的组成：
1. 进程控制块(PCB)：每个进程均有一个PCB，是一个既能标识进程存在、又能刻画执行瞬间特征的数据结构。
2. 程序段：进程中能被调度程序调度到CPU上执行的程序代码段。
3. 数据段
4. 进程标识符(PID)：区别系统内其他进程
5. 进程状态
6. 进程优先级
7. CPU现场保护区：当进程因某种原因释放处理器时，CPU现场信息(如指令计数器、状态寄存器、通用寄存器等)被保存在PCB的该区域中，以便重新获得处理器后继续执行
8. 通信信息：和其他进程的通信情况
9. 家族信息：子进程
10. 占有资源清单


进程状态：就绪状态、执行状态、阻塞状态、创建状态、结束状态
![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/other/operatingsystem/process-state.png)


### 线程
线程是进程内一个相对独立的、可调度的执行单元。线程基本上不拥有资源，只拥有在运行时必不可少的资源(如程序计数器、一组寄存器和栈)，但它可以和其他线程共享进程拥有的全部资源。

线程的实现：
1. 内核级线程：依赖于内核，由操作系统内核完成创建和撤销工作的线程。内核维护进程和线程的上下文信息并完成线程切换工作。
   > 一个内核级线程由于I/O操作而阻塞时，不会影响其他线程的运行。这时，**处理器时间片分配的对象为线程**。
2. 用户级线程：不依赖于操作系统核心，由应用程序利用线程库提供创建、同步、调度和管理线程的函数来控制线程。
   > 用户级线程维护由应用程序完成，内核不需要了解用户级线程存在。用户级线程切换不需要内核特权，通常应用程序的线程调度使用非抢占式或更简单的规则。这时候处理器的时间片是分配给进程的。

**多线程模型**：

多对一模型：多个用户级线程映射到同一个内核线程。
- 优点：用户级线程的切换在用户空间即可完成，不需要切换到核心态，线程管理的系统开销小、效率高
- 缺点：当一个用户级线程被阻塞后，整个进程都会被阻塞，并发度不高。多个线程不可在多核处理机上并发运行
> 多个用户线程对应一个内核线程,该模型的线程管理是由用户空间的线程库来完成的,因此效率更高,并且高效的上下文切换和几乎无限制的线程数量.不过,如果一个线程执行阻塞系统调用,那么整个进程将会阻塞.再者,**因为任一时间只有一个线程可以访问内核**,所以多个线程不能并行运行在多处理核系统上.

一对一模型：一个用户级线程映射到一个内核级线程。每个用户进程有与用户级线程同数量的内核级线程。
- 优点：当一个线程被阻塞后，别的线程还可以继续执行，并发能力强。多线程可以在多核处理机下并行执行
- 缺点：一个**用户进程**会占用多个内核级线程，线程切换由操作系统内核完成，需要切换到核心态，因此线程管理的成本高，开销大
> 每个用户线程对应一个内核线程,该模型在一个线程执行阻塞系统调用时,能够允许另一个线程继续执行,所以对于IO密集型的场景,CPU、磁盘IO、网卡等资源利用率还是非常友好的,提供了更好的并发功能.但是对于CPU计算密集型的,会导致上下文切换,结合上面内核线程的劣势.\
> **Java的内存模型就是一对一模型** 

多对多模型：n个用户级线程映射到m个内核级线程。每个用户进程对应m个内核级线程。
- 优点：克服了多对一模型并发度不高的缺点，又可服了一对一模型中一个用户进程占用太多内核级线程，开销太大的缺点
> 多个用户线程对应多个内核线程,使得库和操作系统都可以管理线程,用户线程由运行时库调度器管理,内核线程由操作系统调度器管理,可运行的用户线程由运行时库分派并标记为准备好执行的可用线程,操作系统选择用户线程并将它映射到可用内核线程.


### 线程与进程比较
- **拥有资源**：进程为拥有系统资源的基本单元，而线程不拥有系统资源，但是线程可以访问隶属进程的系统资源
- **并发性**：进入线程的操作系统，不仅进程可以并发，而且统一进程的线程也可以并发。系统的并发度更高，大大提高了系统的吞吐量。
- **调度**：统一进程中的线程切换不会引起进程切换，而不同进程的线程切换会引起进程切换。
- **系统开销**：
   - 创建或撤销开销：由于创建或撤销进程时，系统都要为之分配或回收资源，如内存空间、I/O设备等。操作系统所付出的代价远大于创建或撤销线程是的开销。
   - 切换开销：进程切换时，涉及整个当前进程CPU环境的保存以及新进程的CPU环境的设置。而线程上下文的切换，只需要保存和设置少量寄存器的内容。多线程的同步和通信因为共享同一进程，甚至无需操作系统干预。

### 处理器调度
- 高级调度：即作业调度，按照一定策略将选择磁盘上的程序装入内存，并建立进程。
- 中级调度：即交换调度，按照一定策略在内外存之间进行数据交换。
- 低级调度：即CPU调度（进程调度），按照一定策略选择就绪进程，占用cpu执行。

调度基本原则：
1. CPU利用率
2. 系统吞吐量：单位时间内CPU完成的作业数量。
3. 响应时间：多个用户对系统进行操作，都要求在一定的时间内得到响应。
4. 周转时间：作业从提交到完成的时间间隔


调度算法：
1. 先来先服务调度算法(first-come first-serverd,FCFS) 
2. 短作业优先调度算法(shortest job first,SJF) : 把处理器分配给最快完成的作业，会导致长作业饿死。
3. 优先级调度算法：确定优先级进行调度，调度方式还可以分为抢占和非抢占的调度方式
4. 时间片轮转调度算法：一个进程在一个时间片未执行完毕，插入到队尾等待，循环直到处理完成
5. 高响应比优先算法(highest response ratio first,HSRF)：通过设置响应比公式：`响应比=(作业等待时间+估计运行时间)/估计运行时间`，解决长作业饿死问题
6. 多级队列调度算法：多个队列每个队列使用一种调度算法
7. 多级反馈队列调度算法：时间片轮转调度算法和优先级调度算法的综合，动态调整队列优先级和时间片大小。进程所在队列的优先级越高时间片越小。可兼顾多方面的系统目标，如为提高系统吞吐量和缩短平均响应周期而照顾端线程。
> 适用于作业调度的算法：先来先服务调度算法、短作业优先调度算法、优先级调度算法、高响应比优先算法
> 适用于进程调度的算法：先来先服务调度算法、短作业优先调度算法、优先级调度算法、时间片轮转调度算法、多级队列调度算法、多级反馈队列调度算法

![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/other/operatingsystem/multiple-queue-call.png)

