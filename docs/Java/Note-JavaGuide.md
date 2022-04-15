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
![Image text](http://rad0xouev.hd-bkt.clouddn.com/%E5%93%86%E5%95%A6A%E6%A2%A6%E4%BC%B4%E6%88%91%E8%A1%8C.jpg)  

- JDK 和 JRE
1. JDK是 Java Developmnet Kit 的缩写，它是功能齐全的Java SDK。它拥有JRE所拥有的一切，还有编译器(javac)和工具(jdb、javadoc)，它能够创建和编译程序。

2. JRE是 Java 运行时环境。它是运行已编译 Java程序所需的所有内容的集合，包括 Java虚拟机、Java类库、Java命令和其他的一些基础构件，但是它不能用于创建新程序。
   
3. 若你只是为了运行一下 Java程序的话，那么你只需要安装 JRE 就可以了，但若你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK 了。当然这不是绝对的，有时即使你不打算在计算机上进行任何 Java 编程方面的工作，仍然需要安装 JDK。例如，如果需要使用 JSP 部署 WEB 应用程序，那么从技术上讲，你只是在应用程序服务器中来运行 Java 程序。那为什么仍然需要安装 JDk呢？因为应用程序服务器会将 JSP 转换为 Java Servlet，并且需要使用 JDK 来编译 Servlet。

##### 什么是字节码？
- 字节码
1. 在 Java 中，JVM 可以理解的代码就叫做字节码（即扩展名为 .class 的文件），它不面向任何特定的处理器，只面向于虚拟机。Java语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率较低的问题，且同时又保留了解释型语言可移植的特点。所以，Java 程序运行时相对来说还是高效的(不过，和 C++、Rust、Go等语言相比却还是有一定的差距的)，而且，由于字节码并不针对一种特定的机器，因此，Java 程序无需重新编译便可以在多种不同的操作系统的计算机上运行。  
Java 程序从源代码到运行的过程如下图所示：
