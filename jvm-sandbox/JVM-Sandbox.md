# JVM-Sandbox

JVM-Sandbox（沙箱）实现了一种在不重启、不侵入目标JVM应用的AOP解决方案。

## 沙箱的特性
1. 无侵入：目标应用无需重启也无需感知沙箱的存在
2. 类隔离：沙箱以及沙箱的模块不会和目标应用的类相互干扰
3. 可插拔：沙箱以及沙箱的模块可以随时加载和卸载，不会在目标应用留下痕迹
4. 多租户：目标应用可以同时挂载不同租户下的沙箱并独立控制
5. 高兼容：支持JDK[6,11]


## 沙箱常见应用场景

- 线上故障定位
- 线上系统流控
- 线上故障模拟
- 方法请求录制和结果回放
- 动态日志打印
- 安全信息监测和脱敏

## 沙箱事件
在JVM-Sandbox的世界观中，任何一个Java方法的调用都可以分解为BEFORE、RETURN和THROWS三个环节，由此在三个环节上引申出对应环节的事件探测和流程控制机制

- BEFORE事件：执行方法体之前被调用
- RETURN事件：执行方法体返回之前被调用
- THROWS事件：执行方法体抛出异常之前被调用


## 实时无侵入AOP框架
JVM-SANDBOX属于基于Instrumentation的动态编织类的AOP框架，**通过精心构造了字节码增强逻辑，使得沙箱的模块能在不违反JDK约束情况下实现对目标应用方法的无侵入运行时AOP拦截。**

## 本地安装
1. 下载
2. 解压
3. 运行 ./install-local.sh -p /root

```
   VERSION=1.2.1
   PATH=/root/sandbox
   install sandbox successful.
```

## 模块编写
[修复一个损坏的“钟”](https://github.com/alibaba/jvm-sandbox/wiki/FIRST-MODULE)


## GitHub
https://github.com/alibaba/jvm-sandbox
