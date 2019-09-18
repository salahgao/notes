# Q&A

## 目录

- [分布式锁](#分布式锁)
- [JUnit4 中的 before beforeClass after afterClass](#junit4-中的-before-beforeclass-after-afterclass)


### 分布式锁


### JUnit4 中的 before beforeClass after afterClass

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