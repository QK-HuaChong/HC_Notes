# Spring Cloud Fegin --- 声明式REST调用

## 功能定位

>Feign是Netflix开发的声明式、模板化的HTTP客户端，其灵感来自Retrofit、JAXRS-2.0以及Websocket。Feign可帮助我们更加便捷、优雅地调用HTTPAPl。
>在Spring Cloud中，使用Feign非常简单—创建一个接口，并在接口上添加一些注解，代码就完成了。Feign支持多种注解，例如Feign自带的注解或者JAX-RS注解等。
>Spring Cloud对Feign 进行了增强，使Feign支持了Spring MVC注解，并整合了Ribbon和Eureka，从而让Feign的使用更加方便。

## 配置服务映射

- 一、首先在Server端创建相关的方法

````java
    /**
 * Created by cong on 2018/5/8.
 */
@RestController
public class LsgUserController {

    /*private static final Logger LOG = LoggerFactory.getLogger(LsgUserController.class);*/

    @Autowired
    private LsgUserRepository lsgUserRepository;

    @GetMapping("/{id}")
    public LsgUser findById(@PathVariable Long id){
        LsgUser lsgUser = this.lsgUserRepository.findById(id).orElse(null);
        return lsgUser;
    }

    @GetMapping("/name")
    public String showName(){
        /*LOG.info("Print information about Provider 1");*/
        return "Provider-1-";
    }
}
````

- 二、在Client定义服务映射接口

```java
   @FeignClient(name = "spring-lsg-provider")
public interface LsgConsumerFeigns {
    @RequestMapping(value = "/{id}",method = RequestMethod.GET)
    LsgUser findById(@PathVariable("id") Long id);
    @GetMapping("/name")
    String showName();
}
```

### 相关的属性

|属性名|描述|
|-----|---|
|value/name|指定FeignClient的名称，如果项目使用了Ribbon，name属性会作为微服务的名称，用于服务发现
|url|url一般用于调试，可以手动指定@FeignClient调用的地址|
|decode404|当发生http 404错误时，如果该字段位true，会调用decoder进行解码，否则抛出FeignException|
|configuration|Feign配置类，可以自定义Feign的Encoder、Decoder、LogLevel、Contract|
|fallback|定义容错的处理类，当调用远程接口失败或超时时，会调用对应接口的容错逻辑，fallback指定的类必须实现@FeignClient标记的接口|
|fallbackFactory|工厂类，用于生成fallback类示例，通过这个属性我们可以实现每个接口通用的容错逻辑，减少重复的代码|
|path|定义当前FeignClient的统一前缀|

- 三、在启动类上添加相关注解
  - @EnableDiscoveryClient
  - @EnableFeignClients

```java
    @SpringBootApplication
    @EnableFeignClients
    @EnableDiscoveryClient
    public class LsgConsumerApplication {

        public static void main(String[] args) {
            SpringApplication.run(LsgConsumerApplication.class, args);
        }

    }
```

### fallback 容错处理类

```java
@RestController
public class LsgConsumerController {

    private static final Logger LOG = LoggerFactory.getLogger(LsgConsumerController.class);

    @Autowired
    private RestTemplate restTemplate;

    @Autowired
    private LsgConsumerFeigns lsgConsumerFegin;


    @HystrixCommand(fallbackMethod = "findByIdFallback")
    @GetMapping("/name")
    public String findByName(){
        /*return this.restTemplate.getForObject("http://spring-lsg-provider/name",String.class);*/
        return this.lsgConsumerFegin.showName();
    }

    public String findByIdFallback(){
        return "Server termination";
    }
}
```
