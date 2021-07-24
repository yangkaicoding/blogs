#### 前言
&emsp;&emsp;Feign是声明式的web service客户端，它让微服务之间的调用变得更简单了，类似与controller调用service。SpringCloud集成了Ribbon和Eureka，可在使用Feign时提供负载均衡的http客户端。

#### 正文
- 引入Feign
- 
1. 构建项目，添加SpringCloud对feign支持的依赖。
```java
<!-- eureka 服务注册-->
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
<!-- feign远程调用服务 -->
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```
&emsp;&emsp;备注：因为feign底层使用了ribbon作为负载均衡的客户端，而ribbon的负载也是依赖于eureka获得各个服务的地址，所以要引入eureka-client。

2. SpringbootApplication启动类加上@FeignClient注解，以及@EnableDiscoveryClient。
```java
@EnableFeignClients
@EnableDiscoveryClient
@SpringBootApplication
public class ProductApplication {
    public static void main(String[] args) {
        SpringApplication.run(ProductApplication.class, args);
    }
}
```


