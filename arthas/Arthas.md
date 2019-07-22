# Arthas 

Arthas 是Alibaba开源的Java诊断工具，深受开发者喜爱。

当你遇到以下类似问题而束手无策时，Arthas可以帮助你解决：

1. 这个类从哪个 jar 包加载的？为什么会报各种类相关的 Exception？
2. 我改的代码为什么没有执行到？难道是我没 commit？分支搞错了？
3. 遇到问题无法在线上 debug，难道只能通过加日志再重新发布吗？
4. 线上遇到某个用户的数据处理有问题，但线上同样无法 debug，线下无法重现！
5. 是否有一个全局视角来查看系统的运行状况？
6. 有什么办法可以监控到JVM的实时运行状态？

Arthas支持JDK 6+，支持Linux/Mac/Winodws，采用命令行交互模式，同时提供丰富的 Tab 自动补全功能，进一步方便进行问题的定位和诊断。

## Demo源码

[Demo源码](https://github.com/alibaba/arthas/blob/master/demo/src/main/java/demo/MathGame.java)

## 常用命令

1. 可以结合monitor与trace定位应用性能问题

### thread——查看当前 JVM 的线程堆栈信息

```
// 支持一键展示当前最忙的前N个线程并打印堆栈
$ thread -n 3 

// thread -b, 找出当前阻塞其他线程的线程
$ thread -b
```

### jad——反编译指定已加载类的源码

```
// 反编译 java.lang.String
$ jad java.lang.String

// 反编译指定的函数
jad demo.MathGame main
```

### monitor——方法执行监控

对匹配 class-pattern/method-pattern的类、方法的调用进行监控。

```
$ monitor -c 5 demo.MathGame primeFactors
Press Q or Ctrl+C to abort.
Affect(class-cnt:1 , method-cnt:1) cost in 19 ms.
 timestamp            class          method        total  success  fail  avg-rt(ms)  fail-rate                                                                                                 
-----------------------------------------------------------------------------------------------                                                                                                
 2019-07-12 03:36:07  demo.MathGame  primeFactors  5      1        4     0.13        80.00%                                                                                                    

 timestamp            class          method        total  success  fail  avg-rt(ms)  fail-rate                                                                                                 
-----------------------------------------------------------------------------------------------                                                                                                
 2019-07-12 03:36:12  demo.MathGame  primeFactors  5      3        2     0.25        40.00%                                                                                                    

 timestamp            class          method        total  success  fail  avg-rt(ms)  fail-rate                                                                                                 
-----------------------------------------------------------------------------------------------                                                                                                
 2019-07-12 03:36:17  demo.MathGame  primeFactors  5      2        3     0.11        60.00%              
```


### watch——方法执行数据观测

让你能方便的观察到指定方法的调用情况。能观察到的范围为：返回值、抛出异常、入参，通过编写 OGNL 表达式进行对应变量的查看。

```
// 观察方法出参和返回值
$ watch demo.MathGame primeFactors "{params,returnObj}" -x 2
Press Q or Ctrl+C to abort.
Affect(class-cnt:1 , method-cnt:1) cost in 20 ms.
ts=2019-07-12 03:42:46; [cost=0.122004ms] result=@ArrayList[
    @Object[][
        @Integer[201318],
    ],
    @ArrayList[
        @Integer[2],
        @Integer[3],
        @Integer[13],
        @Integer[29],
        @Integer[89],
    ],
]

// 观察方法入参
$ watch demo.MathGame primeFactors "{params,returnObj}" -x 2 -b
Press Q or Ctrl+C to abort.
Affect(class-cnt:1 , method-cnt:1) cost in 26 ms.
ts=2019-07-12 03:43:39; [cost=0.046001ms] result=@ArrayList[
    @Object[][
        @Integer[-7478],
    ],
    null,
]

// 按照耗时进行过滤
$ watch demo.MathGame primeFactors '{params, returnObj}' '#cost>200' -x 2
Press Ctrl+C to abort.
Affect(class-cnt:1 , method-cnt:1) cost in 66 ms.
ts=2018-12-03 19:40:28; [cost=2112.168897ms] result=@ArrayList[
    @Object[][
        @Integer[2141897465],
    ],
    @ArrayList[
        @Integer[5],
        @Integer[428379493],
    ],
]
```

### trace——方法内部调用路径，并输出方法路径上的每个节点上耗时

方法内部调用路径，并输出方法路径上的每个节点上耗时。trace 命令能主动搜索 class-pattern/method-pattern 对应的方法调用路径，渲染和统计整个调用链路上的所有性能开销和追踪调用链路。

```
$ trace demo.MathGame run
Press Q or Ctrl+C to abort.
Affect(class-cnt:1 , method-cnt:1) cost in 39 ms.
`---ts=2019-07-12 07:26:57;thread_name=main;id=1;is_daemon=false;priority=5;TCCL=sun.misc.Launcher$AppClassLoader@70dea4e
    `---[0.710725ms] demo.MathGame:run()
        +---[0.020401ms] java.util.Random:nextInt() #23
        +---[0.077602ms] demo.MathGame:primeFactors() #24 [throws Exception]
        +---[0.0084ms] java.lang.StringBuilder:<init>() #28
        +---[0.0112ms] java.lang.Integer:valueOf() #28
        +---[0.164106ms] java.lang.String:format() #28
        +---[min=0.0035ms,max=0.003801ms,total=0.007301ms,count=2] java.lang.StringBuilder:append() #28
        +---[0.013701ms] java.lang.Exception:getMessage() #28
        +---[0.0034ms] java.lang.StringBuilder:toString() #28
        `---[0.094704ms] java.io.PrintStream:println() #28
        
$ trace demo.MathGame run '#cost > 1'
Press Q or Ctrl+C to abort.
Affect(class-cnt:1 , method-cnt:1) cost in 80 ms.
`---ts=2019-07-12 07:28:50;thread_name=main;id=1;is_daemon=false;priority=5;TCCL=sun.misc.Launcher$AppClassLoader@70dea4e
    `---[2.532188ms] demo.MathGame:run()
        +---[0.012001ms] java.util.Random:nextInt() #23
        +---[2.315081ms] demo.MathGame:primeFactors() #24
        `---[0.084003ms] demo.MathGame:print() #25

```

### stack——输出当前方法被调用的调用路径

输出当前方法被调用的调用路径。很多时候我们都知道一个方法被执行，但这个方法被执行的路径非常多，或者你根本就不知道这个方法是从那里被执行了，此时你需要的是 stack 命令。

```
$ stack demo.MathGame primeFactors
Press Q or Ctrl+C to abort.
Affect(class-cnt:1 , method-cnt:1) cost in 74 ms.
ts=2019-07-12 08:11:07;thread_name=main;id=1;is_daemon=false;priority=5;TCCL=sun.misc.Launcher$AppClassLoader@70dea4e
    @demo.MathGame.run()
        at demo.MathGame.main(MathGame.java:16)

// 据执行时间来过滤
$ stack demo.MathGame primeFactors '#cost>5'
Press Ctrl+C to abort.
Affect(class-cnt:1 , method-cnt:1) cost in 35 ms.
ts=2018-12-04 01:35:58;thread_name=main;id=1;is_daemon=false;priority=5;TCCL=sun.misc.Launcher$AppClassLoader@3d4eac69
    @demo.MathGame.run()
        at demo.MathGame.main(MathGame.java:16)
```

## 在线教程
https://alibaba.github.io/arthas/


## GitHub
https://github.com/alibaba/arthas