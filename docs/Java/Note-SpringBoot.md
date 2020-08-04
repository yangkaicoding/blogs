#### 前言
&emsp;&emsp;SpringBoot可以简单地看成简化了的、按照约定开发的SSM框架，简化了传统的SSM框架开发过程中需要进行大量配置等工作，其实很多配置行为本身只是一种手段，并不是目的，基于这个考虑，SpringBoot采用约定大于配置的方式，简化了传统框架原有样板化的配置。

#### 正文
- SpringBoot的优点
1. 快速开发
2. 轻松部署
3. 自动化配置

- IntelliJ IDEA SpringBoot项目构建步骤
1. 菜单->New->Project->Spring Initializr->Next；
2. 输入Group，Artifact两个项目参数，其他参数不需要修改，然后Next；
3. 勾选Web，然后点击Next；
4. 指定项目路径，例如：D:\project_stu\project_springboot；
5. 创建成功。

&emsp;&emsp; 备注：GroupId和ArtifactId是maven管理项目包时用作区分的字段，GroupId分为几个字段，例如com.vpclub，前面的com叫做域，后面的为自己起的域名，ArtifactId一般是项目名或模块名。

- SpringBoot项目部署方式-jar方式
1. 命令行切换到项目所在目录，执行mvn clean package命令即可
2. 命令行输入java -Xms128m -Xmx512m -jar eureka-server-1.0.0.jar即可启动jar包，并设置启动的内存

- SpringBoot项目部署方式-war方式
1. 修改SpringbootApplication启动类，添加如下规定代码。
```
添加@ServletComponentScan注解，并且继承 SpringBootServletInitializer
```
2. 修改pom.xml文件，添加打包成war的声明，并将spring-boot-starter-tomcat修改为 provided方式，以避免和独立 tomcat 容器的冲突。
```
<!--添加打包成war的声明-->
<packaging>war</packaging>
<!--将spring-boot-starter-tomcat修改为provided方式-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```
3. 命令行切换到项目所在目录，执行mvn clean package命令即可。

4. 重命名war包，然后进行部署，如果用Springboot-0.0.1-SNAPSHOT.war这个文件名进行部署，那么访问的时候就要在路径上加上 Springboot-0.0.1-SNAPSHOT，较为麻烦。

5. 若将其重命名为root.war，然后放进tomcat中的webapps目录即可。root.war 并不是指访问的时候要使用/root/hello，而是直接使用/hello即可进行访问，因为root表示为根路径。

- SpringBoot项目支持JSP
1. 构建项目，添加SpringBoot对JSP支持的依赖。
```
<!-- tomcat依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-jasper</artifactId>
</dependency>
<!-- servlet依赖-->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
</dependency>
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jstl</artifactId>
</dependency>
```
2. 配置支持JSP的配置文件application.properties，用于视图重定向jsp文件的位置。
```
spring.mvc.view.prefix=/WEB-INF/jsp/
spring.mvc.view.suffix=.jsp
```
3. 编写controller，注意此时注解要用@controller，不能使用@RestController，例如：
```
@RequestMapping("/hello")
public String hello(Model m) {
    m.addAttribute("now", DateFormat.getDateTimeInstance().format(new Date()));
    return "hello";
}
引伸：Springboot注解：@Controller和@RestController的区别？
1：使用@Controller注解在对应的方法上时，视图解析器可以解析返回的jsp、html页面，并且跳转到相应的页面，若返回json等内容到页面时，则需要加上@ResponeBody注解。
2：使用@RestController注解在对应的方法上时，就不能返回jsp、html页面，视图解析器无法进行解析，@RestController是spring4里的新注解，是@ResponseBody和@Controller的缩写。
```
4. 在项目工程下src/main目录下添加webapp/WEB-INF/jsp文件夹，里面添加jsp页面。
```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>title</title>
</head>
<body>
    Hi JSP. 现在时间是  ${now}
</body>
</html>
```
- SpringBoot项目全局异常处理
1. 在Springboot项目中,代码出现异常会 跳转到error页面进行错误展示，对用户和前端都不够友好，全局异常处理的目的是希望以更友好的方式来显示异常。
```
Springboot中的全局异常处理是通过@ControllerAdvice和@ExceptionHandler这两个注解来实现的。
@ControllerAdvice：增强型控制器，对于控制器的全局配置放在同一个位置，全局异常的注解，注解在类上。
@ControllerAdvice：默认只会处理controller层抛出的异常，若需要处理service层的异常，需要自定义异常并继承RuntimeException类，然后@ExceptionHandle(MyException即可。
@ExceptionHandler：指明需要处理的异常类型以及子类，注解在方法上面。一个方法处理多个异常类的异常@ExceptionHandler(value={RuntimeException.class,MyRuntimeException.class})@ExceptionHandler注解的方法，会根据抛出异常类去寻找处理方法，如果没有，就往上找父类，直到找到为止。
```
- SpringBoot项目配置端口和上下文路径
1. 通过修改resources下的application.properties等配置文件即可。
```
server.port=8888
server.context-path=/test
备注：Springboot 2.1.2 已经把server.context-path舍弃掉了，高版本中为server.servlet.context-path
```
- SpringBoot项目配置切换
1. 通过application.properties里的spring.profiles.active实现多配置支持与灵活切换
```
核心配置文件夹：application.properties
spring.mvc.view.prefix=/WEB-INF/jsp/
spring.mvc.view.suffix=.jsp
spring.profiles.active=pro
开发环境用的配置文件：application-dev.properties
server.port=8080
server.context-path=/test
生产环境用的配置文件：application-pro.properties
server.port=80
server.context-path=/
```
2. 除了可以通过修改application.properties配置文件进行切换，还可以在部署环境下，通过指定不同的参数进而指定要生效的配置文件。
```
java -Xms128m -Xmx512m -jar eureka-server-1.0.0.jar --spring.profiles.active=dev
```
- SpringBoot项目 application.yml配置文件
1. 在Springboot框架中，除了支持application.properties配置文件外，Springboot框架还支持application.yml格式，其两者都是Springboot框架中常用的配置文件，二者主要在于写法规范上的区别。
```
spring.mvc.view.prefix=/WEB-INF/jsp/
spring.mvc.view.suffix=.jsp
server.port=8888
server.servlet.context-path=/test
```
```
# application.yml配置文件写法：
spring:
   mvc:
    view:
        prefix: /WEB-INF/jsp/
        suffix: .jp
server:
   port: 8888
   servlet:
   context-path: /test
注意：
1：在yml文件里面所有的配置，相同的级别只能出现一次。
2：在yml文件里面如果需要进行赋值那么必须是要在“：”后面进行一个spacebar键的缩进。
3：properties文件和yml文件之间存在排斥性，最好不要同时使用。
4：在properties文件中的“.”在yml文件里面要全部换成“：”进行连接，并且每一级之间必须换行，在第二级开始前应该进行一个Tab键的缩进，但若为同级则就不需要进行进。
```


