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
- String getLocalizedMessage()：返回异常对象的本地化信息。使用 Throwable 的子类覆盖这个方法，可以生成本地化信息。若子类没有覆盖该方法，则该方法的返回信息与 getMessage() 返回结果相同