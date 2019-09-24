# 问答

## 目录



- [Nginx的请求转发算法，如何配置根据权重转发](#nginx的请求转发算法，如何配置根据权重转发)
- [分布式锁](#分布式锁)
- [JUnit4中的 before beforeClass after afterClass](#junit4中的-before-beforeclass-after-afterclass)

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