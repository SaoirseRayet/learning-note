<a name="index">**Index**</a>

<a href="#0">设计及架构思想</a>  
&emsp;<a href="#1">1. 编程思想</a>  
&emsp;&emsp;<a href="#2">1.1. 面向对象编程(Object Oriented Programming，OOP)</a>  
&emsp;&emsp;<a href="#3">1.2. 面向过程编程</a>  
&emsp;&emsp;<a href="#4">1.3. 函数式编程</a>  
&emsp;<a href="#5">2. 六大设计原则</a>  
&emsp;&emsp;<a href="#6">2.1. 单一职责原则</a>  
&emsp;<a href="#7">3. MVC 模式</a>  
&emsp;<a href="#8">4. BFF(Backend for Frontend)</a>  
&emsp;<a href="#9">5. 系统架构</a>  
&emsp;&emsp;<a href="#10">5.1. 单体</a>  
&emsp;&emsp;<a href="#11">5.2. 集群</a>  
&emsp;&emsp;<a href="#12">5.3. 分布式</a>  
&emsp;&emsp;<a href="#13">5.4. 微服务</a>  
&emsp;&emsp;&emsp;<a href="#14">5.4.1. 拆分原则</a>  
&emsp;&emsp;&emsp;<a href="#15">5.4.2. DDD 领域驱动</a>  
&emsp;&emsp;&emsp;&emsp;<a href="#16">5.4.2.1. 分层架构</a>  
&emsp;&emsp;&emsp;&emsp;<a href="#17">5.4.2.2. 服务</a>  
&emsp;&emsp;&emsp;&emsp;&emsp;<a href="#18">5.4.2.2.1. 模型</a>  
&emsp;&emsp;&emsp;&emsp;&emsp;<a href="#19">5.4.2.2.2. 聚合</a>  
&emsp;&emsp;&emsp;&emsp;&emsp;<a href="#20">5.4.2.2.3. 工厂</a>  
&emsp;&emsp;&emsp;&emsp;&emsp;<a href="#21">5.4.2.2.4. 资源库</a>  
&emsp;&emsp;&emsp;&emsp;<a href="#22">5.4.2.3. 界定的上下文</a>  
&emsp;<a href="#23">6. 相关资料</a>  
<a href="#24">中间件设计资料</a>  
# <a name="0">设计及架构思想</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

## <a name="1">编程思想</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="2">面向对象编程(Object Oriented Programming，OOP)</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
面向对象编程思想是以现实世界中事物，建立模型体现出来的抽象思维过程。
根据抽象的模型，依照事物之间的关系及方法进行操作，以求达到重用性、灵活性和扩展性的设计目的。
> 面向对象编程是把构成问题的事务分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描叙某个事物在整个解决问题的步骤中的行为。

OOP=对象+类+继承+多态+消息，其中核心概念是类和对象。

特点： 封装、多态、继承

### <a name="3">面向过程编程</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
面向过程编程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候一个一个依次调用就可以了。

### <a name="4">函数式编程</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
函数式编程类似于面向过程的程序设计，但其思想更接近数学计算。允许把函数本身作为参数传入另一个函数，还允许返回一个函数。是一种抽象程度很高的编程范式，纯粹的函数式编程语言编写的函数没有变量。
> 面向过程编程体现的是解决方法的步骤，而函数式编程体现的是数据集的映射。

## <a name="5">六大设计原则</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
### <a name="6">单一职责原则</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
定义：单一职责原则适用于类、接口、方法。

## <a name="7">MVC 模式</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
MVC是一种框架模式。经典MVC模式中，M是指业务模型，V是指用户界面，C则是控制器。

使用MVC的目的是将M和V的实现代码分离，从而使同一个程序可以使用不同的表现形式。其中，View的定义比较清晰，就是用户界面。

## <a name="8">BFF(Backend for Frontend)</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
BFF，即 Backend For Frontend（服务于前端的后端），也就是服务器设计 API 时会考虑前端的使用，并在服务端直接进行业务逻辑的处理，又称为用户体验适配器。BFF 只是一种逻辑分层，而非一种技术

BFF 解决了什么问题？\
前端页面时常存在，某个页面需要向 backend A、backend B 以及 backend C...... 发送请求，不同服务的返回值用于渲染页面中不同的 component，即一个页面存在很多请求的场景。
有了 BFF 这一层时，我们就不需要考虑系统后端的迁移。后端发生的变化都可以在 BFF 层做一些响应的修改。

![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/design/systemdesign/bff.png)

- 多端应用: 为不同的设备提供不同的 API，虽然它们可能是实现相同的功能，但因为不同设备的特殊性，它们对服务端的 API 访问也各有其特点，需要区别处理。
- 服务聚合：BFF 的出现为前端应用提供了一个对业务服务调用的聚合点，它屏蔽了复杂的服务调用链，让前端可以聚焦在所需要的数据上，而不用关注底层提供这些数据的服务。
- 认证、授权、请求记录等通用功能可以在BFF层实现，使用依赖包共享的方式实现。而引入额外的服务层可能导致的请求延迟的情况。

缺点：
- 在基础服务上多加了一层转发，带来了响应时间延迟
- 带来的代码重复和工作量增加

参考资料：
- [BFF —— Backend For Frontend](https://www.jianshu.com/p/eb1875c62ad3)
- [Pattern: Backends For Frontends](https://samnewman.io/patterns/architectural/bff/)
## <a name="9">系统架构</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="10">单体</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="11">集群</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="12">分布式</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="13">微服务</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

#### <a name="14">拆分原则</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
垂直划分优先原则：应该根据业务领域对服务进行垂直划分，让团队能关注业务实现。

持续演进原则： 服务数量在非必要的情况下，应该逐步划分，持续演进，避免服务数量的爆炸性增长


#### <a name="15">DDD 领域驱动</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
基本元素：分层架构、实体、值对象、服务、模块、聚合、工厂、资源库


##### <a name="16">分层架构</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/design/systemdesign/structure.png)

![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/design/systemdesign/structureIntroduce.png)

- 应用层（接入层）：通常用来接收前端（展现层）的请求，转发给领域层获取请求结果，再组装结果返回前端。
- 基础设施层：作为其他层支撑的存在，最通俗的例子就是searchServ，正常的搜索服务都会集成ElasticSearch或者其他搜索功能，searchSearch封装了与基础服务集成的及细节，只暴露了领域需要的接口。

##### <a name="17">服务</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
当一个操作凸现为一个领域中的重要概念时，就需要为它建立一个服务了。以下是服务的 3 个特征：
1. 服务执行的操作涉及一个领域概念，这个领域概念通常不属于一个实体或者值对象。
2. 被执行的操作涉及到领域中的其他的对象。
3. 操作是无状态的。

> 考虑一个实际的 Web 报表应用的例子。报表使用存储在数据库中的数据，它们会基于模版产生。最终的结果是一个在 Web 浏览器中可以显式给用户查看的 HTML 页面。\
用户界面层被合并成 Web 页面，允许用户登录，选择所期望的报表，单击一个按钮就可以发出请求。应用层是非常薄的一个层，它位于用户界面和领域层以及基础设施层的中间位置。它在登录操作时，会跟数据库基础设施进行交互；在需要创建报表时会和领域层进行交互。领域层中包含了领域的核心部分，对象直接关联到报表。有两个这样的对象是报表产生的基础，它们是 Report 和Template。基础设施层将支持数据库访问和文件访问。


###### <a name="18">模型</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
> 对一个大型的复杂项目而言，模型趋向于越来越大。模型到达了一个作为整体很难讨论的点，理解不同部件之间的关系和交互变得很困难。基于此原因，很有必要将模型组织进模块。模块被用来作为组织相关概念和任务以便降低复杂性的一种方法。

在设计中使用模块是一种增进内聚和消除耦合的方法。模块应该由在功能上或者逻辑上属于一体的元素构成，以保证内聚。模块应该具有定义好的接口，这些接口可以被其他的模块访问。

###### <a name="19">聚合</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
聚合是针对数据变化可以考虑成一个单元的一组相关的对象。聚合使用边界将内部和外部的对象划分开来。每个聚合有一个根。
> 这个根是一个实体，并且它是外部可以访问的唯一的对象。根可以保持对任意聚合对象的引用，并且其他的对象可以持有任意其他的对象，但一个外部对象只能持有根对象的引用。如果边界内有其他的实体，那些实体的标识符是本地化的，只在聚合内有意义。

一个简单的聚合的案例如下图所示。客户是聚合的根，并且其他所有的对象都是内部的。如果需要地址，一个它的拷贝将被传递到外部对象。
![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/design/systemdesign/aggreate.png)


###### <a name="20">工厂</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
工厂用来封装对象创建所必需的知识，它们对创建聚合特别有用。当聚合的根建立时，所有聚合包含的对象将随之建立，所有的不变量得到了强化。

###### <a name="21">资源库</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
使用一个资源库，它的目的是封装所有获取对象引用所需的逻辑。领域对象不需处理基础设施，以得到领域中对其他对象的所需的引用。只需从资源库中获取它们，于是模型重获它应有的清晰和焦点。

提供基于某种条件选择对象的方法，返回属性值符合条件的完全实例化的对象或者一组对象，继而封装实际的存储和查询技术。仅对真正需要直接访问的聚合根提供资源库。让客户程序保持对模型的关注，把所有的对象存储和访问细节委托给资源库。

数据驱动强调的是数据结构，也就是通过分析需求，来确定整体数据结构，根据表之间的关系划分服务。


##### <a name="22">界定的上下文</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
界定的上下文：主要的思想是定义模型的范围，画出它的上下文的边界，然后尽最大可能保持模型的一致性。

被创建的上下文有清晰的角色和被指明的关系。在上下文之间：
1. 共享内核（Shared Kernel）和
2. 客户-供应商（Customer-Supplier）是具有高级交互的模式。

## <a name="23">相关资料</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
[微服务拆分方法论](https://blog.csdn.net/no_game_no_life_/article/details/103390169)

# <a name="24">中间件设计资料</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
![image](https://github.com/rbmonster/file-storage/blob/main/learning-note/design/systemdesign/disk-memory.png)

通常在大部分组件设计时，往往会选择一种主要介质来存储、另一种介质作为辅助使用。就拿 redis 来说，它主要采用内存存储数据，磁盘用来做辅助的持久化。拿 RabbitMQ 举例，它也是主要采用内存存储消息，但也支持将消息持久化到磁盘。而 RocketMQ、Kafka、Pulsar 这种，则是数据主要存储在磁盘，通过内存来主力提升系统的性能。关系型数据库例如 mysql 这种组件也是主要采用磁盘组织数据，合理利用内存提升性能。

针对采用内存存储数据的方案而言，难点一方面在于如何在不降低访问效率的情况下，充分利用有限的内存空间来存储尽可能多的数据，这个过程中少不了对数据结构的选型、优化；另一方面在于如何保证数据尽可能少的丢失，我们可以看到针对此问题的解决方案通常是快照+广泛意义的 wal 文件来解决。此类典型的代表就是 redis 啦。

针对采用磁盘存储数据的方案而言，难点一方面在于如何根据系统所要解决的特点场景进行合理的对磁盘布局。读多写少情况下采用 b+树方式存储数据；写多读少情况下采用 lsm tree 这类方案处理。另一方面在于如何尽可能减少对磁盘的频繁访问，一些做法是采用 mmap 进行内存映射，提升读性能；还有一些则是采用缓存机制缓存频繁访问的数据。还有一些则是采用巧妙的数据结构布局，充分利用磁盘预读特性保证系统性能。

**总的来说，针对写磁盘的优化，要不采用顺序写提升性能、要不采用异步写磁盘提升性能(异步写磁盘时需要结合 wal 保证数据的持久化，事实上 wal 也主要采用顺序写的特性)；针对读磁盘的优化，一方面是缓存、另一方面是 mmap 内存映射加速读。**

上述这些存储方案上权衡的选择在 kafka、RocketMQ、Pulsar 中都可以看到。其实抛开消息队列而言，这些存储方案的选择上无论是关系型数据库还是 kv 型组件都是通用的。

[消息队列背后的设计思想](https://mp.weixin.qq.com/s/k8sA6XPrp80JiNbuwKaVfg)