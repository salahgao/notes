# 问答

## TODO
- 操作系统 用户态 内核态
- 多态
- 设计模式
- AOP 实现 静态植入 静态代理 动态代理 AspectJ CGLIB
- 两个Integer的引用对象传给一个swap方法在方法内部交换引用，返回后，两个引用的值是否会发现变化 不会发生变化 为什么？

## 目录
- [memcache和redis的区别](#memcache和redis的区别)
- [JVM的一些命令](#jvm的一些命令)
- [遍历hashmap的三种方式](#遍历hashmap的三种方式)
- [为什么线程执行要调用start而不是直接run](#为什么线程执行要调用start而不是直接run)
- [ThreadLocal的使用场景](#ThreadLocal的使用场景)
- [Java有哪些锁？乐观锁 悲观锁 synchronized 可重入锁 读写锁,用过reentrantlock吗？reentrantlock与synmchronized的区别](#java有哪些锁？乐观锁-悲观锁-synchronized-可重入锁-读写锁用过reentrantlock吗？reentrantlock与synmchronized的区别)
- [线程如何退出结束](#线程如何退出结束)
- [定时器用什么做的](#定时器用什么做的)
- [时间的格式化方法](#时间的格式化方法)
- [字符串的格式化方法](#字符串的格式化方法)
- [用过spring的线程池还是java的线程池？](#用过spring的线程池还是java的线程池？)
- [IO会阻塞吗？readLine是不是阻塞的](#io会阻塞吗？readline是不是阻塞的)
- [ZooKeeper的实现机制，有缓存，如何存储注册服务的](#zookeeper的实现机制，有缓存，如何存储注册服务的)
- [Spring的监听器](#spring的监听器)
- [web.xml的配置](#webxml的配置)
- [spring的bean配置的几种方式](#spring的bean配置的几种方式)
- [Tomcat的各种配置，如何配置docBase](#tomcat的各种配置，如何配置docBase)
- [是否用过maven install。 maven test。](#是否用过maven-install。-maven-test。)
- [AOP的底层实现，动态代理是如何动态，假如有100个对象，如何动态的为这100个对象代理](#aop的底层实现，动态代理是如何动态，假如有100个对象，如何动态的为这100个对象代理)
- [两个Integer的引用对象传给一个swap方法在方法内部交换引用，返回后，两个引用的值是否会发现变化](#两个Integer的引用对象传给一个swap方法在方法内部交换引用，返回后，两个引用的值是否会发现变化)
- [Java内存模型，垃圾回收机制，不可达算法](#java内存模型，垃圾回收机制，不可达算法)
- [一万个人抢100个红包，如何实现（不用队列），如何保证2个人不能抢到同一个红包，可用分布式锁](#一万个人抢100个红包，如何实现（不用队列），如何保证2个人不能抢到同一个红包，可用分布式锁)
- [HashMap的底层实现](#hashmap的底层实现)
- [sleep和wait的区别](#sleep和wait的区别)
- [线程的状态，线程的阻塞的方式](#线程的状态，线程的阻塞的方式)
- [用hashmap实现redis有什么问题](#用hashmap实现redis有什么问题)
- [Nginx的请求转发算法，如何配置根据权重转发](#nginx的请求转发算法，如何配置根据权重转发)
- [分布式锁](#分布式锁)
- [JUnit4中的 before beforeClass after afterClass](#junit4中的-before-beforeclass-after-afterclass)

### memcache和redis的区别

主要从以下几方面来看：
- Redis支持服务器端的数据操作
- 内存使用效率
- 性能
- 数据类型支持
- 网络IO模型
- 内存管理机制

    在Redis中，并不是所有的数据都一直存储在内存中的。这是和Memcached相比一个最大的区别。

- 数据持久化支持

    Redis虽然是基于内存的存储系统，但是它本身是支持内存数据的持久化的，而且提供两种主要的持久化策略：RDB快照和AOF日志。而memcached是不支持数据持久化操作的。

- 集群
- 数据一致性 事务


- [Redis和Memcached的区别](https://www.biaodianfu.com/redis-vs-memcached.html)
- [分布式缓存Redis之与Memcached的比较](https://blog.csdn.net/u011489043/article/details/78922390)
- [Redis与Memcached的区别](https://blog.51cto.com/gnucto/998509)



### JVM的一些命令

- [jvm系列(四):jvm调优-命令大全（jps jstat jmap jhat jstack jinfo）](https://www.cnblogs.com/ityouknow/p/5714703.html)

### 遍历hashmap的三种方式

- [HashMap循环遍历方式及其性能对比](https://www.trinea.cn/android/hashmap-loop-performance/)

### 为什么线程执行要调用start而不是直接run

- [多线程为什么调用start而不是调用run方法](https://blog.csdn.net/qq_30264833/article/details/57406456)
- [为什么线程执行要调用start而不是直接run](https://www.cnblogs.com/GrimMjxCl/p/9398840.html)

### ThreadLocal的使用场景

This class provides thread-local variables. These variables differ from their normal counterparts in that each thread that accesses one (via its get or set method) has its own, independently initialized copy of the variable. 

此类提供线程局部变量。这些变量与普通变量不同，每个访问（通过其get或set方法）的线程 都有其自己的，独立初始化的变量副本。 

ThreadLocal 并不是解决并发情况下共享变量的线程安全问题。而是同一个系统中，单次执行链条上下游安全传值用的。

### Java有哪些锁？乐观锁 悲观锁 synchronized 可重入锁 读写锁,用过reentrantlock吗？reentrantlock与synmchronized的区别

Java锁
- 大部分情况是否有另外的线程在同步资源：乐观锁 悲观锁
- 多个线程竞争锁是否排队：公平锁 非公平锁
- 一个线程多个锁方法获取同一把锁：可重入锁 非可重入锁
- 多个线程能否共享锁：独占锁 共享锁

synchronized ReentrantLock 区别
1. 底层实现不同：synchronized是jvm使用系统的mutex lock来实现的 ReentrantLock是Java API层面使用CAS来实现加锁
2. 功能不同：ReentrantLock提供 等待可中断、公平锁、绑定多个条件等功能

- [不可不说的Java“锁”事](https://tech.meituan.com/2018/11/15/java-lock.html) 
- [Synchronize和ReentrantLock区别](https://blog.csdn.net/qq838642798/article/details/65441415)

### 线程如何退出结束

- [Java结束线程的三种方法](https://blog.csdn.net/xu__cg/article/details/52831127)

### 定时器用什么做的

Java Timer 使用TaskQueue（简易堆） TimerThread（单一线程）来实现的，更多查看以下内容

- [定时器的几种实现方式](https://juejin.im/post/5c4d3d1af265da6151151846)

### 时间的格式化方法
```java
SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
String str = simpleDateFormat.format(new Date()); //2019-10-14 14:52:19
```

### 字符串的格式化方法
```java
String s = String.format("Hi,%s", "Alice");
```
### 用过spring的线程池还是java的线程池？

- [深入理解 Java 线程池：ThreadPoolExecutor](https://juejin.im/entry/58fada5d570c350058d3aaad)
- [Spring线程池和JDK线程池的区别及与FutureTask配合使用得到任务执行结果](https://blog.csdn.net/zmx729618/article/details/69526323)
- [Java 四种线程池的用法分析](https://blog.csdn.net/u011974987/article/details/51027795)

### IO会阻塞吗？readLine是不是阻塞的

IO会阻塞，readLine是阻塞的

- [IO - 同步，异步，阻塞，非阻塞](https://blog.csdn.net/historyasamirror/article/details/5778378)
- [Java Socket通信BufferedReader.readLine()阻塞问题](http://blog.stayzeal.cn/2018/04/02/Java-Socket通信BufferedReader-readLine-阻塞问题/)

### ZooKeeper的实现机制，有缓存，如何存储注册服务的

- [zookeeper实现原理](https://blog.csdn.net/pdw2009/article/details/47209681)
- [Zookeeper数据与存储](https://www.cnblogs.com/leesf456/p/6179118.html)
- [Zookeeper-服务注册与发现](https://juejin.im/post/5cbecdc76fb9a0321d73aaf8#heading-1)

### Spring的监听器

注解事件监听器与非注解事件监听器

### web.xml的配置

### spring的bean配置的几种方式

- 基于XML配置
- 基于注解配置
- 基于Java类配置

**参考**
- [关于spring中bean的三种配置方式的比较](https://blog.csdn.net/qq_19635589/article/details/72898618)

### Tomcat的各种配置，如何配置docBase

### 是否用过maven install。 maven test。

- test: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- install: install the package into the local repository, for use as a dependency in other projects locally

**参考**
- [Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)

### AOP的底层实现，动态代理是如何动态，假如有100个对象，如何动态的为这100个对象代理

AOP的底层使用动态代理来实现。

动态代理使用：
- Proxy->newProxyInstance(infs, handler) 用于生成代理对象
- InvocationHandler：这个接口主要用于自定义代理逻辑处理
- 为了完成对被代理对象的方法拦截，我们需要在InvocationHandler对象中传入被代理对象实例。

**参考**
- [10分钟看懂动态代理设计模式](https://juejin.im/post/5a99048a6fb9a028d5668e62)
- [Spring AOP底层实现- JDK动态代理和CGLIB动态代理](https://www.jianshu.com/p/b3d18892bb81)
- [Java动态代理 深度详解](https://www.imooc.com/article/21339)
- [Java三种代理模式：静态代理、动态代理和cglib代理](https://segmentfault.com/a/1190000011291179)

### 两个Integer的引用对象传给一个swap方法在方法内部交换引用，返回后，两个引用的值是否会发现变化

不会发生变化

### Java内存模型，垃圾回收机制，不可达算法

#### JVM内存结构

堆 方法区 程序计数器 栈 本地方法区

- [JVM内存结构](https://www.cnblogs.com/ityouknow/p/5610232.html)

#### Java内存模型

Java 内存模型，Java Memory Model

JMM就是一组规则，这组规则意在解决在并发编程可能出现的线程安全问题，并提供了内置解决方案（happen-before原则）及其外部可使用的同步手段(synchronized/volatile等)，确保了程序执行在多线程环境中的应有的原子性，可视性及其有序性。

JMM是一种规范，目的是解决由于多线程通过共享内存进行通信时，存在的本地内存数据不一致、编译器会对代码指令重排序、处理器会对代码乱序执行等带来的问题。

- **[全面理解Java内存模型(JMM)及volatile关键字](https://blog.csdn.net/javazejian/article/details/72772461)**
- [再有人问你Java内存模型是什么，就把这篇文章发给他。](https://www.hollischuang.com/archives/2550)
- [《成神之路-基础篇》JVM——Java内存模型(已完结)](https://www.hollischuang.com/archives/1003)  

#### 对象不可达

对象不可达算法：引用计数法、根搜索算法

引用计数法就是如果一个对象没有被任何引用指向，则可视之为垃圾。这种方法的缺点就是不能检测到环的存在。

根搜索算法的基本思路就是通过一系列名为”GC Roots”的对象作为起始点，从这些节点开始向下搜索，搜索所走过的路径称为引用链(Reference Chain)，当一个对象到GC Roots没有任何引用链相连时，则证明此对象是不可用的。

- [【JVM底层策略 一】GC roots如何判断对象不可达](https://blog.csdn.net/sinat_33087001/article/details/77987463)
- [可达性算法、Java引用 详解](https://www.jianshu.com/p/8f5fa8288d9b)

#### 垃圾回收

- [图解Java 垃圾回收机制](https://blog.csdn.net/justloveyou_/article/details/71216049)


### 一万个人抢100个红包，如何实现（不用队列），如何保证2个人不能抢到同一个红包，可用分布式锁

红包存储在长度为100的数组中，使用分布式锁，一个一个获取红包，如果索引大于99则抢红包结束。

另外一种思路是，红包分组为10组每组10个红包，一万个人落到十组同时抢红包，这样抢红包效率更高。

### HashMap的底层实现

### sleep和wait的区别

- wait只能在同步（synchronize）环境中被调用，而sleep不需要。详见Why to wait and notify needs to call from synchronized method
- 进入wait状态的线程能够被notify和notifyAll线程唤醒，但是进入sleeping状态的线程不能被notify方法唤醒。
- wait通常有条件地执行，线程会一直处于wait状态，直到某个条件变为真。但是sleep仅仅让你的线程进入睡眠状态。
- wait方法在进入wait状态的时候会释放对象的锁，但是sleep方法不会。
- wait方法是针对一个被同步代码块加锁的对象，而sleep是针对一个线程。更详细的讲解可以参考《Java核心技术卷1》，里面介绍了如何使用wait和notify方法。

**参考**
- [[译]Java中Wait、Sleep和Yield方法的区别](https://www.jianshu.com/p/25e959037eed)
- [Java的wait()、notify()学习三部曲之一：JVM源码分析](https://blog.csdn.net/boling_cavalry/article/details/77793224)

### 线程的状态，线程的阻塞的方式

Java中线程的状态分为6种。

1. 初始(NEW)：新创建了一个线程对象，但还没有调用start()方法。
2. 运行(RUNNABLE)：Java线程中将就绪（ready）和运行中（running）两种状态笼统的称为“运行”。线程对象创建后，其他线程(比如main线程）调用了该对象的start()方法。该状态的线程位于可运行线程池中，等待被线程调度选中，获取CPU的使用权，此时处于就绪状态（ready）。就绪状态的线程在获得CPU时间片后变为运行中状态（running）。
3. 阻塞(BLOCKED)：表示线程阻塞于锁。
4. 等待(WAITING)：进入该状态的线程需要等待其他线程做出一些特定动作（通知或中断）。
5. 超时等待(TIMED_WAITING)：该状态不同于WAITING，它可以在指定的时间后自行返回。
6. 终止(TERMINATED)：表示该线程已经执行完毕。

**线程的状态图**
![线程的状态图](images/thread-state.jpeg)

**线程的阻塞的方式**
1. 线程睡眠：Thread.sleep (long millis)方法，使线程转到阻塞状态。millis参数设定睡眠的时间，以毫秒为单位。当睡眠结束后，就转为就绪（Runnable）状态。sleep()平台移植性好。
2. 线程等待：Object类中的wait()方法，导致当前的线程等待，直到其他线程调用此对象的 notify() 唤醒方法。这个两个唤醒方法也是Object类中的方法，行为等价于调用 wait() 一样。wait() 和 notify() 方法：两个方法配套使用，wait() 使得线程进入阻塞状态，它有两种形式，一种允许 指定以毫秒为单位的一段时间作为参数，另一种没有参数，前者当对应的 notify() 被调用或者超出指定时间时线程重新进入可执行状态，后者则必须对应的 notify() 被调用.
3. 线程礼让，Thread.yield() 方法，暂停当前正在执行的线程对象，把执行机会让给相同或者更高优先级的线程。yield() 使得线程放弃当前分得的 CPU 时间，但是不使线程阻塞，即线程仍处于可执行状态，随时可能再次分得 CPU 时间。调用 yield() 的效果等价于调度程序认为该线程已执行了足够的时间从而转到另一个线程.
4. 线程自闭，join()方法，等待其他线程终止。在当前线程中调用另一个线程的join()方法，则当前线程转入阻塞状态，直到另一个进程运行结束，当前线程再由阻塞转为就绪状态。
5. suspend() 和 resume() 方法：两个方法配套使用，suspend()使得线程进入阻塞状态，并且不会自动恢复，必须其对应的resume() 被调用，才能使得线程重新进入可执行状态。典型地，suspend() 和 resume() 被用在等待另一个线程产生的结果的情形：测试发现结果还没有产生后，让线程阻塞，另一个线程产生了结果后，调用 resume() 使其恢复。Thread中suspend()和resume()两个方法在JDK1.5中已经废除，不再介绍。因为有死锁倾向。

**参考**
- [Java线程的6种状态及切换(透彻讲解)](https://blog.csdn.net/pange1991/article/details/53860651)
- [Java中什么方法导致线程阻塞](https://blog.csdn.net/weixin_41101173/article/details/79679300)

### 用hashmap实现redis有什么问题
- 容量问题：容量空间受JVM堆栈大小限制
- 线程并发问题：hashmap非线程安全

### Nginx的请求转发算法，如何配置根据权重转发

NGINX支持许多用于HTTP，TCP和UDP负载平衡的应用程序负载平衡方法。所有方法都考虑了可以选择分配给每个上游服务器的权重。

- Round Robin (the default) – 在上游服务器列表中按顺序分配请求。
- Least Connections – 将请求发送到活动连接数最少的服务器。
- Least Time – 将请求发送到组合了最快响应时间和最少活动连接的公式所选择的服务器。NGINX Plus专有。
- Hash – 根据您定义的键（例如客户端IP地址或请求URL）分配请求。如果上游服务器组发生更改，NGINX Plus可以选择应用一致的哈希值以最大程度地减少负载的重新分配。
- IP Hash – 根据客户端IP地址的前三个八位字节分配请求。
- 随机选择两个选项  – 随机选择两个服务器，然后将请求发送到选定的服务器，然后通过应用最小连接算法（或NGINX Plus最小时间算法，如果已配置）。

**配置根据权重转发**

当为服务器指定权重参数时，权重将作为负载均衡决策的一部分。

```
upstream myapp1 {
    server srv1.example.com weight=3;
    server srv2.example.com;
    server srv3.example.com;
}
```
使用此配置，每5个新请求将按以下方式分布在应用程序实例中：3个请求将定向到srv1，一个请求将定向到srv2，另一个将定向到srv3。

**参考**
- [Using nginx as HTTP load balancer](http://nginx.org/en/docs/http/load_balancing.html)
- [High-Performance Load Balancing](https://www.nginx.com/products/nginx/load-balancing/)


### 分布式锁

分布式锁已有的实现包括：
- 基于 ZooKeeper 的 Curator
- 基于 Redis 的 Redission

详细阅读 [再有人问你分布式锁，这篇文章扔给他](https://juejin.im/post/5bbb0d8df265da0abd3533a5) 


### JUnit4中的 before beforeClass after afterClass

一个JUnit4 的单元测试用例执行顺序为:

- @BeforeClass -> @Before -> @Test -> @After -> @AfterClass;

每一个测试方法的调用顺序为:

- @Before -> @Test -> @After;

**BeforeClass** 在所有测试之前只执行一次，且必须为 public static void no-arg method

> Sometimes several tests need to share computationally expensive setup (like logging into a database). While this can compromise the independence of tests, sometimes it is a necessary optimization. Annotating a public static void no-arg method with @BeforeClass causes it to be run once before any of the test methods in the class. The @BeforeClass methods of superclasses will be run before those the current class.

**Before** 初始化方法 对于每一个测试方法都要执行一次

> When writing tests, it is common to find that several tests need similar objects created before they can run. Annotating a public void method with @Before causes that method to be run before the Test method. The @Before methods of superclasses will be run before those of the current class.

**After** 释放资源 对于每一个测试方法都要执行一次

> If you allocate external resources in a Before method you need to release them after the test runs. Annotating a public void method with @After causes that method to be run after the Test method. All @After methods are guaranteed to run even if a Before or Test method throws an exception. The @After methods declared in superclasses will be run after those of the current class.

**@AfterClass** 在所有测试之后只执行一次，且必须为static void

> If you allocate expensive external resources in a BeforeClass method you need to release them after all the tests in the class have run. Annotating a public static void method with @AfterClass causes that method to be run after all the tests in the class have been run. All @AfterClass methods are guaranteed to run even if a BeforeClass method throws an exception. The @AfterClass methods declared in superclasses will be run after those of the current class.

**参考**

- [junit用法，before,beforeClass,after, afterClass的执行顺序](https://blog.csdn.net/lyalei/article/details/79133710)
- [JUnit 4.13-rc-1 API](https://junit.org/junit4/javadoc/latest/index.html)