# Spring Cloud Ribbon 负载均衡

## 功能定位

>Ribbon是Netflix发布的负载均衡器，它有助于控制HTTP和TCP客户端的行为。为Ribbon 配置服务提供者地址列表后，Ribbon就可基于某种负载均衡算法，自动地帮助服务消费者去请求。Ribbon默认为我们提供了很多的负载均衡算法，例如轮询、随机等。当然，我们也可为Ribbon实现自定义的负载均衡算法。

## 为服务消费方整合Ribbon

### 添加依赖

```xml
    <!-- 
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-ribbon</artifactId>
        </dependency> 
    -->

    <!-- 该依赖中包含了Ribbon -->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
```

### 添加注解

>只须添加注解 *@LoadBalanced*注解，就可为RestTemplate整合Rib bon，使其具备负载均衡的能力。

```java
    @Bean
    @LoadBalanced
    public RestTemplate restTemplate(){
        return new RestTemplate();
    }
```

### 编写Controller

```java
   @RestController
    public class LsgConsumerController {

    private static final Logger LOG = LoggerFactory.getLogger(LsgConsumerController.class);

    @Autowired
    private RestTemplate restTemplate;

    @Autowired
    private LoadBalancerClient loadBalancerClient;

    @GetMapping("/name")
    public String findByName(){
        return this.restTemplate.getForObject("http://spring-lsg-provider/name",String.class);
    }

    @GetMapping("/user/{id}")
    public LsgUser findById(@PathVariable Long id){
        return this.restTemplate.getForObject("http://spring-lsg-provider/"+id,LsgUser.class);
}
```
