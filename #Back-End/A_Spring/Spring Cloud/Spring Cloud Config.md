# Spring Cloud Config 配置统一管理

## 简介

>Spring Cloud Config分为Config Server和Config Client两部分，为分布式系统外部化配置提供了支持。 Spring Cloud Config非常适合Spring应用程序，也能与其他编程语言编写的应用组合使用。
>
>微服务在启动时，通过Config Client请求Config Server以获取配置内容，同时会缓存这些内容。

## Config Server

### 一、添加依赖

```xml
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-config-server</artifactId>
    </dependency>
```

### 二、添加注解

>在启动类上添加 *@EnableConfigServer* 注解

```java
    @SpringBootApplication
    @EnableConfigServer
    public class LsgConfigApplication {
        public static void main(String[] args) {
            SpringApplication.run(LsgConfigApplication.class, args);
        }
    }
```

### 三、编辑配置文件

- uri: Git仓库的路径
- username：用户名
- password：用户密码

```yml
    spring:
        application:
            name: config-server
        cloud:
            config:
            server:
                git:
                uri: https://github.com/QK-HuaChong/HC_Notes
                username: QK-HuaChong
                password: ********
```

### 四、Config Server端点

映射规则

- /{application}/{profile}/[{label}]
- /{label}/{application}-{profile}.properties
- /{application}-{profile}.properties
- /{label}/{application}-{profile}.yml
- /{application}-{profile}.yml
  
---

- {application}通常使用微服务名称，对应Git仓库中文件名的前缀；
- {profile}对应{application}-后面的dev、pro、test等；
- {label}对应Git仓库的分支名，默认为master。

## Config Client

### 一、添加相关依赖

```xml
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-config-client</artifactId>
    </dependency>
```

### 二、编辑配置文件

>Spring Cloud有一个“引导上下文”的概念，这是主应用程序的父上下文。引导上下文负责从配置服务器加载配置属性，以及解密外部配置文件中的属性。和主应用程序加载application.\*（yml或properties）中的属性不同，引导上下文加载bootstrap.*
>中的属性。配置在bootstrap.*中的属性有更高的优先级，因此默认情况下它们不能被本地配置覆盖。

- name: 对应Config Server中的application
- uri: Config Server 的地址
- profile: 对应Config所获取的配置文件的profile
- lable: 对应Git仓库的分支名

```yml
spring:
  application:
    name: config
  cloud:
    config:
      uri: http://localhost:8788/
      profile: test
      label: master
```

### 编写Controller

```java
@RestController
public class LsgConfigClientContorller {

    private static final Logger LOGGER = LoggerFactory.getLogger(LsgConfigClientContorller.class);

    @Value("${profile}")
    private String profile;

    @RequestMapping("/profile")
    public String show(){
        LOGGER.info("Get Config Info Successfully");
        return this.profile;
    }
}
```
