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


### 泛型的使用方式有哪几种？
泛型一般有三种使用方式：泛型类、泛型接口、泛型方法。

1. 泛型类
```java
//此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
//在实例化泛型类时，必须指定T的具体类型
public class Generic<T>{

    private T key;

    public Generic(T key) {
        this.key = key;
    }

    public T getKey(){
        return key;
    }
}
```
如何实例化泛型类：
```java
Generic<Integer> genericInteger = new Generic<Integer>(123456);
```
2. 泛型接口
```java
public interface Generator<T> {
    public T method();
}
```
实现泛型接口，不指定类型：
```java
class GeneratorImpl<T> implements Generator<T>{
    @Override
    public T method() {
        return null;
    }
}
```
3. 泛型方法
```java
   public static < E > void printArray( E[] inputArray )
   {
         for ( E element : inputArray ){
            System.out.printf( "%s ", element );
         }
         System.out.println();
    }
```
使用：
```java
Integer[] intArray = { 1, 2, 3 };
String[] stringArray = { "Hello", "World" };

printArray( intArray );
printArray( stringArray );
```
注意：public static < E > void printArray( E[] inputArray ) 一般被称为静态泛型方法；  
在Java中泛型只是一个占位符，必须在传递类型后才能使用。类在实例化时才能真正的传递类型参数，  
由于静态方法的加载要先于类的实例化，也就是说类中的泛型还没有传递真正的类型参数，静态的方法的加载就已经完成了，所以静态泛型方法是没有办法使用类上声明的泛型的。只能使用自己所声明的<E>。


### 项目中哪里用到了泛型？
- 构建集合工具类（参考 Collections 中的 sort, binarySearch 方法）
- 定义 Excel 处理类 ExcelUtil<T> 用于动态指定 Excel 导出的数据类型
- 自定义接口通用返回结果 CommonResult<T> 通过参数 T 可根据具体的返回类型动态指定结果的数据类型。


## 反射

### 何谓反射？
如果说大家研究过框架的底层原理或者咱们自己写过框架的话，一定对反射这个概念不陌生。  
反射之所以被称为框架的灵魂，主要是因为它赋予了我们在运行时分析类以及执行类中方法的能力。通过反射你可以获取任意一个类的所有属性和方法，你还可以调用这些方法和属性。

### 反射的优缺点？
反射可以让我们的代码更加灵活、为各种框架提供开箱即用的功能提供了便利。  
不过，反射让我们在运行时有了分析操作类的能力的同时、也增加了安全问题，比如可以无视泛型参数的安全检查（泛型参数的安全检查发生在编译时）。另外，反射的性能也要稍差点。


### 反射的应用场景？
例如，下面是通过JDK实现动态代理的示例代码，其中就使用了反射类 Method 来调用指定的方法。
```java
public class DebugInvocationHandler implements InvocationHandler {
    /**
     * 代理类中的真实对象
     */
    private final Object target;

    public DebugInvocationHandler(Object target) {
        this.target = target;
    }

    public Object invoke(Object proxy, Method method, Object[] args) throws InvocationTargetException, IllegalAccessException {
        System.out.println("before method " + method.getName());
        Object result = method.invoke(target, args);
        System.out.println("after method " + method.getName());
        return result;
    }
}
```
另外，像Java中的一大利器"注解"的实现也用到了反射。 


## 注解

### 何谓注解？
Annotation （注解）是Java5 开始引入的新特性，可以看作是一种特殊的注释，主要用于修饰类、方法或者变量，提供某些信息供程序在编译或运行时使用。

注解本质是一个继承了 Annotation 的特殊接口：
```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {

}

public interface Override extends Annotation{

}
```
JDK 提供了很多内置的注解（@Override、@Deprecated），同时，我们还可以自定义注解。

### 注解的解析方法有哪几种？
注解只有被解析之后才会生效，常见的解析方法有两种：
- 运行期通过反射处理：像框架中自带的注解(比如 Spring 框架的 @Value、@Component)都是通过反射来进行处理的。
- 编译期直接扫描处理：编译器在编译 Java 代码的时候扫描对应的注解并处理，比如某个方法使用 @Override 注解，编译器在编译的时候就会检测当前的方法是否重写了父类对应的方法。

