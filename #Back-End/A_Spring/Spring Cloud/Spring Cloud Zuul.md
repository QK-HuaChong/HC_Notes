# Spring Cloud Zuul --- 网关

## Zuul简介

>Zuul是Netlix开源的微服务网关，它可以和Eureka、Ribbon、Hystrix等组件配合使用。
>Zuul的核心是一系列的过滤器，这些过滤器可以完成以下功能。

- 身份认证与安全：识别每个资源的验证要求，并拒绝那些与要求不符的请求。
- 审查与监控：在边缘位置追踪有意义的数据和统计结果，从而带来精确的生产视图。
- 动态路由：动态地将请求路由到不同的后端集群。压力测试：逐渐增加指向集群的流量，以了解性能。
- 负载分配：为每一种负载类型分配对应容量，并弃用超出限定值的请求。
静态响应处理：在边缘位置直接建立部分响应，从而避免其转发到内部集群。
- 多区域弹性：跨越AWS Region进行请求路由，旨在实现ELB（Elastic Load Balancing）使用的多样化，以及让系统的边缘更贴近系统的使用者。

## 实现Zuul网关

### 相关依赖

```xml
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-zuul</artifactId>
    </dependency>
```

### 添加注解

- 在启动内上添加 **@EnableZuulProxy** 注解,声明这是Zuul代理

```java
    @SpringBootApplication
    @EnableZuulProxy
    public class LsgZuulApplication {

        public static void main(String[] args) {
            SpringApplication.run(LsgZuulApplication.class, args);
        }
    }
```

### 添加配置信息

```yml
server:
  port: 8766
spring:
  application:
    name: spring-lsg-zuul

eureka:
  client:
    serviceUrl:
      defaultZone:  http://user:password123@localhost:8761/eureka/
  instance:
      prefer-ip-address: true


```

#### Zuul对路由端点的配置

>在配置文件中指定服务的serviceId = 自定义路径

- routes 设置路由端点的路径
- ignored-services 忽略指定的服务

```yml
zuul:
  routes:
    spring-lsg-consumer: /consumer/**
  ignored-services: spring-lsg-provider
```

## Zuul的过滤器

>Zuul大部分功能都是通过过滤器来实现的。Zuul中定义了4种标准过滤器类型，这些过滤器类型对应于请求的典型生命周期。

- PRE：这种过滤器在请求被路由之前调用。可利用这种过滤器实现身份验证、在集群中选择请求的微服务、记录调试信息等。
- ROUTING：这种过滤器将请求路由到微服务。这种过滤器用于构建发送给微服务的请求，并使用Apache HtpClient 或Netfilx Ribbon 请求微服务。
- POST：这种过滤器在路由到微服务以后执行。这种过滤器可用来为响应添加标准的HTTP Header、收集统计信息和指标、将响应从微服务发送给客户端等。
- ERROR：在其他阶段发生错误时执行该过滤器。

### Zuul过滤器的生命周期

![Zuul过滤器的生命周期](img/sc-z-001.png)

### 自定义Zuul过滤器

- 创建类继承ZuulFilter，并重写其中的方法

- filterType：返回过滤器的类型。有pre、route、post、error等几种取值，分别对应上文的几种过滤器。详细可以参考com.netflix.zuul.ZuulFilter.- filterType()中的注释。
- filterorder：返回一个int值来指定过滤器的执行顺序，不同的过滤器允许返回相同的数字。
- shouldFilter：返回一个boolean值来判断该过滤器是否要执行，true表示执行，false表示不执行。
- run：过滤器的具体逻辑。本例中让它打印了请求的HTTP方法以及请求的地址。

```java
    public class LsgPreRequestLogFilter extends ZuulFilter {

    private static final Logger LOG = LoggerFactory.getLogger(LsgPreRequestLogFilter.class);

    @Override
    public String filterType() {
        return "pre";
    }

    @Override
    public int filterOrder() {
        return 1;
    }

    @Override
    public boolean shouldFilter() {
        return true;
    }

    @Override
    public Object run() throws ZuulException {
        RequestContext requestContext = RequestContext.getCurrentContext();
        HttpServletRequest request = requestContext.getRequest();
        LsgPreRequestLogFilter.LOG.info(String.format("send %s request to %s",request.getMethod(),request.getRequestURL()));
        return null;
    }
}
```

### 禁用过滤器

>设置zuul.\<SimpleClassName>.\<filterType>.disable=true，即可禁用SimpleClassName 所对应的过滤器。以过滤器org.springframework.cloud.netflix.zuul.filters.
>post.SendResponseFilter为例，只须设置zuul.SendResponseFilter.post.disable=true，即可禁用该过滤器。

## Zuul的容错与回退

