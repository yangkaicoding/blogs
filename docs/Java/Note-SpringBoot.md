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
4：在properties文件中的“.”在yml文件里面要全部换成“：”进行连接，并且每一级之间必须换行，在第二级开始前应该进行一个Tab键的缩进，但若为同级则就不需要进行缩进。
```
- SpringBoot持久层支持
- JPA

&emsp;&emsp;JPA(Java Persistence API)是SUN公司官方提供的Java持久化规范。它为Java开发人员提供了一种对象/关系映射工具来管理Java应用中的关系数据。它的出现主要是为了简化现有的持久化开发工作和整合ORM技术，尤其是在充分吸收了现有的Hibernate，TopLink，JDO等ORM框架的基础上发展而来的，具有易于使用，伸缩性强等优点。

&emsp;&emsp;JPA是一套规范，而不是一套产品，而像Hibernate，TopLink，JDO等ORM框架则是一套产品，如果说这些产品实现了JPA的规范，那么我们就可以称他们为JPA的实现产品。

&emsp;&emsp;Spring Data JPA 是Spring基于ORM框架，JPA规范的基础上封装的一套JPA应用框架，可使开发者使用极简的代码即可实现对数据库的访问和操作，同时它提供了包括增删改查等在内的常用功能，且易于扩展，可以极大的提高开发效率。

1. 构建项目，添加SpringBoot对JPA支持的依赖。
```java
<!-- mysql的依赖-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.21</version>
</dependency>
<!-- jpa的依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```
2. 配置支持JPA的配置文件application.properties。
```java
#数据源设置
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/how2java?characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
#JPA相关配置
spring.jpa.properties.hibernate.hbm2ddl.auto=update
spring.jpa.show-sql=true
```
3. 构建实体类及对应的DAO层，详情见示例项目project_springboot_jpa详情。

- MyBatis注解方式
1. 构建项目，添加SpringBoot对MyBatis支持的依赖。
```java
<!-- mysql的依赖-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.21</version>
</dependency>
<!-- mybatis的依赖-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.1.1</version>
</dependency>
```
2. 配置支持MyBatis的配置文件application.properties。
```java
#数据源设置
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/how2java?characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```
3. 构建实体类及对应的Mapper层，详情见示例项目project_springboot_mybatis_annotation详情

- MyBatis xml文件配置方式
1. 构建项目，添加SpringBoot对MyBatis支持的依赖。
```java
<!-- mysql的依赖-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.21</version>
</dependency>
<!-- mybatis的依赖-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.1.1</version>
</dependency>
```
2. 配置支持MyBatis的配置文件application.properties。
```java
#数据源设置
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/how2java?characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
#mybatis
mybatis.mapper-locations=classpath:mapper/**/*.xml
#实体扫描，多个package用逗号或分号分隔
mybatis.type-aliases-package=com.how2java.springboot.entity
```
3. 添加MyBatis.xml配置文件。
```java
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="cn.vpclub.how2j.springboot.mybatis.xml.mapper.CategoryMapper">
</mapper>
```
4. 构建实体类及对应的Mapper层，详情见示例项目project_springboot_mybatis_xml详情。

- SpringBoot 增删改查+分页查询
&emsp;&emsp;JPA新增和修改所采用的都是save方法，它根据实体类的id是否为0来判断是进行增加还是修改。

&emsp;&emsp;MyBatis采用sql语句来实现增删改查，其就是调用不同的sql语句，分页查询需要增加pageHelper的插件支持，并添加pageHelperConfig配置类。

```java
<!-- pageHelper的依赖-->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>4.1.6</version>
</dependency>
```
```java
/**
* PageHelper 配置类
*
* @author: 杨凯
* @since: 2019/10/11 10:23
*/
@Configuration
public class PageHelperConfig {
    /**
     * @Bean 表示启动PageHelper这个拦截器
     * @configuration 表示PageHelperConfig这个类是用来做配置的
     */
    @Bean
    public PageHelper pageHelper() {
        PageHelper pageHelper = new PageHelper();
        Properties properties = new Properties();
        //offsetAsPageNum，设置为true时，会将RowBounds第一个参数offset当成pageNum页码使用
        properties.setProperty("offsetAsPageNum", "true");
        //rowBoundsWithCount,设置为true时，使用RowBounds分页会进行count查询
        properties.setProperty("rowBoundsWithCount", "true");
        //reasonable：启用合理化时，如果pageNum<1会查询第一页，如果pageNum>pages会查询最后一页
        properties.setProperty("reasonable", "true");
        pageHelper.setProperties(properties);
        return pageHelper;
    }
}
```
- SpringBoot单元测试
1. 构建项目，添加junit单元测试和sping-boot-starter-test的依赖。
```java
<!--单元测试的依赖-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
<!--spring-boot-starter-test的依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>  
```
2. 添加测试类，以用于测试接口是否正确。
```java
@RunWith(SpringRunner.class)
@SpringBootTest(classes = SpringbootApplication.class)
public class TestJPA {
    @Autowired
    private CategoryDAO categoryDAO;
    @Test
    public void test() {
        List<Category> categories = categoryDAO.findAll();
        for (Category category : categories) {
            System.out.println("category.getName：" + category.getName());
        }
    }
}
```
- SpringBoot文件上传下载
1. 构建项目，添加文件上传相关配置。
```java
#文件上传配置
# 最大支持文件大小
spring.http.multipart.max-file-size=100Mb
# 最大支持请求大小
spring.http.multipart.max-request-size=100Mb
```
2. 添加文件上传下载方法
```java
@Slf4j
@RestController
@RequestMapping("/file")
public class FileLoadController {

	@Value("${system.constant.filePath}")
	private String uploadPath;

	/**
	 * 文件上传 -通用
	 *
	 * @param file
	 * @param request
	 * @return
	 */
	@ApiOperation("上传")
	@RequestMapping(value = "/upload")
	public Result uploadImg(MultipartFile file, HttpServletRequest request) {

		log.info("文件名称，{}", file.getOriginalFilename());

		//上传文件存储路径
		String filePath = uploadPath;
		//设置上传文件时间
		String uploadDate = DateUtils.format(new Date(), Constant.YEARMONTHDAY);

		Map<String, Object> fileMap = new ConcurrentHashMap<>();

		//判断文件是否为图片
		String fileType = null;
		if (!isImage(file)) {
			fileType = "file";
		} else {
			fileType = "image";
		}
		filePath = filePath + "/" + fileType + "/" + uploadDate;
		String fileName = file.getOriginalFilename();

		String oldFileName = fileName;
		//文件后缀
		String suffixName = fileName.substring(fileName.lastIndexOf("."), fileName.length());
		//生成新的文件名称
		fileName = getUUID() + suffixName;
		fileMap.put("fileName", oldFileName);

		File localFile = new File(filePath);
		if (!localFile.exists()) {
			boolean isCreated = localFile.mkdirs();
			if (!isCreated) {
				//目标上传目录创建失败,可做其他处理,例如抛出自定义异常等,一般应该不会出现这种情况。
				return new Result().error("文件目录创建失败");
			}
		}
		localFile = new File(filePath + "/" + fileName);
		try {
			file.transferTo(localFile);
			fileMap.put("filePath", fileType + "/" + uploadDate + "/" + fileName);
			return new Result().ok(JSONUtil.toJsonStr(fileMap));
		} catch (Exception e) {
			log.error("文件上传异常" + e);
			return new Result().error("该文件上传异常：" + oldFileName);
		}
	}

	/**
	 * 文件下载 - 通用
	 *
	 * @param filePath
	 * @param fileName
	 * @param response
	 */
	@ApiOperation("下载")
	@RequestMapping(value = "/download")
	public void download(String filePath, String fileName, HttpServletResponse response) {
		String realPath = filePath;
		log.info("realPath:{}", realPath);
		try {
			FileUtil.downLoad(uploadPath + "/" + filePath, new String(fileName.getBytes(), "ISO8859-1"), response);
		} catch (UnsupportedEncodingException e) {
			log.error("文件下载错误,{}", e);
		}
	}

	/**
	 * 生成UUID
	 *
	 * @return
	 */
	public static String getUUID() {
		UUID uuid = UUID.randomUUID();
		String str = uuid.toString();
		String uuidStr = str.replace("-", "");
		return uuidStr;
	}

	/**
	 * 判断文件是否为图片
	 *
	 * @param file
	 * @return
	 */
	private boolean isImage(MultipartFile file) {
		boolean flag = false;
		try {
			InputStream is = file.getInputStream();
			BufferedImage bi = ImageIO.read(is);
			if (null == bi) {
				return flag;
			}
			is.close();
			flag = true;
		} catch (Exception e) {
			log.error("判断文件是否为图片错误：{}", e);
		}
		return flag;
	}

	/**
	 * 判断是否为允许的上传文件类型,true表示允许
	 */
	private boolean checkFile(String fileName) {
		//设置允许上传文件类型
		String suffixList = "txt,doc,docx,xls,xlsx,pdf,ppt,pptx,zip,rar";
		//获取上传的文件后缀名
		String suffix = fileName.substring(fileName.lastIndexOf(".") + 1, fileName.length());
		if (suffixList.contains(suffix.trim().toLowerCase())) {
			return true;
		}
		return false;
	}
}
```
- SpringBoot Restful风格

&emsp;&emsp;Rest即Representational State Transfer的缩写，可译为“表现层状态转化”。Rest最大的几个特点为：资源、同一接口、URL和无状态。

&emsp;&emsp;Restful是一种网络应用程序的设计风格和开发模式，基于Http，可以使用XML格式定义或JSON格式定义。Restful适用于移动互联网厂商作为业务使用接口的场景，实现第三方OTT调用移动网络资源的功能，动作类型为新增、变更、删除所调用的资源。

- Restful的特点：
1. 每一个URL代表一种资源。
2. 资源的表现形式是XML获得HTML。
3. 通过操作资源的表现形式来操作资源。
4. 客户端与服务端之间的交互在请求之间是无状态的，从客户端到服务端的每个请求都必须包含理解请求所必须的信息。
5. 客户端使用GET、POST、PUT、DELETE等4个表示操作方式的动词来对服务端进行操作，GET用来获取资源，POST用来新建资源(也可用于资源更新)，PUT用来更新资源，DELETE用来删除资源。



