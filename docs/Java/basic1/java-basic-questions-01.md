## 基础概念

### Java语言有哪些特点？
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

### JVM VS JDK VS JRE
- JVM
1. Java虚拟机(JVM)是运行Java字节码的虚拟机。JVM有针对不同操作系统(windows、Linux、macos)的特定实现，目的是使用相同的字节码，它们都会给出相同的结果。字节码和不同系统的JVM实现是Java语言“一次编写，随处运行(Write Once, Run Anywhere)”的关键所在。

2. JVM并不是只有一种！只要满足JVM规范，每个公司、组织或者个人都可以开发属于自己的专属JVM，也就是说我们平常接触到的HotSpot VM仅仅只是JVM规范的一种实现而已。当然除了我们平时最常用的HotSpot VM外，还有J9 VM、Zing VM、JRockit VM等JVM。并且你可以在 [Java SE Specifications](https://docs.oracle.com/javase/specs/index.html) 上找到各个版本的 JDK 对应的 JVM 规范。  

- JDK 和 JRE
1. JDK是 Java Developmnet Kit 的缩写，它是功能齐全的Java SDK。它拥有JRE所拥有的一切，还有编译器(javac)和工具(jdb、javadoc)，它能够创建和编译程序。

2. JRE是 Java 运行时环境。它是运行已编译 Java程序所需的所有内容的集合，包括 Java虚拟机、Java类库、Java命令和其他的一些基础构件，但是它不能用于创建新程序。
   
3. 若你只是为了运行一下 Java程序的话，那么你只需要安装 JRE 就可以了，但若你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK 了。当然这不是绝对的，有时即使你不打算在计算机上进行任何 Java 编程方面的工作，仍然需要安装 JDK。例如，如果需要使用 JSP 部署 WEB 应用程序，那么从技术上讲，你只是在应用程序服务器中来运行 Java 程序。那为什么仍然需要安装 JDk呢？因为应用程序服务器会将 JSP 转换为 Java Servlet，并且需要使用 JDK 来编译 Servlet。


### 什么是字节码？
- 字节码
1. 在 Java 中，JVM 可以理解的代码就叫做字节码（即扩展名为 .class 的文件），它不面向任何特定的处理器，只面向于虚拟机。Java语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率较低的问题，且同时又保留了解释型语言可移植的特点。所以，Java 程序运行时相对来说还是高效的(不过，和 C++、Rust、Go等语言相比却还是有一定的差距的)，而且，由于字节码并不针对一种特定的机器，因此，Java 程序无需重新编译便可以在多种不同的操作系统的计算机上运行。  
Java 程序从源代码到运行的过程如下图所示：  
![image](https://snailclimb.gitee.io/javaguide/docs/java/basis/images/java%E7%A8%8B%E5%BA%8F%E8%BD%AC%E5%8F%98%E4%B8%BA%E6%9C%BA%E5%99%A8%E4%BB%A3%E7%A0%81%E7%9A%84%E8%BF%87%E7%A8%8B.png)  

2. 我们需要格外注意的是 .class->机器码 这一步。在这一步 JVM 类加载器会首先加载字节码文件，然后通过解释器逐行来解释执行，这种方式的执行速度会相对比较慢。而且有些方法和代码块是需要经常被调用的(也就是所谓的热点代码)，所以后面引进了 JIT(just-in-time compilation)编译器，而 JIT 又属于运行时编译。因此，当 JIT编译器在完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而同时我们知道，机器码的运行效率肯定是高于 Java解释器的，这也解释了我们为什么经常会说 Java 是编译与解释共存的语言。

```
HotSpot VM 采用了惰性评估(Lazy Evaluation)的做法，根据二八定律，消耗大部分系统资源的只有那一小部分的代码(也就是所谓的热点代码)，而这也恰恰正好就是 JIT 所需要编译的部分。JVM 会根据代码每次被执行的情况收集信息并相应地做出一些优化，因此执行的次数越多，它的速度也就越快。在 JDK9 中引入了一种新的编译模式 AOT(Ahead of Time Compilation)，它是直接将字节码编译成机器码，这样就避免了 JIT 预热等各方面的开销。JDK 支持分层编译和 AOT 协作使用，但是 AOT 编译器的编译质量肯定是比不上 JIT 编译器的。
```

### 为什么说Java语言是“编译与解释并存”？
- 我们可以将高级编程语言按照程序的执行方式分为以下两种：
1. 解释型：解释型语言会通过解释器一句一句的将代码解释为机器代码后再执行，解释型语言开发效率比较快，但执行速度比较慢。常见的解释型语言有 Python、JavaScript、PHP等。
2. 编译型：编译型语言会通过编译器将源代码一次性翻译成可被该平台执行的机器码，一般情况下，编译语言的执行速度比较快，开发效率比较低。常见的编译型语言有C、C++、Go、Rust等。  
![image](https://snailclimb.gitee.io/javaguide/docs/java/basis/images/%E7%BC%96%E8%AF%91%E5%9E%8B%E8%AF%AD%E8%A8%80%E5%92%8C%E8%A7%A3%E9%87%8A%E5%9E%8B%E8%AF%AD%E8%A8%80.png)
- 那为什么说Java语言是“编译与解释并存”？  
这是因为 Java 语言既有编译型语言的特征，也具有解释型语言的特征。因为 Java 程序要经过先编译、后解释这两个步骤之后，才会生成字节码(.class文件)，这种字节码必须由 Java 解释器来解释执行。


### Oracle JDK VS OpenJDK
- Oracle JDK 和 OpenJDK 之间是否存在重大差异？
1. 对于 Java7而言，并没有什么关键得地方。OpenJDK 项目主要基于 Sun公司捐赠得 HotSpot 源代码。此外，OpenJDK 被选为 Java7 得参考实现，由 Oracle 工程师来进行维护。关于 JVM、JDK、JRE 和 OpenJDK 之间得区别，Oracle 博客帖子在2012年有一个更详细的答案，以下是截取的内容：

OpenJDK 存储库中的源代码与用于构建 Oracle JDK 的代码之间有什么区别？  
答：两者非常接近，我们的Oracle JDK 版本构建过程基于 OpenJDK7 构建，但只添加了几个部分，例如部署代码，其中包括 Oracle 的 Java 插件和 Java WebStart 的实现，以及一些闭源的第三方组件，如图形光栅化器，一些开源的第三方组件，如 Rhino，以及一些零碎的东西，如附加文档或第三方字体。展望未来，我们的目的是开源 Oracle JDK 的所有部分，除了我们考虑商业功能的部分。  

- 区别总结：
1. Oracle JDK 大概每6个月发一次主要版本，而 OpenJDK 版本大概每三个月发布一次，但这也不是固定的。
2. Oracle JDK 是 OpenJDK 的一个实现，并不是完全开源的，而 OpenJDK 是一个参考模型并且是完全开源的。
3. Oracle JDK 与 OpenJDK 相比提供了更好的性能，但 Oracle JDK 不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新的版本来获得支持。
4. Oracle JDK 比 OpenJDK 更为稳定。OpenJDK 和 Oracle JDK 的代码几乎相同，但 Oracle JDK 有更多的类和一些错误修复。因此，如果你想开发企业/商业软件，我建议你选择 Oracle JDK，因为它经过了彻底的测试和稳定。在某些情况下，有些人提到在使用 OpenJDK 时可能会遇到许多应用程序崩溃的问题，但是只需要切换到 Oracle JDK 就可以彻底解决问题。



### Java 与 C++ 的区别？
- 虽然，Java 和 C++ 都是面向对象的语言，且都支持封装、继承和多态，但是它们两者之间还是有很多不同的地方：
1. Java 不提供指针来直接访问内存，程序内存更加安全；
2. Java 有自动内存管理的垃圾回收机制(GC)，且不需要程序员手动释放无用内存；
3. Java 的类是单继承的，但 C++ 支持多重继承；虽然在 Java 中类不可以多继承，但是接口可以多继承；
4. C++ 同时支持方法的重载和操作符重载，但是Java 中只支持方法的重载(操作符重载增加了复杂性，这与 Java 最初的设计思想不相符合)。

****

## 基础语法

### 字符型常量和字符串常量的区别？
1. 内存：字符串常量只占2个字节；字符串常量占用若干个字节。
2. 形式：字符型常量是由单引号引起的一个字符，字符串常量是由双引号引起的零个或若干个字符。
3. 含义：字符型常量相当于一个整型值(ASCII值)，可以参加表达式运算；字符串常量则代表一个地址值(该字符串在内存中存放的位置)。


### 注释有哪几种形式？
1. 单行注释
2. 多行注释
3. 文档注释   
```
在我们编写代码的时候，如果代码量比较少，我们自己或者团队其他成员还可以很轻易地看懂代码，但是当项目结构一旦复杂起来，我们就需要用到注释了。
注释并不会执行(编译器在编译代码之前会把代码中的所有注释抹掉，字节码中不保留注释)，注释是我们程序写给自己看的，能够帮助看代码的人快速理清代码之间的逻辑关系。
因此，我们在写程序的时候随手加上注释是一个非常好的习惯，但是代码的注释并不是越详细越好，实际上好的代码本身就是注释，因此我们要尽量规范和美化自己的代码来减少不必要的注释。  
``` 

### 标识符和关键字的区别是什么？
1. 在我们编写程序的时候，需要大量地为程序、类、变量、方法等取名字，于是就有了标识符。简单来说，标识符就是一个名字。
2. 有一些标识，Java 语言已经赋予了其特殊的含义，只能用于特定的地方，这些特殊的标识符就是关键字。简单来说，关键字是被赋予特殊含义的标识符。比如，我们想要开一家店，则要给这个店起一个名字，起的这个"名字"就叫标识符。但是我们店的名字不能叫"警察局"，因为警察局这个名字已经被赋予了特殊的含义，而"警察局"就是我们日常生活中的关键字。


### Java 语言 关键字有哪些？
| 分类 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 | 关键字 |
| :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |    
| 访问控制 | privte | protected | public |            
| 与包相关 | import | package |
| 保留字段 | goto | const |
| 变量引用 | void | this | super |
| 错误处理 | try | catch | throw | throws | finally |
| 基本类型 | byte | short | char | double | float | int | long | boolean |
| 程序控制 | break | continue | return | do | while | if | else | for | instanceof | switch | case | default | assert |
| 类、方法和变量的修饰符 | abstract | class | extend | final | implements | interface | navite | new | static | strictfp | synchronized | transient | volatile | enum |
```
TIPS：所有的关键字都是小写的，在 IDEA 中会以特殊颜色来进行显示。
default 这个关键字很特殊，即属于程序控制，也属于类、方法和变量修饰符，同时还属于访问控制关键字。
```
- 在程序控制中，当在 switch 中匹配不到任何情况时，可以使用 default 来编写默认匹配的情况。
- 在类、方法和变量修饰符中，从 JDK8 开始引入了默认的方法，可以使用 default 关键字来定义一个方法的默认实现。
- 在访问控制中，如果一个方法前没有任何修饰符，则默认会有一个修饰符 default 但是这个修饰符若加上了就会报错。  
- 注意：虽然 true , false 和 null 看起来像关键字一样但实际上他们只是字面值，同样你也不可以作为标识符来进行使用。


### 自增自减运算符？
在写代码的过程中，常见的一种情况是需要某个整数类型变量增加1或者减少1，在 Java 中提供了一种特殊的运算符，用于这种表达式，叫做自增运算符(++)和自减运算符(--)。

++ 和 -- 运算符可以放在变量之前，也可以放在变量之后，当运算符放在变量之前时(前缀)，先自增/减，再赋值；当运算符放在变量之后时(后缀)，先赋值，再自增/减。例如，当 b = ++a 时，先自增(自身+1)，在赋值给b；当 b = a++ 时，则先赋值给b，然后再自增(自身+1)。换句话来说，也就是 ++a 输出的是 a+1 的值，而 a++ 输出的是 a 的值。用一句口诀来总结就是：符号在前就先加/减，符号在后就后加/减。


### break 、return 和 continue 关键词的区别是什么？
在循环结构中，当循环条件不满足或者循环次数达到要求时，循环会正常结束。但是，有时候可能需要在循环过程中，当发生了某种条件之后，提前终止循环，这时就需要用到下面这几个关键词:
1. break：   指跳出整个循环体，继续执行循环体下面的语句。
2. return：  用于跳出所在的方法，同时结束掉该方法的运行。
3. continue：指跳出当前的这一次循环，继续下一次的循环。

return 用于跳出所在的方法，结束该方法的执行。return 一般有意向两种用法：
- return：结束方法执行，用于没有返回值函数的方法。
- return value：返回一个特定的值，用于有返回值函数的方法。

****

## 方法


### 什么是方法的返回值？方法有哪几种类型？
方法的返回值是指我们获取到的某个方法体中的代码执行后产生的结果(当然大前提是该方法可能产生结果)。返回值的作用是接收到结果，使得它可以用于其他的操作。
我们可以按照方法的返回值和参数类型将方法分为下面这几种：
1. 无参数无返回值的方法
```java
public void f1() {
    //......
}
// 下面这个方法也没有返回值，虽然用到了 return
public void f(int a) {
    if (...) {
        // 表示结束方法的执行,下方的输出语句不会执行
        return;
    }
    System.out.println(a);
}
```
2. 有参数无返回值的方法
```java
public void f2(Parameter 1, ..., Parameter n) {
    //......
}
```
3. 有返回值无参数的方法
```java
public int f3() {
    //......
    return x;
}
```
4.有返回值有参数的方法
```java
public int f4(int a, int b) {
    return a * b;
}
```


### 静态方法为什么不能调用非静态成员？
这个需要结合 JVM 的相关知识，主要原因如下：
1. 静态方法是属于类的，在类加载的时候就会分配内存，因此可以通过类名来直接访问。而非静态成员属于实例对象，只有在对象实例化之后才存在，因此需要通过类的实例对象去访问。
2. 在类的非静态成员不存在的时候静态成员就已经存在了，此时调用在内存中还不存在的非静态成员，属于非法操作。


### 静态方法和实例方法有何不同？
1. 调用方式
在外部调用静态方法时，可以使用 类名·方法名的方式，也可以使用对象·方法名的方式，而实例方法只有后面这种方式。也就是说，调用静态方法可以无须创建对象。  
不过，需要注意的是一般不建议使用对象·方法名的方式来调用静态方法，这种方式非常容易造成混淆，因为静态方法不属于类的某个对象而且属于这个类。因此，一般建议使用类名·方法名的方式来调用静态方法。
```java
public class Person {
    public void method() {
      //......
    }

    public static void staicMethod(){
      //......
    }
    public static void main(String[] args) {
        Person person = new Person();
        // 调用实例方法
        person.method();
        // 调用静态方法
        Person.staicMethod()
    }
}
``` 
2. 访问类成员是否存在限制
静态方法在访问本类的成员时，只允许访问静态成员(即静态成员变量和静态方法)，不允许访问实例成员(即实例成员变量和实例方法)，而实例方法则不存在这个限制。


### 重载和重写的区别？
重载就是同样的一个方法能够输入根据输入数据的不同，做出不同的处理。  
重写就是当子类继承自父类的相同方法，输入数据一样，但要做出有别于父类的响应时，你就要覆盖父类的方法。


### 重载
发生在同一类中(或者父类和子类之间)，方法名必须相同，参数类型不同、个数不同、顺序不同、方法返回值和访问修饰符可以不同。
《Java 核心技术》这边书是这样介绍重载的：
如果多个方法(比如 stringBuilder 的构造方法)有相同的名字、不同的参数，便产生了重载。
```java
StringBuilder sb = new StringBuilder();
StringBuilder sb2 = new StringBuilder("HelloWorld");
```
编译器必须挑选出具体执行那个方法，他通过用各个方法给出的参数类型与特定方法调用所使用的值类型进行匹配来挑选出相应的方法。如果编译器找不到匹配的参数，就会产生编译时错误，因为根本不存在匹配，或者没有一个比其他的更好(这个过程被称为重载解析(overloading resolution))。  

Java 允许重载任何方法，而不只是构造器方法。

综上，重载就是同一个类中的多个同名方法根据不同的传参来执行不同的逻辑处理。


### 重写
重写发生在运行期间，是子类对父类的允许访问的方法的实现过程进行重写编写。
1. 方法名、参数列表必须相同，子类方法返回值类型应比父类方法返回值类型更小或相等，抛出的异常范围小于等于父类，访问修饰符范围大于父类。
2. 如果父类方法访问修饰符为 private/final/static 则子类就不能重写该方法，但是被 static 修饰的方法能够被再次声明。
3. 构造方法无法被重写。

综上，重写就是子类对父类方法的重新改造，外部样子不能改变，内部逻辑可以改变。

| 区别点 | 重载方法 | 重写方法 |
| :----: | :----: | :----: | 
| 发生范围 | 同一个类(或父类和子类之间) | 子类 |
| 参数列表 | 必须修改 | 一定不能修改 |
| 返回类型 | 可以修改 | 子类方法的返回值类型应该比父类方法返回值类型更小或相等 |
| 异常 | 可以修改 | 子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等|
| 访问修饰符 | 可以修改 | 一定不能做更严格的限制(可以降低限制) |
| 发生阶段 | 编译期间 | 运行期间 |
```
方法的重写要遵循“两同两小一大” (以下内容摘自 《疯狂讲义》)：
1. “两同”即方法名相同、形参列表相同。
2. “两小”指的是子类方法的返回值类型应比父类方法返回值类型更小或相等，子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等。
3. “一大”指的是子类方法的访问权限应比父类的访问权限更大或相等。
```
⭐️ 关于重写的返回类型这里需要额外多说明一下，上面的表述不太清晰准确：如果方法的返回类型是 void 和基本数据类型，则返回值重写时不可修改。但是如果方法的返回值是引用类型，重写时是可以返回该引用类型的子类的。
```java
public class Hero {
    public String name() {
        return "超级英雄";
    }
}
public class SuperMan extends Hero{
    @Override
    public String name() {
        return "超人";
    }
    public Hero hero() {
        return new Hero();
    }
}

public class SuperSuperMan extends SuperMan {
    public String name() {
        return "超级超级英雄";
    }

    @Override
    public SuperMan hero() {
        return new SuperMan();
    }
}

```


什么是可变长参数？
从 Java5开始，Java支持定义可变长参数，所谓可变长参数就是允许在调用方法时传入不定长度的参数。就比如下面的这个 printVariable 方法就可以接收0个或者多个参数。
```java
public static void method1(String... args) {
   //......
}

```
另外，可变长参数只能作为函数的最后一个参数，但其前面可以有也可以没有任何其他参数。
```java
public static void method2(String arg1, String... args) {
   //......
}
```
遇到方法重载的情况怎么办呢？会优先匹配固定参数还是可变参数的方法呢？
答案是会优先匹配固定参数的方法，因为固定参数的方法匹配度更高。
```java
public class VariableLengthArgument {

    public static void printVariable(String... args) {
        for (String s : args) {
            System.out.println(s);
        }
    }

    public static void printVariable(String arg1, String arg2) {
        System.out.println(arg1 + arg2);
    }

    public static void main(String[] args) {
        printVariable("a", "b");
        printVariable("a", "b", "c", "d");
    }
}
```
```
输出：
ab
a
b
c
d
```
另外，Java的可变参数编译后实际会被转换成为一个数组，我们看编译后生成的 class 文件就可以看出来了。
```
public class VariableLengthArgument {

    public static void printVariable(String... args) {
        String[] var1 = args;
        int var2 = args.length;

        for(int var3 = 0; var3 < var2; ++var3) {
            String s = var1[var3];
            System.out.println(s);
        }

    }
    // ......
}
```

## 基本数据类型

### Java 中的几种基本数据类型了解么？
Java 中有8种基本数据类型，分别为：
- 6种数字类型
  - 4种整数类型：byte、short、int、long
  - 2种浮点类型：float、double
- 1种字符类型：char
- 1种布尔类型：boolean

这8种基本数据类型的默认值以及所占空间的大小如下：
| 基本类型 | 位数 | 字节 | 默认值 | 取值范围 |
| :----: | :----: | :----: | :----: | :----: |  
| byte | 8 | 1 | 0 | -128 ~ 127 |
| short | 16 | 2 | 0 | -32768 ~ 32767 |
| int | 32 | 4 | 0 | -2147483648 ~ 2147483647 |
| long | 64 | 8 | 0L | -9223372036854775808 ~ 9223372036854775807 |
| char | 16 | 2 | 'u0000' | 0 ~ 65535 |
| float | 32 | 4 | 0f | 1.4E-45 ~ 3.4028235E38 |
| double | 64 | 8 | 0d | 4.9E-324 ~ 1.7976931348623157E308 |
| boolean | 1 |  | false | true ~ false |

对于 boolean，官方文档种未明确定义，它依赖于 JVM 厂商的具体实现。逻辑上理解是占用1位，但是实际种会考虑计算机高效存储的因素。  
另外，Java 的每种基本数据类型所占用存储空间大小不会像其他大多数语言那样随着机器硬件架构的变化而变化。这种所占存储空间大小的不变性是 Java 程序比用其他大多数语言编写的程序更具可移植性的原因之一(《Java编程思想》2.2节有提到)。

⚠️注意：
1. Java 里使用 long 类型的数据一定要在数值的后面加上L，否则将作为整型进行解析。
2. Java 里使用 char a = 'h' 需使用单引号，String a = "hello world" 需使用双引号。
3. 这八种基本数据类型都有对应的包装类型其分别为：Byte、Short、Integer、Long、Float、Double、Character、Boolean。


### 基本类型与包装类型的区别？
- 包装类型不赋值就是 null，而基本类型有默认值且不是 null。
- 包装类型可用于泛型，而 基本类型不行。
- 基本数据类型的局部变量存在在 Java 虚拟机栈中的局部变量中，基本数据类型的成员变量(未被static修饰)存放在Java虚拟机的堆中。包装类型属于对象类型，我们知道几乎所有对象实例都存在于堆中。
- 相对于对象类型，基本数据类型占用的空间非常小。

为什么说几乎所有的对象实例？  
这是因为 HotSpot 虚拟机引入了JIT优化之后，会对对象进行逃逸分析，如果发现某一个对象并没有逃逸到方法外部，那么就可能通过表里替换来实现栈上分配，而避免堆上分配内存。

⚠️注意：
基本数据类型存放在栈中是一个常见的误区！基本数据类型的成员变量如果没有被static修饰的话(不建议这么使用，应该要使用基本数据类型所对应的包装类型)，就存放在堆中。


### 包装类型的缓存机制了解么？
Java 基本数据类型的包装类型的大部分都用到了缓存机制来提升性能。
Byte、Short、Integer、Long 这4种包装类默认创建了数值[-127, 128]的相应类型的缓存数据，Character 创建了数值在[0, 127]范围的缓存数据，而 Boolean 则直接返回 true 或 false。

Integer缓存源码：
```java
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
private static class IntegerCache {
    static final int low = -128;
    static final int high;
    static {
        // high value may be configured by property
        int h = 127;
    }
}
```
Character缓存源码：
```java
public static Character valueOf(char c) {
    if (c <= 127) { // must cache
      return CharacterCache.cache[(int)c];
    }
    return new Character(c);
}

private static class CharacterCache {
    private CharacterCache(){}
    static final Character cache[] = new Character[127 + 1];
    static {
        for (int i = 0; i < cache.length; i++)
            cache[i] = new Character((char)i);
    }

}
```
Boolean缓存源码：
```java
public static Boolean valueOf(boolean b) {
    return (b ? TRUE : FALSE);
}
```
如果数值超出对应范围任然会去创建新的对象，缓存的范围区间的大小只是在性能和资源之间的权衡，但两种浮点数类型的包装类 Float、Double 却并没有实现缓存机制。

```java
Integer i1 = 33;
Integer i2 = 33;
System.out.println(i1 == i2);// 输出 true

Float i11 = 333f;
Float i22 = 333f;
System.out.println(i11 == i22);// 输出 false

Double i3 = 1.2;
Double i4 = 1.2;
System.out.println(i3 == i4);// 输出 false
```

⭐️经典问题：
```java
请问下面这段代码的输出结果是什么？

Integer i1 = 40;
Integer i2 = new Integer(40);
System.out.println(i1==i2);// 输出 false
```
⭐️问题解析：  
Integer i1 = 40; 这一行代会进行自动装箱操作，换一句话说这行代码等价于 Integer i1 = Interger.valueOf(40); 因此，i1 直接使用的是缓存中的对象，而 Integer i2 = new Integer(40); 则会去直接创建新的对象。
所有整型包装类对象之间值的比较，应全部使用 equals 方法来进行比较。阿里巴巴规范中是这样描述的，对于 Integer var = ? 在-128 至 127 之间的赋值，Integer 对象是在IntegerCache.cache 产生，会复用已有的对象，这个区间内的 Integer 值可以直接使用 == 来进行判断，但是这个区间外的所有数据，都会在堆上产生，并不会复用已有的对象，故这里也是一个大坑，因此推荐使用 equals方法来进行判断。


### 自动装箱与拆箱了解吗？ 原理是什么？
什么是自动拆装箱？
- 拆箱：将包装类型转换为基本数据类型
- 装箱：将基本类型用它们对应的引用类型包装起来

举例：
```java
int n = i;   //拆箱
Integer i = 10;  //装箱
```  
其实，从字节码中，我们可以发现装箱其实就是调用了包装类的 valueOf() 方法，而拆箱其实就是调用了 xxxValue() 方法，因此：Integer i = 10 等价于 Integer i = Integer.valueOf(10); 而 int n = i 则等价于 int n = i.intValue();

⚠️注意：
如果频繁拆装箱的话，也会严重影响系统的性能，因此我们应该尽量避免不必要的拆装箱操作。
```java
private static long sum() {
    // 应该使用 long 而不是 Long
    Long sum = 0L;
    for (long i = 0; i <= Integer.MAX_VALUE; i++)
        sum += i;
    return sum;
}

```



