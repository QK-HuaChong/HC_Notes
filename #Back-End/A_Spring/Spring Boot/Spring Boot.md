# Spring Boot

## 1.Spring Boot 项目的搭建：

### 1.1.注入Starter依赖：在pom.xml文件中注入以下以来：

```xml
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <!--spring boot web 开发 -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```

### 1.2.启动类：

>注解说明:
@SpringBootApplication：
> 发现@SpringBootApplication是一个复合注解，包括@ComponentScan，和@SpringBootConfiguration，@EnableAutoConfiguration.
>
> @SpringBootConfiguration继承自@Configuration，二者功能也一致，标注当前类是配置类，并会将当前类内声明的一个或多个以@Bean注解标记的方法的实例纳入到srping容器中，并且实例名就是方法名。
>
> @EnableAutoConfiguration的作用启动自动的配置，@EnableAutoConfiguration注解的意思就是Springboot根据你添加的jar包来配置你项目的默认配置，比如根据spring-boot-starter-web ，来判断你的项目是否需要添加了webmvc和tomcat，就会自动的帮你配置web项目中所需要的默认配置。在下面博客会具体分析这个注解，快速入门的demo实际没有用到该注解。
>
> @ComponentScan，扫描当前包及其子包下被@Component，@Controller，@Service，@Repository注解标记的类并纳入到spring容器中进行管理。是以前的<context:component-scan>（以前使用在xml中使用的标签，用来扫描包配置的平行支持）。所以本demo中的User为何会被spring容器管理。

## 2.Spring Boot + Redis 缓存处理：

### 2.1.Redis介绍：

Redis是一款开源的、高性能的键-值存储（key-value store）。它常被称作是一款数据结构服务器（data structure server）。

### 2.2.依赖注入：

```xml
    <dependency>  
        <groupId>org.springframework.boot</groupId>  
        <artifactId>spring-boot-starter-redis</artifactId>
    </dependency>
```

### 2.3.添加配置信息：

```txt
# REDIS (RedisProperties)
# Redis数据库索引（默认为0）
spring.redis.database=0  
# Redis服务器地址
spring.redis.host=192.168.0.58
# Redis服务器连接端口
spring.redis.port=6379  
# Redis服务器连接密码（默认为空）
spring.redis.password=  
# 连接池最大连接数（使用负值表示没有限制）
spring.redis.pool.max-active=8  
# 连接池最大阻塞等待时间（使用负值表示没有限制）
spring.redis.pool.max-wait=-1  
# 连接池中的最大空闲连接
spring.redis.pool.max-idle=8  
# 连接池中的最小空闲连接
spring.redis.pool.min-idle=0  
# 连接超时时间（毫秒）
spring.redis.timeout=0  
```

## 3. thymeleaf模板引擎：

### 3.1.表达式语法：

|表达式：|1.变量表达式|2.选择或星号表达式|3.消息表达4.URL表达式|
|-|-|-|-|


* 1.变量表达式:
  变量表达式即OGNL表达式或Spring EL表达式(在Spring术语中也叫model attributes)。如下所示：

  ```java
    ${session.user.name}
  ```

* 2.选择或星号表达式
  选择表达式很像变量表达式，不过它们用一个预先选择的对象来代替上下文变量容器(map)来执行，如下：

  ```java
    *{customer.name}
  ```

* 3.URL表达式:
  允许我们从一个外部文件获取区域文字信息(.properties)，用Key索引Value，还可以提供一组参数(可选).

  ```java
    #{main.title}  
    #{message.entrycreated(${entryId})}
  ```

* 4.URL表达式:
  URL表达式指的是把一个有用的上下文或回话信息添加到URL，这个过程经常被叫做URL重写。

  ```html
    <form th:action="@{/createOrder}">  
    <a href="main.html" th:href="@{/main}">
  ```

#### 3.1.1常用th标签：

  <table border="2">
  <tbody>
    <tr>
      <td>th:id</td>
      <td>替换id</td>
      <td><code>    &lt;input th:id="'xxx' + ${collect.id}"/&gt; </code></td>
    </tr>
    <tr>
      <td style="color:red">th:text</td>
      <td>文本替换</td>
      <td><code  >&lt;p  th:text="${collect.description}"&gt;description&lt;/p&gt;</code></td>
    </tr>
    <tr>
      <td>th:utext</td>
      <td>支持html的文本替换</td>
      <td><code  >&lt;p  th:utext="${htmlcontent}"&gt;conten&lt;/p&gt;</code></td>
    </tr>
    <tr>
      <td>th:object</td>
      <td>替换对象</td>
      <td><code  >&lt;div th:object="${session.user}"&gt; </code></td>
    </tr>
    <tr>
      <td>th:value</td>
      <td>属性赋值</td>
      <td><code  >&lt;input th:value="${user.name}" /&gt; </code></td>
    </tr>
    <tr>
      <td>th:with</td>
      <td>变量赋值运算</td>
      <td><code  >&lt;div th:with="isEven=${prodStat.count}%2==0"&gt;&lt;/div&gt; </code></td>
    </tr>
    <tr>
      <td>th:style</td>
      <td>设置样式</td>
      <td><code  >th:style="'display:' + @{(${sitrue} ? 'none' : 'inline-block')} + ''" </code></td>
    </tr>
    <tr>
      <td>th:onclick</td>
      <td>点击事件</td>
      <td><code  >th:onclick="'getCollect()'" </code></td>
    </tr>
    <tr>
      <td style="color:red">th:each</td>
      <td>属性赋值</td>
      <td><code  >tr th:each="user,userStat:${users}"&gt; </code></td>
    </tr>
    <tr>
      <td style="color:red">th:if</td>
      <td>判断条件</td>
      <td><code  > &lt;a th:if="${userId == collect.userId}" &gt; </code></td>
    </tr>
    <tr>
      <td>th:unless</td>
      <td>和th:if判断相反</td>
      <td><code  >&lt;a th:href="@{/login}" th:unless=${session.user != null}&gt;Login&lt;/a&gt; </code></td>
    </tr>
    <tr>
      <td>th:href</td>
      <td>链接地址</td>
      <td><code  >&lt;a th:href="@{/login}" th:unless=${session.user != null}&gt;Login&lt;/a&gt; /&gt; </code></td>
    </tr>
    <tr>
      <td>th:switch</td>
      <td>多路选择 配合th:case 使用</td>
      <td><code  >&lt;div th:switch="${user.role}"&gt; </code></td>
    </tr>
    <tr>
      <td>th:case</td>
      <td>th:switch的一个分支</td>
      <td><code  > &lt;p th:case="'admin'"&gt;User is an administrator&lt;/p&gt;</code></td>
    </tr>
    <tr>
      <td>th:fragment</td>
      <td>布局标签，定义一个代码片段，方便其它地方引用</td>
      <td><code  >&lt;div th:fragment="alert"&gt;</code></td>
    </tr>
    <tr>
      <td>th:include</td>
      <td>布局标签，替换内容到引入的文件</td>
      <td><code  >&lt;head th:include="layout :: htmlhead" th:with="title='xx'"&gt;&lt;/head&gt; /&gt; </code></td>
    </tr>
    <tr>
      <td>th:replace</td>
      <td>布局标签，替换整个标签到引入的文件</td>
      <td><code  >&lt;div th:replace="fragments/header :: title"&gt;&lt;/div&gt; </code></td>
    </tr>
    <tr>
      <td>th:selected</td>
      <td>selected选择框 选中</td>
      <td><code  >th:selected="(${xxx.id} == ${configObj.dd})"</code></td>
    </tr>
    <tr>
      <td>th:src</td>
      <td>图片类地址引入</td>
      <td><code  >&lt;img class="img-responsive" alt="App Logo" th:src="@{/img/logo.png}"  /&gt; </code></td>
    </tr>
    <tr>
      <td>th:inline</td>
      <td>定义js脚本可以使用变量</td>
      <td><code  >&lt;script type="text/javascript" th:inline="javascript"&gt;</code></td>
    </tr>
    <tr>
      <td>th:action</td>
      <td>表单提交的地址</td>
      <td><code  >&lt;form action="subscribe.html" th:action="@{/subscribe}"&gt;</code></td>
    </tr>
    <tr>
      <td>th:remove</td>
      <td>删除某个属性</td>
      <td><code  >&lt;tr th:remove="all"&gt;   1.all:删除包含标签和所有的孩子。2.body:不包含标记删除,但删除其所有的孩子。3.tag:包含标记的删除,但不删除它的孩子。4.all-but-first:删除所有包含标签的孩子,除了第一个。5.none:什么也不做。这个值是有用的动态评估。</code></td>
    </tr>
    <tr>
      <td>th:attr</td>
      <td>设置标签属性，多个属性可以用逗号分隔</td>
      <td>比如 <code  >th:attr="src=@{/image/aa.jpg},title=#{logo}"</code>，此标签不太优雅，一般用的比较少。</td>
    </tr>
  </tbody>
  </table>

## 4.Spring Boot + JPA

### 4.1.注入依赖

```xml
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-jpa</artifactId>
      <version>2.1.2.RELEASE</version>
    </dependency>
```

> ## MySQL 驱动名称改动：

 ```properties
spring.datasource.driver-class-name=com.mysql.jdbc.Driver变更为:
 spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

```

### 4.2.创建JPA：

创建JPA接口并且继承SpringDataJPA内的接口作为父类

```java
  // JpaRepository接口（SpringDataJPA提供的简单数据操作接口）
  // JpaSpecificationExecutor（SpringDataJPA提供的复杂查询接口）
  public interface UserRepository extends
        JpaRepository<UserEntity,Long>,
        JpaSpecificationExecutor<UserEntity>,
        Serializable {
}
```

### 4.3.将JPA注入到需要使用的类中：

```java
    @Autowired
    UserRepository userRepository;

     @Override
    public List<UserEntity> getUserList() {
        List<UserEntity> userList= new ArrayList<UserEntity>();
        userList=userRepository.findAll();
        return  userList;
    }
```

### 4.4.@Query注解自定义SQL

```java
  @Query(value = "select id,username from fd_boy where username = ?",nativeQuery = true)
    public UserEntity getUserEntiteByName(String names);
```

## 4.热部署

### Spring Boot 配置热部署

* 注入依赖

```xml
  <!-- 热部署 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>
```

* 添加配置信息

```yml
  spring:
  devtools:
    restart:
      enabled: true
  freemarker:
    cache: true
```

## 5. 集成Swagger：

* 导入相关jar

```xml
    <!--Swagger UI-->
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <version>2.8.0</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
            <version>2.8.0</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-bean-validators</artifactId>
            <version>2.8.0</version>
        </dependency>
```

* 添加配置类：与启动类同级

```java

import ...

@Configuration
@EnableSwagger2
public class Swagger2 {
//swagger2的配置文件，这里可以配置swagger2的一些基本的内容，比如扫描的包等等
    @Bean
    public Docket createRestApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .select()
                //为当前包路径
                .apis(RequestHandlerSelectors.basePackage("com.springboot.example.Controller"))
                .paths(PathSelectors.any())
                .build();
    }
    //构建 api文档的详细信息函数,注意这里的注解引用的是哪个
    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                //页面标题
                .title("Spring Boot 测试使用 Swagger2 构建RESTful API")
                //创建人
                .contact(new Contact("MarryFeng", "http://www.baidu.com", ""))
                //版本号
                .version("1.0")
                //描述
                .description("API 描述")
                .build();
    }
}
```

* Swagger注解

>swagger通过注解表明该接口会生成文档，包括接口名、请求方法、参数、返回的信息等等。

|名称|描述
--|:--
@Api：|修饰整个类，描述Controller的作用
@ApiOperation：|描述一个类的一个方法，或者说一个接口
@ApiParam：|单个参数描述
@ApiModel：|用对象来接收参数
@ApiProperty：|用对象接收参数时，描述对象的一个字段
@ApiResponse：|HTTP响应其中1个描述
@ApiResponses：|HTTP响应整体描述
@ApiIgnore：|使用该注解忽略这个API
@ApiError ：|发生错误返回的信息
@ApiImplicitParam：|一个请求参数
@ApiImplicitParams：|多个请求参数

## Lombok的使用

### 如何使用

* IDEA需要安装Lombok插件
  * 打开IDEA的Setting –> 选择Plugins选项 –> 选择Browse repositories –> 搜索lombok –> 点击安装 –> 安装完成重启IDEA –> 安装成功

* 导入相关jar

```xml
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.18</version>
    <scope>provided</scope>
</dependency>
```

### 相关注解介绍

|注解名|作用|
-|-|
@Getter|作用在类上或成员变量上，生成对应的 getter 方法
@Setter|作用在类上或成员变量上，生成对应的 setter 方法
@NoArgsConstructor|作用在类上，生成对应的无参构造方法
@AllArgsConstructor|作用在类上，生成对应的有参构造方法
@ToString|作用在类上，生成对应的 toString 方法
@EqualsAndHashCode|作用在类上，生成对应的 equals 和 hashCode 方法
@Data|作用在类上，效果等同于上述 5 个注解，排除 @AllArgsConstructor 功能
@Log4j/@Slf4j|作用在类上，生成对应的 Logger 对象，变量名为 log