#### 前言

##### Java概述
- 何为编程？

&emsp;&emsp;编程就是让计算机为解决某个问题而使用某种程序设计语言编写程序代码，并最终得到结果的过程。
&emsp;&emsp;为了使计算机能够理解人的意图，人类就必须要将需解决的问题的思路、方法、和手段通过计算机能够理解的形式告诉计算机，使得计算机能够根据人的指令一步一步去工作，进而完成某种特定的任务。这种人和计算机之间交流的过程就是编程。

- 什么是Java?

&emsp;&emsp;Java是一门面向对象的编程语言，不仅吸收了C++语言的各种优点，还摈弃了C++里难以理解的多继承、指针等概念，因此Java语言具有功能强大和简单易用两个特征。Java语言作为静态面向对象编程语言的代表，极好地实现了面向对象的理论，允许程序员以优雅的思维方式进行复杂的编程。

- jdk1.5之后的三大版本
1. Java SE（J2SE，Java 2 Platform Standard Edition，标准版）
```
备注：Java SE 以前称为J2SE。它允许开发和部署在桌面、服务器、嵌入式环境中使用的Java应用程序。Java SE包含了支持Java Web服务开发的类，并为Java EE和Java ME提供基础。
```
2. Java EE（J2EE，Java 2 Platform Enterprise Edition，企业版）
```
备注：Java EE 以前称为J2EE。企业版本帮助开发和部署可移植、健壮、可伸缩且安全的服务器端的Java应用程序。Java EE是在Java SE的基础上构建的，它提供Web服务、组件模型、管理和通信API,可以用来实现企业级的面向服务体系结构（service-oriented architecture，SOA）和Web2.0的应用程序。2018年2月，Eclipse宣布正式将JavaEE更名为JakartaEE。
```
3. Java ME（J2ME，Java2 Platform Mico Edition，微型版）
```
备注：Java ME以前称为J2ME。Java ME为在移动设备和嵌入式设备（比如手机、PDA、电视机顶盒盒打印机）上运行的应用程序提供一个健壮且灵活的环境。Java ME包括灵活的用户界面、健壮的安全模型、许多内置的网络协议以及可以动态下载的连网和离线应用程序的丰富支持。基于Java ME规范的应用程序只需编写一次，就可以用于许多设备，而且可以利用每个设备的本机功能。
```
- JVM、JRE和JDk的关系
1. JVM
```
Java Virtual Machine是Java虚拟机，Java程序需要运行在虚拟机上，不同的平台有自己的虚拟机，因此Java语言可以实现跨平台。
```
2. JRE
```
Java Runtime Environment包括Java虚拟机和Java程序所需的核心类库等。核心类库主要是java.lang包：包含了运行Java程序必不可少的系统类，如基本数据类型、基本数据函数、字符串处理、线程、异常处理类等，系统缺省加载这个包。如果想要运行一个开放好的Java程序，计算机中只需要安装JRE即可。
```
3. JDK
```
Java Development Kit是提供给Java开发人员使用的，其中包含了Java的开发工具，也包括了JRE。所以安装了JDK，就无需再单独安装JRE了。其中的开发工具：编译工具（javac.exe)，打包工具（jar.exe）等。
```
- 什么是跨平台性？

&emsp;&emsp;所谓跨平台性，是指java语言编写的程序，一次编译后，可以在多个系统平台上运行。
&emsp;&emsp;实现原理：Java程序是通过java虚拟机在系统平台上运行的，因此只需要该系统安装相应的java虚拟机，该系统就可以运行java程序。

- Java语言的特点？
1. 简单易学
2. 面向对象（封装、继承、多态）
3. 平台无关性
4. 支持网络编程
5. 支持多线程（多线程机制使应用程序在同一时间并行执行多项任务）
6. 安全性
7. 健壮性（Java语言的强类型机制、异常处理、垃圾的自动回收等）

- 什么是Java程序的主类？

&emsp;&emsp;一个程序中可以有多个类，但只能有一个类是主类。在Java应用程序中，这个主类是指包含main()方法的类。而在Java小程序中，这个主类是一个继承自系统类JApple或Applet的子类。应用程序的主类不一定要求是public类，但小程序的主类要求必须是public类。主类是Java程序执行的入口点。

- Java应用程序与小程序之间有哪些差别？

&emsp;&emsp;应用程序是从主线程启动（也就是main()方法），applet小程序没有main方法，主要是嵌入在浏览器页面上运行（调用init()线程或者run()来启动），嵌入浏览器这点跟falsh的小游戏类似。

- Java和C++的区别？
1. 都是面向对象的语言，都支持封装、继承和多态。
2. Java不提供指针来直接访问内存，程序内存更加安全
3. Java的类是单继承，C++z支持多重继承；虽然Java的类不可以多继承，但是接口可以多继承。
4. Java有自动内存管理机制，不需要程序员手动释放无用内存。

****

##### 基础语法
- Java的数据类型？

&emsp;&emsp;Java语言是强类型语言，对于每一种数据都定义了明确的具体的数据类型，在内存中分配了不同大小的内存空间。

- 基本数据类型

```
1. 整数类型（byte、short、int、long）
2. 浮点类型（flot、double）
3. 数值型
4. 字符型（char）
5. 布尔型（boolean）
```
- 引用数据类型

```
1. 类（class）
2. 接口（interface）
3. 数组（[]）
```
- switch是否能作用在byte上？是否能作用在long上？是否能作用在String上？

&emsp;在Java 5以前，switch(expr)中，expr只能是byte、short、char、int。从Java5开始，Java中引入了枚举类型，expr也可以是enum类型，从Java7开始，expr还可以是字符串(String),但是长整型（long）在目前所有的版本中都是不可以的。

- 如何用最有效的方法计算2乘以8？

&emsp;&emsp;2 << 3 (向左移动3位相当于乘以2的3次方，向右移动3位相当于除以2的3次方)。

- Math.round(11.5)等于多少？Math.round(-11.5)等于多少？

&emsp;&emsp;Math.round(11.5)的返回值是12，Math.round(-11.5)的返回值是-11，四舍五入的原理是在参数上加0.5然后进行下取整。

- float f=3.4是否正确？

&emsp;&emsp;不正确，3.4是双精度数，将双精度型（double）赋值给浮点型（flot）属于向下转型（down-casting，也称为窄化）会造成精度损失，因此需要强制类型转换float f = (float)3.4；或者写成flot f =3.4F。

- short s1 = 1;s1 = s1 + 1;有错误吗？short s1 = 1; s1 += 1有错误吗？

&emsp;&emsp;对于 short s1 = 1; s1 = s1 + 1; 由于1是int类型，因此s1+1运算结果也是int型，需要强制转换类型才能赋值给short型，所以会报错。

&emsp;&emsp;对于 short s1 = 1; s1 += 1;&emsp;&emsp;可以正确编译，因为s1 += 1;相当于s1 = (short)(s1 + 1);其中有隐含的强制类型转换，所以不会报错。

****

#### 访问修饰符

&emsp;&emsp;定义：Java中，可以使用访问修饰符来保护对类、变量、方法和构造方法的访问。Java支持public、private、protected、default四种不同的访问权限。
```
public：对所有的类可见，使用的对象为类、接口、变量、方法。
default：在同一包内可见，不使用任何修饰符，使用的对象为类、接口、变量、方法。
private：在同一类内可见，使用的对象为：变量、方法。注意：private不能修饰外部类。
protected：对同一包内的类和所有的子类可见，使用的对象为变量、方法。注意：protected不能修饰外部类。
```
##### 运算符
- &和&&的区别？

&emsp;&emsp;&运算符有两种用法：1：按位与；2：逻辑与

&emsp;&emsp;&&运算符是短路与运算。逻辑与跟短路与的差别是非常巨大的，虽然二者都要求运算符左右的两端的布尔值都是true整个表达式的值才是true。&&之所以称为短路运算，是因为如果&&左边的表达式的值是false，右边的表达式会被直接短路掉，不会进行运算。逻辑或运算符（|）和短路或运算符（||）的差别也是如此。

- final有什么用？

&emsp;&emsp;作用：用于修饰类、属性和方法
```
被final修饰的类不可以被继承。
被fianl修饰的方法不可以被重写。
被final修饰的变量不可以被改变，被fianl修饰不可变的是变量的引用，而不是引用指向的内容，引用指向的内容是可以改变的。
```
- final finally finalize区别？

&emsp;&emsp;final可以修饰类、变量、方法，修饰类表示该类不能被继承、修饰方法表示该方法不能被重写、修饰变量表示该变量是一个常量不能被重写赋值。

&emsp;&emsp;finally一般作用在try-catch代码块中，在处理异常的时候，通常我们将一定要执行的代码放在finally代码块中，表示不管是否出现异常，该代码块都会执行，一般用来存放一些关闭资源的代码。

&emsp;&emsp;finalize是一个方法，属于Object类的一个方法，而Object类是所有类的父类，该方法一般由垃圾回收器来调用，当我们调用System.gc()方法的时候，由垃圾回收器调用finalize()，回收垃圾。

- this关键字的用法

&emsp;&emsp;this是自身的一个对象，代表对象本身，可以理解为指向对象本身的一个指针。

&emsp;&emsp;this的用法在Java中大体可以分为3种：

1. 普通的直接引用，this相当于是指向当前对象本身。
2. 形参与成属性名称重名，用this来区分
```java
public person(String name，int age) {
    this.name = name;
    this.age = age;
}
```
3. 引用本类的构造函数
```java
public class person{
    private int age;
    private String naem;

    //无参构造
    public person() {

    }

    //有参构造
    public person(String name) {
        this.name = name;
    }

    public person(String name，int age) {
        this(name);
        this.age = age;
    }
}
```
- super关键字的用法

&emsp;&emsp;super可以理解为是指向自己超（父）类对象的一个指针，而这个超类指的是离自己最近的一个的父类。

&emsp;&emsp;super也有三种用法：

1. 普通的直接引用，与this类似，super相当于是指向当前对象的父类的引用，这样就可以用super.xxx来引用父类的成员。
2. 子类中的成员变量或方法与父类中的成员变量或方法同名时，用super进行区分。
```java
public person{
    protected String name;

    public person(String name) {
        this.name = name;
    }
}
public class student extends person{
    private String name;

    public student(String name, String name1) {
        super(name);
        this.name = name1;
    }

    public void getInfo(){
        System.out.println(this.name);//child
        System.out.println(super.name);//fatcher
    }
}
public calss Test {
    public static void main(String[] args) {
        Student s1 = new Student(”Fatcher“,"Child");
        s1.getInfo();
    }
}
```
3. 引用父类构造函数

&emsp;&emsp;super(参数)：调用父类中的某一个构造函数（应该为构造函数中的第一条语句）

&emsp;&emsp;this(参数)： 调用本类中另一种形式的构造函数（应该为构造函数中的第一条语句）

- this与super的区别
1. this：它代表当前对象名（在程序中易产生二义性之处，应当使用this来指明当前对象；如果函数的形参与类中的成员数据同名，这时需用this来指明成员变量名）。
2. super：它引用当前对象的直接父类中的成员（用来访问直接父类中被隐藏的父类中的成员数据或函数，基类与派生类中有相同成员定义时需用：super.变量名、super.成员函数名）。
3. super()与this()关键字类似，区别是super()在子类中调用父类的构造方法，this()在本类内调用本类的其他构造方法。 
4. super()和this()均需放在构造方法内第一行。
5. this和super不能同时出现在一个构造函数里面，因为this必然会调用其它的构造函数，而其它的构造函数必然也会有super语句的存在，所以在同一个构造函数里面有相同的语句，就失去了语句的意义，编译器也不会通过。
1. this()和super()都指的是对象，所以，均不可以在static环境中使用，包括static变量，static方法，static代码块。
2. 从本质上讲，this是一个指向本对象的指针，然而super是一个Java关键字。

- static存在的主要意义

&emsp;&emsp;static的主要意义是在于创建独立于具体对象的域变量或方法，因此以致于即使没有创建对象，也能使用属性和调用方法。

&emsp;&emsp;static关键字还有一个比较关键的作用的就是用来形成静态代码块以优化程序性能。static代码块可以置于类中的任何地方，类中可以有多个static代码块。在类初次被加载的时候，会按照static代码块的顺序来执行每个static代码块，并且只会执行一次。

- static的独特之处

&emsp;&emsp;1.被static修饰的变量或者方法是独立于该类的任何对象，也就是说，这些变量和方法不属于任何一个实例对象，而是被类的实例对象所共享。
```
如何通俗理解"被类的实例对象所共享"这句话呢？通俗来讲就是说，一个类的静态成员，它是属于大伙的（这里的大伙指的是这个类的多个对象实例，我们都知道一个类可以创建多个实例）是所有的类对象共享的，不像成员变量是各自的（各自指的是这个类的单个实例对象）。
```
&emsp;&emsp;2.在该类被第一次加载的时候，就会去加载被static修饰的部分，而且只会在类第一次使用的时候进行加载并进行初始化，后面根据需要可以再次进行赋值。

&emsp;&emsp;3.static变量值在类加载的时候分配空间，以后创建类对象的时候不会重新分配，但是赋值的话，是可以任意赋值的。

&emsp;&emsp;4.被static修饰的变量或者方法是优先与对象存在的，也就是说当一个类加载完毕之后，即便没有创建对象，也可以去访问。

- static应用场景

&emsp;&emsp;因为static是被类的实例对象所共享，因此如果某个成员变量是被所有对象所共享的，那么这个成员变量就应该被定义为静态变量。
```
1：修饰成员变量
2：修饰成员方法
3：静态代码块
4：修饰类（只能修饰内部类也就是静态内部类）
5：静态导包
```
- static注意事项
1. 静态只能访问静态
2. 非静态既可以访问非静态的，也可以访问静态的。