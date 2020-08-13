### 面试准备

- #### 自我介绍的要素：
1. 用简单的话说清楚自己主要擅长的技术栈及领域
2. 把重点放在自己在行的地方以及自己的优势之处
3. 重点突出自己的能力

&emsp;&emsp;备注：面试自我介绍并不需要死记硬背，记住要说的要点，面试的时候根据现场的情况临场发挥也是没有问题的，另外，网上一般建议的是准备好两份自我介绍：一份对hr说的，主要讲能突出自己的经历，会的编程技术一语带过；另一份对技术面试官说的，主要讲自己会的技术细节和项目经验。

```
面试官，您好，我叫杨凯，毕业于武汉商学院，我目前有3年多的工作经验，能熟练使用Spring、SpringBoot、SpringCloud、MyBatis及MyBatis-plus等主流框架，离开上一家公司是因为我想寻求更好的发展机会，在上一家公司我经历了12个开发项目，有着较为丰富的分布式服务开发经验，也曾独立负责过整个项目，熟悉整个项目的开发及部署流程，工作之余，我比较喜欢通过博客总结和分享自己所学的知识，因为我认为学习的关键在于出，而不再与入，生活中我是一个比较积极乐观的人，业余时间比较喜欢运动去方式自己，期待能成为贵公司的一员，谢谢。
```

- #### 面经：
- ##### Spring基础面试题集合

1.   什么是Spring？
```
Spring是一个开源应用框架，旨在降低应用程序开发的复杂度，它是轻量级、松散耦合的；它具有分层体系结构，允许用户选择组件，同时还为J2EE应用程序开发提供了一个有凝聚力的框架；它还可以集成其他框架，如 Structs、Hibernate等，所以又称为框架的框架。
```
2.   Spring框架优势？
```
1：由于Spring的分层架构，用户可以自由选择自己需要的组件。
2：Spring支持 POJO(Plain Old Java Object)编程，从而具备持续集成和可测试性。
3：由于依赖注入和控制反转，JDBC 得以简化。
4：开源免费
```
3.   Spring有哪些不同的功能？
```
1：IOC：控制反转
2：AOP：面向切面编程可以将应用业务逻辑和系统服务分离，以实现高内聚。
3：MVC：对web应用提供了高度可配置性，其他框架的集成也十分方便。
4：容器：Spring负责创建和管理对象（Bean）的生命周期和配置。
5：JDBC异常：Spring的JDBC抽象层提供了一个异常层次结构，简化了错误处理策略。
6：事务管理：提供了用于事务管理的通用抽象层。Spring 的事务支持也可用于容器较少的环境。
```
4.   Spring的AOP及IOC原理？
```
IOC：控制反转，是一种设计思想，就是将原本在程序中手动创建对象的控制权，交由Spring框架来管理。IOC容器是Spring用来实现IOC的载体，Ioc容器实际就是个Map集合，Map中存放的是各个对象。将对象之间的相互依赖关系交给IOC容器去管理，并由IOC容器完成对象的注入，这样可以很大程度的简化应用的开发，把应用从复杂的依赖关系中解放出来，IOC容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可。
AOP：面向切面编程，能够将那些与业务无关，却为业务模块所共同调用的逻辑或责任(例如：事务处理、日志管理、权限控制等)封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可拓展性和可维护性，Spring AOP就是基于动态代理的，如果要代理的对象实现了某个接口，那么Spring AOP会使用JDK Proxy去创建对象，而对于没有实现接口的对象，就无法使用JDK Proxy去进行代理了，这时候Spring AOP会使用Cglib生成一个被代理对象的子类来作为代理。
```
****

- ##### SpringMvc基础面试题集合

1.   SpringMvc框架的概述及实现原理？

&emsp;&emsp; MVC是一种设计模式，SpringMVC可以帮助我我们进行更为简洁的wen层开发，并且它天生与Spring框架集成，Spring mvc下我们一般把后端分为service层（处理业务）、Dao层(数据库操作)、Entity层（实体类）、Controller层（控制层，返回数据给前台页面）。
```
MVC是一种设计模式，SpringMVC可以帮助我我们进行更为简洁的wen层开发，并且它天生与Spring框架集成，Spring mvc下我们一般把后端分为service层（处理业务）、Dao层(数据库操作)、Entity层（实体类）、Controller层（控制层，返回数据给前台页面）。
SpringMvc 实现原理：
1：客户端（浏览器）发送请求，直接请求到DispatcherServlet
2：Dispatcher根据请求的信息调用HandlerMapper，解析请求对应的Handler
3：解析到对应的Handler后（也就是我们常说的Controller控制器）开始由HandlerAdapter(处理器适配器)处理
4：HandlerAdapter会根据Handlel去调用真正的处理器来处理请求，并处理相应的业务逻辑。
5：处理器处理完业务后，会返回一个ModelAndView对象 model是返回数据的对象，view是逻辑上的view
6：ViewReslover（视图解析器）会根据逻辑view查找实际的view
7：DispatcherServlet把返回的Model传给View进行视图渲染
8：把View返回给客户端（浏览器）
```
****

- ##### SpringBoot基础面试题集合

1.  什么是SpringBoot?
```
Spring Boot是Spring开源组织下的子项目，是Spring组件一站式解决方案，主要是简化了使用Spring的难度，简省了繁重的配置，提供了各种启动器，开发者能快速上手。
```
2.  SpringBoot常用注解?
```
启动注解： 
@SpringBootApplication，它也是SpringBoot的核心注解，主要组合包含了以下3个注解：
@SpringBootConfiguration：组合了 @Configuration 注解，实现配置文件的功能。
@EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能：@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class })。
@ComponentScan：Spring组件扫描。
前端控制器注解：
@Controller：控制器，处理http请求。
@RestController：复合注解，相当于@ResponseBody+@Controller合在一起的作用,RestController使用的效果是将方法返回的对象直接在浏览器上展示成json格式。
@RequestBody：通过HttpMessageConverter读取Request Body并反序列化为Object（泛指）对象。
@ResponseBody：通过适当的转换器转换为指定的格式之后，写入到response对象的body区，通常用来返回JSON数据或是XML数据。
@GetMapping：将get请求映射到特定处理程序的方法上。
@PostMapping：将post请求映射到特定处理程序的方法上。
@RequestMapping：将HTTP请求映射到MVC和REST控制器的处理方法上。
请求参数注解：
@PathVariable：获取url中的数据
@RequestParam：获取请求参数的值
@服务类注解：
@Service：用于标注服务层组件,表示定义一个bean。
@Service：使用时没有传参数，Bean名称默认为当前类的类名，首字母小写。
@Service：(“serviceBeanId”)或@Service(value=”serviceBeanId”)使用时传参数，使用value作为Bean名字。
实体类注解：
@Table(name = "dataBaseName")：注释在实体类上，映射数据库中相应的表。
@Id、@Column：注释在实体类中的字段上
自动导入注解：
@Autowired：注解作用在构造函数、方法、方法参数、类字段以及注解上
@Autowired注解可以实现Bean的自动注入
事务注解：
@Transactional
在Spring中，事务有两种实现方式，分别是编程式事务管理和声明式事务管理两种方式：
编程式事务管理：编程式事务管理使用TransactionTemplate或者直接使用底层的PlatformTransactionManager。对于编程式事务管理，spring推荐使用TransactionTemplate。
声明式事务管理：建立在AOP之上的。其本质是对方法前后进行拦截，然后在目标方法开始之前创建或者加入一个事务，在执行完目标方法之后根据执行情况提交或者回滚事务，通过@Transactional就可以进行事务操作，更快捷而且简单，推荐使用。
全局异常处理注解：
@ControllerAdvice：定义全局异常处理
@ExceptionHandler：声明异常处理方法
```
3. SpringBoot框架优劣势?
```
优势：
1：更容易上手，提升了开发效率，为Spring开发提供一个更快、更广泛的入门体验。
2：摒弃了spring以往项目中大量繁琐的配置，遵循约定大于配置的原则，开箱即用，远离繁琐的配置，极大的降低了项目搭建的复杂度。
3：提供了一系列大型项目通用的非业务性功能，例如：内嵌服务器、安全管理、运行数据监控、运行状况检查和外部化配置等。
4：没有代码生成，也不需要XML配置。
5：避免大量的Maven导入和各种版本冲突。
6：让编码变得简单，让配置变得简单，让部署变得简单，让监控变得简单。
劣势：
1：依赖太多，一个spring boot项目就有很多M
2：缺少服务的注册和发现等解决方案
3：缺少监控集成方案，安全管理方案
```
4.  SpringBoot应用场景?
```
1：微服务
2：Java web应用
``` 
5.  SpringBoot配置加载顺序?
```
1：properties文件
2：YAML文件
3：系统环境变量
4：命令行的参数
```
6.  什么是YAML文件？YAML文件配置的优势在哪里？
```
1：配置有序，在一些特殊的场景下，配置有序很关键
2：支持数组，在数组中的元素可以是基本数据类型也可以是对象。
```
7.  Spring Boot 中如何解决跨域问题？

&emsp;&emsp; 跨域可以在前端通过 JSONP 来解决，但是 JSONP 只可以发送 GET 请求，无法发送其他类型的请求，在 RESTful 风格的应用中，就显得非常鸡肋，因此我们推荐在后端通过（CORS，Cross-origin resource sharing） 来解决跨域问题。这种解决方案并非 SpringBoot 特有的，在传统的 SSM 框架中，就可以通过 CORS 来解决跨域问题，只不过之前我们是在 XML 文件中配置 CORS ，现在可以通过实现WebMvcConfigurer接口然后重写addCorsMappings方法解决跨域问题。
```
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("*")
                .allowCredentials(true)
                .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS")
                .maxAge(3600);
    }
}
```
&emsp;&emsp; 项目中前后端分离部署，所以需要解决跨域的问题。我们使用cookie存放用户登录的信息，在spring拦截器进行权限控制，当权限不符合时，直接返回给用户固定的json结果。当用户登录以后，正常使用；当用户退出登录状态时或者token过期时，由于拦截器和跨域的顺序有问题，出现了跨域的现象。我们知道一个http请求，先走filter，到达servlet后才进行拦截器的处理，如果我们把cors放在filter里，就可以优先于权限拦截器执行。
```
@Configuration
public class CorsConfig {
    @Bean
    public CorsFilter corsFilter() {
        CorsConfiguration corsConfiguration = new CorsConfiguration();
        corsConfiguration.addAllowedOrigin("*");
        corsConfiguration.addAllowedHeader("*");
        corsConfiguration.addAllowedMethod("*");
        corsConfiguration.setAllowCredentials(true);
        UrlBasedCorsConfigurationSource urlBasedCorsConfigurationSource = new UrlBasedCorsConfigurationSource();
        urlBasedCorsConfigurationSource.registerCorsConfiguration("/**", corsConfiguration);
        return new CorsFilter(urlBasedCorsConfigurationSource);
    }
}
```
8.  运行SpringBoot有哪几种方式？
```
1：打包后用命令或者放到容器中运行
2：用Maven/Gradle插件运行
3：直接执行main方法运行
```
9.  SpringBoot中如何实现定时任务？

&emsp;&emsp; 定时任务也是一个常见的需求，SpringBoot中对于定时任务的支持主要还是来自Spring框架。
```
在 SpringBoot中使用定时任务主要有两种不同的方式，一个就是使用 Spring中的@Scheduled注解，另一个则是使用第三方框架Quartz，按照Quartz的方式，定义Job和Trigger即可。
```
10.  SpringBoot和SpringCloud的区别？
```
1：SpringBoot专注于快速方便的开发单个个体微服务。
2：SpringBoot可以离开SpringCloud独立使用开发项目， 但是SpringCloud离不开SpringBoot，属于依赖的关系。
3：SpringBoot专注于快速、方便的开发单个微服务个体，SpringCloud关注全局的服务治理框架。
4：SpringCloud是关注全局的微服务协调整理治理框架，它将SpringBoot开发的一个个单体微服务整合并管理起来，为各个微服务之间提供，配置管理、服务发现、断路器、路由、微代理、事件总线、全局锁、决策竞选、分布式会话等等集成服务。
```
**** 

- ##### SpringCloud基础面试题集合

1.  为什么要使用SpringCloud？

&emsp;&emsp; 不论是商业应用还是用户应用，在业务初期都很简单，我们通常会把它实现为单体结构的应用。但是，随着业务逐渐发展，产品思想会变得越来越复杂，单体结构的应用也会越来越复杂。这就会给应用带来如下的几个问题：
```
1: 代码结构混乱：业务复杂，导致代码量很大，管理会越来越困难。同时，这也会给业务的快速迭代带来巨大挑战；
2: 开发效率变低：开发人员同时开发一套代码，很难避免代码冲突。开发过程会伴随着不断解决冲突的过程，这会严重的影响开发效率；
3: 排查解决问题成本高：线上业务发现 bug，修复 bug 的过程可能很简单。但是，由于只有一套代码，需要重新编译、打包、上线，成本很高。
```
2.  什么是SpringCloud?
```
Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、智能路由、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。
```
3.  SpringCloud框架优劣势？
```
优势：
1：产出于Spring大家族，Spring在企业级开发框架中无人能敌，来头很大，可以保证后续的更新、完善。
2：组件丰富，功能齐全。Spring Cloud 为微服务架构提供了非常完整的支持。例如、配置管理、服务发现、断路器、微服务网关等。
3：服务拆分粒度更细，耦合度比较低，有利于资源重复利用，有利于提高开发效率可以更精准的制定优化服务方案，提高系统的可维护性。
4：减轻团队的成本，可以并行开发，不用关注其他人怎么开发，先关注自己的开发。
劣势：
1：微服务过多，治理成本高，不利于维护系统。
2：分布式系统开发的成本高（容错，分布式事务等）对团队挑战大。
```
4.  SpringCloud和dubbo区别?
```
1：调用方式：dubbo是RPC，SpringCloud是Rest Api。
2: 注册中心：dubbo 是zookeeper，Spring Cloud可以是zookeeper或其他。
3：服务网关：dubbo本身没有实现，只能通过其他第三方技术整合，springcloud有Zuul路由网关，作为路由服务器。
```
5.  什么是SpringCloud Gateway?
```
Spring Cloud Gateway是Spring Cloud官方推出的第二代网关框架，取代Zuul网关。网关作为流量的控制，在微服务系统中有着非常作用，网关常见的功能有路由转发、权限校验、限流控制等作用。
```
6.  springCloud五大组件?
```
1：服务发现--Netflix Eureka
组件组成：Eureka服务端和Eureka客户端，Eureka服务端用作服务注册中心，支持集群部署，Eureka客户端是一个java客户端，用来处理服务注册与发现。
工作原理：在应用启动时，Eureka客户端向服务端注册自己的服务信息，同时将服务端的服务信息缓存到本地。客户端会和服务端进行周期性的进行心跳交互进行更新服务信息。
2：客户端负载均衡--Netflix Ribbon
工作原理：提供客户端的软件负载均衡算法，它基于Http和Tcp的客户端负载均衡，使得面向REST请求时变换为客户端的负载服务调用。
3：熔断器--Netflix Hystrix
工作原理：断路器，保护系统，控制故障范围。为了保证高可用，单个服务通常会集群部署，当网络或者其他原因导致单个服务出现问题，调用这个服务就会出现线程阻塞，此时如果大量请求进入，Servlet容器的线程资源就会消耗完毕，最终导致服务瘫痪。服务与服务之间的依赖，故障会传播，对整个微服务框架造成灾难性的严重后果，这个就是服务故障的“雪崩”效应。
4：服务网关--Netflix Zuul
工作原理：api网关，路由，负载均衡等作用，类似于Nginx可以实现反向代理，在微服务架构中，后端服务往往不直接暴露给前端，而是通过一个Api网关根据请求的Url，路由到响应的服务（MVC机制）。当添加Api网关后，在第三方调用端和服务提供方之间就创建了一面墙，这面墙直接与调用方进行通信进行权限控制后再将请求均衡分发给后台服务端。
5：分布式配置--Spring Cloud Config
工作原理：提供服务端和客户端，服务器存储后端的默认实现使用git，因此它轻松支持标签版本的配置环境。Config是静态配置的如果需要动态配置，可以使用spring cloud bus进行动态配置更新。
```
7.  服务注册和发现是什么意思？
```
当我们开始一个项目时，我们通常在属性文件中进行所有的配置。随着越来越多的服务开发和部署，添加和修改这些属性变得更加复杂。有些服务可能会下降，而某些位置可能会发生变化。手动更改属性可能会产生问题。Eureka 服务注册和发现可以在这种情况下提供帮助。由于所有服务都在 Eureka 服务器上注册并通过调用 Eureka 服务器完成查找，因此无需处理服务地点的任何更改和处理。
```
****

- ##### 数据库面试题集合

1.   什么是redis?
```
Redis是完全开源免费的，遵循BSD协议，是一个高性能的key-value的数据库。
```
1.   redis的特点？
```
1：redis支持数据的持久化，可以将内存中的数据保存到磁盘中，重启的时候可以再次加载进行使用。
2：redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
3：redis支持数据的备份，即master-slave模式的数据备份。
```
2.  redis的五种数据结构及应用场景？
```
redis支持五种数据类型：
1：String(字符串)
场景：一般用于复杂的计数功能缓存或最常规的get/set操作，value可以是字符串也可以是数字。
2：hash(哈希)
场景：hash的数据类型，其value存放的是结构化的对象，一般用于操作某个字段，例如在做单点登录时就是采用这种数据结构存储用户信息，以cookid作为key,设置30分钟为缓存过期时间，能很好的模拟出类似session的效果。
3：List(列表)
场景：List的数据类型，可以做简单的消息队列的功能，采用先进先出的原则，List可以很好的完成排队；另外可以利用range命令，做基于redis的分页功能，性能极佳，用户体验好。
4：set(集合)
场景：Set的数据类型，存放的是不重复值的数据集合，可以用来做全局去重的功能。
5：zset(有序集合)
场景：zset的数据类型，多了一个权重参数score，集合中的元素能够按照score进行排列，可以做排行榜应用。
```
**** 

- ##### 前后端分离项目数据交互实现(shiro)

  &emsp;&emsp;一般情况下，web项目都是通过session进行认证，每次请求数据时，都会把jsessionid放在cookie中，以便与服务端保持会话；但在前后端分离项目中，是通过token进行认证（登录时，生成唯一的token凭证），每次请求数据时，都会把token放在head中，服务端通过解析token，进而确定用户身份及用户权限，数据通过json格式进行交互。

1. 步骤1：继承AuthenticatingFilter抽象类即可。
```java
public class Oauth2Filter extends AuthenticatingFilter {
}
```
2. 步骤2：所有请求全部拒绝访问
```java
    @Override
    protected boolean isAccessAllowed(ServletRequest request, ServletResponse response, Object mappedValue) {
        //允许optitons请求
        if(((HttpServletRequest) request).getMethod().equals(RequestMethod.OPTIONS.name())){
            return true;
        }

        return false;
    }
```
3. 步骤3：拒绝访问的请求，会调用onAccessDenied方法，onAccessDenied方法会先获取token，在调用executeLogin方法。
```java
    @Override
    protected boolean onAccessDenied(ServletRequest request, ServletResponse response) throws Exception {
        //获取请求token，如果token不存在，直接返回401
        String token = getRequestToken((HttpServletRequest) request);

        if(StringUtils.isBlank(token)){
            HttpServletResponse httpResponse = (HttpServletResponse) response;
            httpResponse.setContentType("application/json;charset=utf-8");
            httpResponse.setHeader("Access-Control-Allow-Credentials", "true");
            httpResponse.setHeader("Access-Control-Allow-Origin", HttpContextUtils.getOrigin());

            String json = new Gson().toJson(new Result().error(ErrorCode.UNAUTHORIZED));

            httpResponse.getWriter().print(json);

            return false;
        }
        if(redisUtils == null){
            this.redisUtils = (RedisUtils) SpringContextUtils.getBean("redisUtils");
        }
        if(springContextUtils == null || expireTime == null || expireTime.longValue() == 0  ){
            this.springContextUtils = (SpringContextUtils) SpringContextUtils.getBean("springContextUtils");
            expireTime = Long.valueOf(this.springContextUtils.getProperty("dongfeng.expireTime"));
        }
        String userId = (String) this.redisUtils.get(token);
        if(StringUtil.isNotEmpty(userId)){
            //重新设置token过期时间 以免操作过程中超时
            this.redisUtils.set(token,String.valueOf(userId),expireTime);
        }
        return executeLogin(request, response);
    }

    /**
     * 获取请求的token
     */
    private String getRequestToken(HttpServletRequest httpRequest){
        //从header中获取token
        String token = httpRequest.getHeader(Constant.TOKEN_HEADER);

        //如果header中不存在token，则从参数中获取token
        if(StringUtils.isBlank(token)){
            token = httpRequest.getParameter(Constant.TOKEN_HEADER);
        }
        return token;
    }
```
4. 阅读AuthenticatingFilter抽象类中的executeLogin方法，我们发现调用了subject.login(token)，这是shiro的登录方法，且需要token参数，因此我们自定义OAuth2Token类，只要实现AuthenticationToken接口，即可。
```java
public class Oauth2Token implements AuthenticationToken {
}
```
5. 定义OAuth2Realm类，并继承AuthorizingRealm抽象类，调用subject.login(token)时，则会调用doGetAuthenticationInfo方法，进行登录。
```java
    /**
     * 认证(登录时调用)
     */
    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
        String accessToken = (String) token.getPrincipal();
        //根据accessToken，查询用户信息
        String userId = (String) redisUtils.get(accessToken);
        //token失效
        if (StringUtil.isEmpty(accessToken) || StringUtil.isEmpty(userId)) {
            throw new IncorrectCredentialsException(MessageUtils.getMessage(ErrorCode.TOKEN_INVALID));
        }
        //查询用户信息
        SysUserEntity userEntity = shiroService.getUser(Long.valueOf(userId));
        logger.info("userEntity------>" + JSON.toJSONString(userEntity));
        //转换成UserDetail对象
        UserDetail userDetail = ConvertUtils.sourceToTarget(userEntity, UserDetail.class);
        logger.info("userDetail------>" + JSON.toJSONString(userDetail));
        //获取用户对应的部门数据权限
        List<Long> deptIdList = shiroService.getDataScopeList(userDetail.getId());
        userDetail.setDeptIdList(deptIdList);

        //账号锁定
        if (userDetail.getStatus() == 0) {
            throw new LockedAccountException(MessageUtils.getMessage(ErrorCode.ACCOUNT_LOCK));
        }

        SimpleAuthenticationInfo info = new SimpleAuthenticationInfo(userDetail, accessToken, getName());
        return info;
    }
```
6. 若登录失败，则调用Oauth2Filter类中的onLoginFailure方法，进行失败处理，整个流程结束。
```java
    @Override
    protected boolean onLoginFailure(AuthenticationToken token, AuthenticationException e, ServletRequest request, ServletResponse response) {
        HttpServletResponse httpResponse = (HttpServletResponse) response;
        httpResponse.setContentType("application/json;charset=utf-8");
        httpResponse.setHeader("Access-Control-Allow-Credentials", "true");
        httpResponse.setHeader("Access-Control-Allow-Origin", HttpContextUtils.getOrigin());
        try {
            //处理登录失败的异常
            Throwable throwable = e.getCause() == null ? e : e.getCause();
            Result r = new Result().error(HttpStatus.SC_UNAUTHORIZED, throwable.getMessage());

            String json = new Gson().toJson(r);
            httpResponse.getWriter().print(json);
        } catch (IOException e1) {

        }
        return false;
    }
```
7. 若登录成功，则会调用doGetAuthorizationInfo方法，查询用户的权限，在调用具体的接口，整个流程结束。
```java
    /**
     * 授权(验证权限时调用)
     */
    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principals) {
        UserDetail user = (UserDetail) principals.getPrimaryPrincipal();

        //用户权限列表
        Set<String> permsSet = shiroService.getUserPermissions(user);

        SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();
        info.setStringPermissions(permsSet);
        return info;
    }
```



