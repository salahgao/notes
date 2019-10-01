# 问答

## TODO
- ThreadPoolExecutor
- 设计模式
- AOP 实现 静态植入 静态代理 动态代理 AspectJ CGLIB
- 两个Integer的引用对象传给一个swap方法在方法内部交换引用，返回后，两个引用的值是否会发现变化 不会发生变化 为什么？

## 目录
- [字符串的格式化方法](#字符串的格式化方法)
- [用过spring的线程池还是java的线程池？](#用过spring的线程池还是java的线程池？)
- [IO会阻塞吗？readLine是不是阻塞的](#io会阻塞吗？readline是不是阻塞的)

- [ZooKeeper的实现机制，有缓存，如何存储注册服务的](#zookeeper的实现机制，有缓存，如何存储注册服务的)
- [Spring的监听器](#spring的监听器)
- [web.xml的配置](#webxml的配置)
- [spring的bean配置的几种方式](#spring的bean配置的几种方式)
- [Tomcat的各种配置，如何配置docBase](#tomcat的各种配置，如何配置docBase)
- [是否用过maven install。 maven test。git（make install是安装本地jar包）](#是否用过maven-install。-maven-test。git（make-install是安装本地jar包）)
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
- https://blog.csdn.net/qq_19635589/article/details/72898618

### Tomcat的各种配置，如何配置docBase

### 是否用过maven install。 maven test。git（make install是安装本地jar包）

- test: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- install: install the package into the local repository, for use as a dependency in other projects locally

**参考**
- https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html

### AOP的底层实现，动态代理是如何动态，假如有100个对象，如何动态的为这100个对象代理

### 两个Integer的引用对象传给一个swap方法在方法内部交换引用，返回后，两个引用的值是否会发现变化

不会发生变化

### Java内存模型，垃圾回收机制，不可达算法

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
- https://www.jianshu.com/p/25e959037eed
- https://blog.csdn.net/boling_cavalry/article/details/77793224

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
- https://blog.csdn.net/pange1991/article/details/53860651
- https://blog.csdn.net/weixin_41101173/article/details/79679300

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
- http://nginx.org/en/docs/http/load_balancing.html
- https://www.nginx.com/products/nginx/load-balancing/


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

- https://blog.csdn.net/lyalei/article/details/79133710

- https://junit.org/junit4/javadoc/latest/index.html