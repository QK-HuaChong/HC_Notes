# Java

## JVM

### 1. 内存模型

- JVM内存模型

![JVM内存模型](img\jvm_01.jpg 'JVM内存模型')

- JMM内存模型：定义程序中变量的访问规则

![JVM内存模型](img\jvm_02.jpg 'JVM内存模型')

- JMM保证

![JVM内存模型](img\jvm_03.jpg 'JVM内存模型')

**注：** volatile

> volatile:1.对变量的赋值会强制刷新到主内存，强制变量的读取会从主内存中重新加载。2.阻止指令重排序
  
#### 1.1、 程序计数器

#### 1.2、 方法区

#### 1.3、 堆/栈

#### 1.4、本地方法栈

### 2. 类加载机制

#### 2.1、类加载的流程

```mermaid
    graph LR
    id1(加载)-->id2(链接)
    subgraph 链接
    id2(验证)-->id3(准备)
    id3(准备)-->id4(解析)
    end
    id4(解析)-->id5(初始化)
    id5(初始化)-->id6(使用)
    id6(链接)-->id7(卸载 GC)
```

#### 2.2、双亲委派模式：

- BootStrap ClassLoader 启动类加载 --->  <JAVA_HOME>/lib
- ExtClassLoader 扩展加载器  --->  <JAVA_HOME>/lin/ext
- AppClassLoader 应用加载器   --->   java -classpath
- Custom ClassLoader 自定义类加载器

### 3. GC 垃圾回收

#### 3.1、分代回收

- 年轻代
- 老年代
- 永久代

#### 3.2、回收算法

- CMS 算法
- G1 算法
- ZGC

#### 3.3、FullGC的触发

- 年轻代晋升老年代空间不足
- 永久代空间不足

### 4. 性能调优

### 5. 编译器优化

### 6. 执行模式