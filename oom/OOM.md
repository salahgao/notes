# Java OutOfMemoryError

除了程序计数器外，虚拟机内的其他几个运行时区域都有发生OutOfMemoryError（下文成OOM）异常的可能。

### java.lang.OutOfMemoryError: Java heap space

随着对象数量的增加，总容量触及最大堆容量限制后就会产生内存溢出异常。Java堆内存溢出，应该先确认内存中导致OOM的兑现管是否是必要的，也就是要先分清楚到底是出现内存泄露（Memory  Leak）还是内容溢出（Memory Overflow）。

测试代码：

```java
import java.util.ArrayList;
import java.util.List;

/**
 * VM Args：-Xms20m -Xmx20m -XX:+HeapDumpOnOutOfMemoryError
 *
 * @author zzm
 */
public class HeapOOM {

    static class OOMObject {
    }

    public static void main(String[] args) {
        List<OOMObject> list = new ArrayList<OOMObject>();

        while (true) {
            list.add(new OOMObject());
        }
    }
}
```

### java.lang.StackOverflowError

在《Java虚拟机规范》中描述了两种异常：
- 如果线程请求的栈深度大于虚拟机所允许的最大深度，将抛出StackOverflowError异常。
- 如果虚拟机的栈内存允许动态扩展。当扩展容量无法申请到足够内存时，将抛出OutOfMemoryError异常。

《Java虚拟机规范》明确允许Java虚拟机实现自行选择是否支持栈的动态扩展，而HotSpot虚拟机的选择是不支持扩展，所以除非在创建线程申请内存时就因无法获得足够的内存而出现OutOfMemoryErroryi异常，否则在线程运行时不会因为扩展而导致内存溢出的，只会因为栈容量无法容纳新的栈帧而导致StackOverflowError异常。

无论是由于栈帧太大还是虚拟机容量太小，当新的栈帧内存无法分配的时候，HotSpot虚拟机抛出的都是StackOverflowError异常。

测试代码

```java
/**
 * VM Args：-Xss128k
 * 线程请求的栈深度大于虚拟机所允许的最大深度
 * @author zzm
 */
public class JavaVMStackSOF_1 {

    private int stackLength = 1;

    public void stackLeak() {
        stackLength++;
        stackLeak();
    }

    public static void main(String[] args) throws Throwable {
        JavaVMStackSOF_1 oom = new JavaVMStackSOF_1();
        try {
            oom.stackLeak();
        } catch (Throwable e) {
            System.out.println("stack length:" + oom.stackLength);
            throw e;
        }
    }
}
```
```java
/**
 * VM Args：-Xss128k
 * 栈容量无法容纳新的栈帧
 * @author zzm
 */
public class JavaVMStackSOF_3 {
    private static int stackLength = 0;

    public static void test() {
        long unused1, unused2, unused3, unused4, unused5,
                unused6, unused7, unused8, unused9, unused10,
                unused11, unused12, unused13, unused14, unused15,
                unused16, unused17, unused18, unused19, unused20,
                unused21, unused22, unused23, unused24, unused25,
                unused26, unused27, unused28, unused29, unused30,
                unused31, unused32, unused33, unused34, unused35,
                unused36, unused37, unused38, unused39, unused40,
                unused41, unused42, unused43, unused44, unused45,
                unused46, unused47, unused48, unused49, unused50,
                unused51, unused52, unused53, unused54, unused55,
                unused56, unused57, unused58, unused59, unused60,
                unused61, unused62, unused63, unused64, unused65,
                unused66, unused67, unused68, unused69, unused70,
                unused71, unused72, unused73, unused74, unused75,
                unused76, unused77, unused78, unused79, unused80,
                unused81, unused82, unused83, unused84, unused85,
                unused86, unused87, unused88, unused89, unused90,
                unused91, unused92, unused93, unused94, unused95,
                unused96, unused97, unused98, unused99, unused100;

        stackLength++;
        test();

        unused1 = unused2 = unused3 = unused4 = unused5 =
        unused6 = unused7 = unused8 = unused9 = unused10 =
        unused11 = unused12 = unused13 = unused14 = unused15 =
        unused16 = unused17 = unused18 = unused19 = unused20 =
        unused21 = unused22 = unused23 = unused24 = unused25 =
        unused26 = unused27 = unused28 = unused29 = unused30 =
        unused31 = unused32 = unused33 = unused34 = unused35 =
        unused36 = unused37 = unused38 = unused39 = unused40 =
        unused41 = unused42 = unused43 = unused44 = unused45 =
        unused46 = unused47 = unused48 = unused49 = unused50 =
        unused51 = unused52 = unused53 = unused54 = unused55 =
        unused56 = unused57 = unused58 = unused59 = unused60 =
        unused61 = unused62 = unused63 = unused64 = unused65 =
        unused66 = unused67 = unused68 = unused69 = unused70 =
        unused71 = unused72 = unused73 = unused74 = unused75 =
        unused76 = unused77 = unused78 = unused79 = unused80 =
        unused81 = unused82 = unused83 = unused84 = unused85 =
        unused86 = unused87 = unused88 = unused89 = unused90 =
        unused91 = unused92 = unused93 = unused94 = unused95 =
        unused96 = unused97 = unused98 = unused99 = unused100 = 0;
    }

    public static void main(String[] args) {
        try {
            test();
        } catch (Error e) {
            System.out.println("stack length:" + stackLength);
            throw e;
        }
    }
}
```

### java.lang.OutOfMemoryError: PermGen space

方法区和运行时常量池溢出。

HotSpot从JDK 7开始逐步“去永久代”的计划，并在JDK8中完全使用元空间代替永久代。

在JDK 6或更早之前的HotSpot虚拟机中，常量池都是分配在永久代中。

```java
/**
 * JDK 6或更早
 * VM Args：-XX:PermSize=6M -XX:MaxPermSize=6M
 * 运行时常量池溢出
 * @author zzm
 */
public class RuntimeConstantPoolOOM_1 {

    public static void main(String[] args) {
        // 使用Set保持着常量池引用，避免Full GC回收常量池行为
        Set<String> set = new HashSet<String>();
        // 在short范围内足以让6MB的PermSize产生OOM了
        short i = 0;
        while (true) {
            set.add(String.valueOf(i++).intern());
        }
    }
}
```

方法区的主要职责用于存放类型的相关信息，如类名、访问修饰符、常量池、字段描述、方法描述等。

基本思路：运行时产生大量的类去填满方法区，知道溢出为止。借助CGLib直接操作字节码运行时生成了大量动态类。


```java
/**
 * JDK 7
 * VM Args： -XX:PermSize=10M -XX:MaxPermSize=10M
 * 方法区内存溢出
 * @author zzm
 */
public class JavaMethodAreaOOM {

    public static void main(String[] args) {
        while (true) {
            Enhancer enhancer = new Enhancer();
            enhancer.setSuperclass(OOMObject.class);
            enhancer.setUseCache(false);
            enhancer.setCallback(new MethodInterceptor() {
                public Object intercept(Object obj, Method method, Object[] args, MethodProxy proxy) throws Throwable {
                    return proxy.invokeSuper(obj, args);
                }
            });
            enhancer.create();
        }
    }

    static class OOMObject {
    }
}
```
以上程序在jdk1.7.0_80下测试结果为：
```
Exception in thread "main" 
Exception: java.lang.OutOfMemoryError thrown from the UncaughtExceptionHandler in thread "main"
```
在jdk1.7.0下测试结果为：
```
Exception in thread "main" net.sf.cglib.core.CodeGenerationException: java.lang.reflect.InvocationTargetException-->null
	at net.sf.cglib.core.AbstractClassGenerator.generate(AbstractClassGenerator.java:345)
	at net.sf.cglib.proxy.Enhancer.generate(Enhancer.java:492)
	at net.sf.cglib.core.AbstractClassGenerator$ClassLoaderData.get(AbstractClassGenerator.java:114)
	at net.sf.cglib.core.AbstractClassGenerator.create(AbstractClassGenerator.java:291)
	at net.sf.cglib.proxy.Enhancer.createHelper(Enhancer.java:480)
	at net.sf.cglib.proxy.Enhancer.create(Enhancer.java:305)
	at com.salah.ali.omm.JavaMethodAreaOOM.main(JavaMethodAreaOOM.java:26)
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.GeneratedMethodAccessor1.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:601)
	at net.sf.cglib.core.ReflectUtils.defineClass(ReflectUtils.java:459)
	at net.sf.cglib.core.AbstractClassGenerator.generate(AbstractClassGenerator.java:336)
	... 6 more
Caused by: java.lang.OutOfMemoryError: PermGen space
	at java.lang.ClassLoader.defineClass1(Native Method)
	at java.lang.ClassLoader.defineClass(ClassLoader.java:791)
	... 11 more
```

**以上程序使用```VM Args：-XX:MaxMetaspaceSize=64m```同样可以测试元空间溢出情况。**

### java.lang.OutOfMemoryError: Metaspace

主要原因：太多的类或太大的类加载到元空间。

```
/**
 * VM Args：-XX:MaxMetaspaceSize=64m
 * 元空间溢出
 */
public class MetaspaceOOM {

    static javassist.ClassPool cp = javassist.ClassPool.getDefault();

    public static void main(String[] args) throws Exception {
        for (int i = 0; ; i++) {
            Class c = cp.makeClass("eu.plumbr.demo.Generated" + i).toClass();
        }
    }
}
```

### java.lang.OutOfMemoryError 本机直接内存溢出

```java
/**
 * VM Args：-Xmx20M -XX:MaxDirectMemorySize=10M
 *
 * @author zzm
 */
public class DirectMemoryOOM {

    private static final int _1MB = 1024 * 1024;

    public static void main(String[] args) throws Exception {
        Field unsafeField = Unsafe.class.getDeclaredFields()[0];
        unsafeField.setAccessible(true);
        Unsafe unsafe = (Unsafe) unsafeField.get(null);
        while (true) {
            unsafe.allocateMemory(_1MB);
        }
    }
}
```

### java.lang.OutOfMemoryError: Unable to create new native thread

如32位Windows的单个进程限制为2GB，去掉最大堆容量、最大方法区容量、程序计算器消耗的内存（很小，可以忽略）、进程本身耗费的内存，剩下的内存就由虚拟机栈和本地方法栈分配。因此为每个线程分配的栈内存越大，可以建立的线程数量自然就越小，建立线程是就越容易把剩下的内存耗尽。

```java
/**
 * VM Args：-Xss2M （这时候不妨设大些，请在32位系统下运行）
 * 运行前请先保存其他工作，此程序可能导致window假死
 * @author zzm
 */
public class JavaVMStackOOM {

    private void dontStop() {
        while (true) {
        }
    }

    public void stackLeakByThread() {
        while (true) {
            Thread thread = new Thread(new Runnable() {
                public void run() {
                    dontStop();
                }
            });
            thread.start();
        }
    }

    public static void main(String[] args) throws Throwable {
        JavaVMStackOOM oom = new JavaVMStackOOM();
        oom.stackLeakByThread();
    }
}

```

### java.lang.OutOfMemoryError: GC overhead limit exceeded

默认超过98%的时间用来做GC却回收了不到2%的内存时将会抛出此错误。

```java
import java.util.Map;
import java.util.Random;

public class Wrapper {
    public static void main(String args[]) throws Exception {
        Map map = System.getProperties();
        Random r = new Random();
        while (true) {
            map.put(r.nextInt(), "value");
        }
    }
}
```

```
-verbose:gc -XX:+PrintGCDetails -Xmx10m
-verbose:gc -XX:+PrintGCDetails -Xmx10m -XX:+UseParallelGC
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at java.util.Hashtable.rehash(Hashtable.java:402)
	at java.util.Hashtable.addEntry(Hashtable.java:426)
	at java.util.Hashtable.put(Hashtable.java:477)
	at com.salah.ali.oom1.Wrapper.main(Wrapper.java:31)

-verbose:gc -XX:+PrintGCDetails -Xmx100m
-verbose:gc -XX:+PrintGCDetails -Xmx100m -XX:+UseParallelGC
Exception in thread "main" java.lang.OutOfMemoryError: GC overhead limit exceeded
	at java.lang.Integer.valueOf(Integer.java:832)
	at com.salah.ali.oom1.Wrapper.main(Wrapper.java:31)

-verbose:gc -XX:+PrintGCDetails -Xmx100m -XX:+UseConcMarkSweepGC
-verbose:gc -XX:+PrintGCDetails -XX:+UseG1GC
Exception: java.lang.OutOfMemoryError thrown from the UncaughtExceptionHandler in thread "main"

```

### java.lang.OutOfMemoryError: Requested array size exceeds VM limit

试图分配大于Java虚拟机可以支持大小的数组。

```java
public class ArraySizeOOM {

    public static void main(String[] args) {
        for (int i = 10; i >= 0; i--) {
            try {
                int[] arr = new int[Integer.MAX_VALUE - i];
                System.out.format("Successfully initialized an array with %,d elements.\n", Integer.MAX_VALUE - i);
            } catch (Throwable t) {
                t.printStackTrace();
            }
        }
    }
}

```

### java.lang.OutOfMemoryError: Out of swap space

表示系统缺少物理内存和交换空间分配给应用程序。

### java.lang.OutOfMemoryError thrown from the UncaughtExceptionHandle

错误已经被默认的异常处理程序捕获，并且没有任何错误的堆栈信息输出。

### Out of memory: Kill process or sacrifice child

当可用虚拟虚拟内存(包括交换空间)消耗到让整个操作系统面临风险时，就会产生```Out of memory: Kill process or sacrifice child```错误。在这种情况下，OOM Killer会选择“流氓进程”并杀死它。

## Java 8 默认垃圾回收器
- ParNew
- ConcurrentMarkSweep

## 参考
- 深入理解Java虚拟机（第三版）
- https://plumbr.io/outofmemoryerror
- [Java内存溢出(OOM)异常完全指南](https://www.jianshu.com/p/2fdee831ed03 )