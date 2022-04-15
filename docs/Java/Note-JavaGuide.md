#### 前言
&emsp;&emsp;Java基础

##### 基础概念与常识
- Java语言有哪些特点？
1. 可靠性
2. 安全性
3. 简单易学；
4. 编译与解释并存
5. 面向对象(封装、继承、多态)；
6. 平台无关性(Java 拟机实现了平台无关性)；
7. 支持多线程(C++语言没有内置的多线程机制，因此必须调用操作系统的多线程功能来进行多线程程序设计)；
8. 支持网络编程(Java语言诞生本身就是为简化网络编程而设计的，因此Java 语言不仅支持网络编程而且还很方便)。

```
参考：http://www.cplusplus.com/reference/thread/thread/?kw=thread 
拓展：从C++11开始，C++就引入了多线程库，且在windows、Linux、macos上都可以使用 std::thread 和 std::asyc 来创建线程。
```

##### JVM VS JDK VS JRE
- JVM
1. Java虚拟机(JVM)是运行Java字节码的虚拟机。JVM有针对不同操作系统(windows、Linux、macos)的特定实现，目的是使用相同的字节码，它们都会给出相同的结果。字节码和不同系统的JVM实现是Java语言“一次编写，随处运行(Write Once, Run Anywhere)”的关键所在。

2. JVM并不是只有一种！只要满足JVM规范，每个公司、组织或者个人都可以开发属于自己的专属JVM，也就是说我们平常接触到的HotSpot VM仅仅只是JVM规范的一种实现而已。当然除了我们平时最常用的HotSpot VM外，还有J9 VM、Zing VM、JRockit VM等JVM。并且你可以在 [Java SE Specifications](https://docs.oracle.com/javase/specs/index.html) 上找到各个版本的 JDK 对应的 JVM 规范。  

- JDK 和 JRE
1. JDK是 Java Developmnet Kit 的缩写，它是功能齐全的Java SDK。它拥有JRE所拥有的一切，还有编译器(javac)和工具(jdb、javadoc)，它能够创建和编译程序。

2. JRE是 Java 运行时环境。它是运行已编译 Java程序所需的所有内容的集合，包括 Java虚拟机、Java类库、Java命令和其他的一些基础构件，但是它不能用于创建新程序。
   
3. 若你只是为了运行一下 Java程序的话，那么你只需要安装 JRE 就可以了，但若你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK 了。当然这不是绝对的，有时即使你不打算在计算机上进行任何 Java 编程方面的工作，仍然需要安装 JDK。例如，如果需要使用 JSP 部署 WEB 应用程序，那么从技术上讲，你只是在应用程序服务器中来运行 Java 程序。那为什么仍然需要安装 JDk呢？因为应用程序服务器会将 JSP 转换为 Java Servlet，并且需要使用 JDK 来编译 Servlet。


##### 什么是字节码？
- 字节码
1. 在 Java 中，JVM 可以理解的代码就叫做字节码（即扩展名为 .class 的文件），它不面向任何特定的处理器，只面向于虚拟机。Java语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率较低的问题，且同时又保留了解释型语言可移植的特点。所以，Java 程序运行时相对来说还是高效的(不过，和 C++、Rust、Go等语言相比却还是有一定的差距的)，而且，由于字节码并不针对一种特定的机器，因此，Java 程序无需重新编译便可以在多种不同的操作系统的计算机上运行。  
Java 程序从源代码到运行的过程如下图所示：  
![image](https://snailclimb.gitee.io/javaguide/docs/java/basis/images/java%E7%A8%8B%E5%BA%8F%E8%BD%AC%E5%8F%98%E4%B8%BA%E6%9C%BA%E5%99%A8%E4%BB%A3%E7%A0%81%E7%9A%84%E8%BF%87%E7%A8%8B.png)  

2. 我们需要格外注意的是 .class->机器码 这一步。在这一步 JVM 类加载器会首先加载字节码文件，然后通过解释器逐行来解释执行，这种方式的执行速度会相对比较慢。而且有些方法和代码块是需要经常被调用的(也就是所谓的热点代码)，所以后面引进了 JIT(just-in-time compilation)编译器，而 JIT 又属于运行时编译。因此，当 JIT编译器在完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而同时我们知道，机器码的运行效率肯定是高于 Java解释器的，这也解释了我们为什么经常会说 Java 是编译与解释共存的语言。

```
HotSpot VM 采用了惰性评估(Lazy Evaluation)的做法，根据二八定律，消耗大部分系统资源的只有那一小部分的代码(也就是所谓的热点代码)，而这也恰恰正好就是 JIT 所需要编译的部分。JVM 会根据代码每次被执行的情况收集信息并相应地做出一些优化，因此执行的次数越多，它的速度也就越快。在 JDK9 中引入了一种新的编译模式 AOT(Ahead of Time Compilation)，它是直接将字节码编译成机器码，这样就避免了 JIT 预热等各方面的开销。JDK 支持分层编译和 AOT 协作使用，但是 AOT 编译器的编译质量肯定是比不上 JIT 编译器的。
```

##### 为什么说Java语言是“编译与解释并存”？
- 我们可以将高级编程语言按照程序的执行方式分为以下两种：
1. 解释型：解释型语言会通过解释器一句一句的将代码解释为机器代码后再执行，解释型语言开发效率比较快，但执行速度比较慢。常见的解释型语言有 Python、JavaScript、PHP等。
2. 编译型：编译型语言会通过编译器将源代码一次性翻译成可被该平台执行的机器码，一般情况下，编译语言的执行速度比较快，开发效率比较低。常见的编译型语言有C、C++、Go、Rust等。  
![image](https://snailclimb.gitee.io/javaguide/docs/java/basis/images/%E7%BC%96%E8%AF%91%E5%9E%8B%E8%AF%AD%E8%A8%80%E5%92%8C%E8%A7%A3%E9%87%8A%E5%9E%8B%E8%AF%AD%E8%A8%80.png)
- 那为什么说Java语言是“编译与解释并存”？  
这是因为 Java 语言既有编译型语言的特征，也具有解释型语言的特征。因为 Java 程序要经过先编译、后解释这两个步骤之后，才会生成字节码(.class文件)，这种字节码必须由 Java 解释器来解释执行。

