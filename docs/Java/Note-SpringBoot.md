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
```java 
<!--添加打包成war的声明-->
<packaging>war</packaging>

<!--将spring-boot-starter-tomcat修改为 provided方式-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```
3. 命令行切换到项目所在目录，执行mvn clean package命令即可。
4. 重命名war包，然后部署，如果用Springboot-0.0.1-SNAPSHOT.war这个文件名进行部署，那么访问的时候就要在路径上加上 Springboot-0.0.1-SNAPSHOT，较为麻烦。将其重命名为root.war，然后放进tomcat中的webapps目录即可。root.war 并不是指访问的时候要使用/root/hello，而是直接使用/hello即可进行访问，因为root表示为根路径。

- SpringBoot支持JSP
1. 构建项目，添加SpringBoot对JSP支持的依赖。
```java
<!-- tomcat的支持-->
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