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
public class HelloController {

    @RequestMapping("/hello")
    public String hello(){
        System.out.println("访问来1了......");
        return "hello1";
    }

    @RequestMapping("/hjcs")
    public List<String> laowangs(String ids){
        List<String> list = new ArrayList<>();
        list.add("laowang1");
        list.add("laowang2");
        list.add("laowang3");
        return list;
    }

    @RequestMapping(value = "/hellol", method= RequestMethod.GET)
    public String hello(@RequestParam String name) {
        return "Hello " + name;
    }

    @RequestMapping(value = "/hello2", method= RequestMethod.GET)
    public User hello(@RequestHeader String name, @RequestHeader Integer age) {
        return new User(name, age);
    }

    @RequestMapping(value = "/hello3", method = RequestMethod.POST)
    public String hello (@RequestBody User user) {
        return "Hello "+ user. getName () + ", " + user. getAge ();
    }

}
````

- 二、在Client定义服务映射接口

```java
    @FeignClient(value = "hello-service",fallback = FeignFallBack.class)
public interface FeignService {
　　//服务中方法的映射路径
    @RequestMapping("/hello")
    String hello();

    @RequestMapping(value = "/hellol", method= RequestMethod.GET)
    String hello(@RequestParam("name") String name) ;

    @RequestMapping(value = "/hello2", method= RequestMethod.GET)
    User hello(@RequestHeader("name") String name, @RequestHeader("age") Integer age);

    @RequestMapping(value = "/hello3", method= RequestMethod.POST)
    String hello(@RequestBody User user);
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

### fallback 容错处理类

```java
    @Component
public class FeignFallBack implements FeignService{
　　//实现的方法是服务调用的降级方法
    @Override
    public String hello() {
        return "error";
    }

    @Override
    public String hello(String name) {
        return "error";
    }

    @Override
    public User hello(String name, Integer age) {
        return new User();
    }

    @Override
    public String hello(User user) {
        return "error";
    }
}
```
