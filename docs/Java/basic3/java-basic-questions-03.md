## 异常

### Java 异常类层次结构图概览：
![image](images/types-of-exceptions-in-java.png)  


### Exception和Error有什么区别？
在 Java 中，所有的异常都有一个共同的祖先 java.lang 包中的 Throwable 类。Throwable 类有两个重要的子类：  
- Exception：程序本身可以处理的异常，可以通过 catch 来进行捕获。Exception 又可以分为 Checked Exception（受检查的异常，必须处理）和 Unchecked Exception（不受检查的异常，可以不处理）。
- Error：Error 属于程序无法处理的错误，不建议通过 catch 捕获。例如 Java 虚拟机运行错误（Virtual MachineError）、虚拟机内存不够错误（OutOfMemoryError），当这些异常发生时，Java 虚拟机（JVM）一般会选择线程终止。


### Checked Exception 和 Unchecked Exception 有什么区别？
Checked Exception 即受检查的异常，Java 代码在编译过程中，如果受检查异常没有被 catch 或者 throws 关键字处理的话，就没有办法通过编译。  
除了 RuntimeException 及其子类以外，其他的 Exception 类及其子类都属于受检查异常。常见的受检查异常有：IO相关的异常、ClassNotFoundException、SQLException。  
Unchecked Exception 即不受检查的异常，Java 代码在编译过程中，我们即使不处理不受检查的异常也可以正常通过编译，RuntimeException 及其子类都统称为不受检查的异常，常见的有：
- ArithmeticException（算术错误）
- NullPointerException(空指针错误)
- ClassCastException（类型转换错误）
- SecurityException （安全错误比如权限不够）
- ArrayIndexOutOfBoundsException（数组下标越界）
- IllegalArgumentException(参数错误比如方法入参类型错误)
- NumberFormatException（字符串转换为数字格式错误，IllegalArgumentException的子类）


### Throwable类常用方法有哪些？
- String toString()：返回异常发生时的详细信息
- String getMessage()：返回异常发生时的简要描述
- void printStackTrace()：在控制台上打印 Throwable 对象封装的异常信息
- String getLocalizedMessage()：返回异常对象的本地化信息。使用 Throwable 的子类覆盖这个方法，可以生成本地化信息。若子类没有覆盖该方法，则该方法的返回信息与 getMessage()返回结果相同
  

### try-catch-finally如何使用？
- try块：用于捕获异常。其后可接零个或多个catch块，如果没有catch块，则必须跟一个finally块
- catch块：用于处理try所捕获到的异常
- finally块：无论是否捕获或处理异常，finally块里面的语句都会被执行。当在try块或在catch块中遇到return语句时，finally语句块都将在方法返回之前被执行

代码示例：
```java
try {
    System.out.println("Try to do something");
    throw new RuntimeException("RuntimeException");
} catch (Exception e) {
    System.out.println("Catch Exception -> " + e.getMessage());
} finally {
    System.out.println("Finally");
}
```
输出结果：
```java
Try to do something
Catch Exception -> RuntimeException
Finally
```
注意：不要在finally语句中使用return!  
当在try语句和finally语句中都有return语句时，try语句块中的return语句会被忽略，这是因为try语句中的return返回值会先被暂存在一个本地变量中，而当执行到finally语句中的return之后，这个本地变量的值就变更为了finally语句中的return返回值。

代码示例：
```java
public static void main(String[] args) {
    System.out.println(f(2));
}

public static int f(int value) {
    try {
        return value * value;
    } finally {
        if (value == 2) {
            return 0;
        }
    }
}
```
输出结果：
```java
0
```


### finally中的代码一定会执行吗？
不一定的！在某些情况下，finally中的代码不会被执行。  
例如，finally之前虚拟机被终止运行了，finally中的代码就不会被执行。

代码示例：
```java
try {
    System.out.println("Try to do something");
    throw new RuntimeException("RuntimeException");
} catch (Exception e) {
    System.out.println("Catch Exception -> " + e.getMessage());
    // 终止当前正在运行的Java虚拟机
    System.exit(1);
} finally {
    System.out.println("Finally");
}
```
输出结果：
```java
Try to do something
Catch Exception -> RuntimeException
```
除此之外，在以下2种特殊情况下，finally块的代码也不会被执行：
1. 关闭CPU
2. 程序所在的线程死亡


### 异常使用有哪些需要注意的地方？
- 抛出的异常信息一定要有意义。
- 使用日志打印异常之后就不要在抛出异常了（两者不要同时存在一段代码逻辑中）。
- 不要把异常定义为静态变量，因为这样会导致异常栈信息错乱。每次手动抛出异常，我们都需要手动new一个异常对象抛出。
- 建议抛出更加具体的异常，比如字符串转换为数字格式错误的时候应该抛出 NumberFormatException 而不是其父类 IllegalArgumentException 。


## 泛型

### 什么是泛型？有什么作用？
Java 泛型（Generics）是 JDK 5 中所引入的一个新特性。使用泛型参数，可以增强代码的可读性以及稳定性。  
编译器可以对泛型参数进行检测，并且通过泛型参数可以指定传入的对象类型。比如 ArrayList<Person> persons = new ArrayList<Person> 这行代码就指明了该 ArrayList 对象只能传入 Person 对象，如果传入其他类型的对象就会报错。
```java
ArrayList<E> extends AbstractList<E>
```
并且，原生 List 返回类型是 object，需要手动转换类型才能使用，使用泛型后编译器会自动转换。