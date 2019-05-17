# Spring

> *Spring丰富的功能都依赖于两个核心特性：依赖注入（DI）和面向切面（AOP）*

## 应用上下文

>应用上下文:(由org.springframework.context.Applicationcontext接口定义)基于BeanFactory构建，并提供应用框架级别的服务，例如从属性文件解析文本信息以及发布应用事件给感兴趣的事件监听者。

- AnnotationConfigApplicationContext
- AnnotationConfigWebApplicationContext
- ClassPathXmlApplicationContext
- FileSystemXmlApplicationContext
- XmlWebApplicationContext

## 一、装配Bean

>创建应用对象之间协作关系的行为通常称为装配（wiring）

### Bean的三种装配机制

- 在XML中进行显示配置
- 在Java中进行显示配置
- 隐式的Bean发现机制和自动装配

#### 自动装配Bean

两种角度实现：

- 组件扫描：Spring会自动发现应用上下文所创建的Bean
- 自动装配：Spring自动满足bean之间的依赖

#### *1. 组件扫描*

- 1、注解@Component

>使用了@Component注解。这个简单的注解表明该类会作为组件类,并告知Spring要为这个类创建bean。

- 2、注解@ComponentScan

>组件扫描默认是不开启的，使用该注解能够在Spring中启用组件扫描。如果没有其他配置的话，@ComponentScan默认`会扫描与配置类相同的包`。因为CDPlayerConfig类位于soundsystem包中，因此Spring捋会扫描这个`包以及这个包下的所有子包，查找带有Component注解的类`。这样的话，就能发现CompactDisc，并且会在Spring中自动为其创建一个bean。

- 2.1、设置组件扫描的基础包

>在@ComponentScan的value属性中指明包的名称

```java
@Configuration
@ComponentScan(*包名*)
public class CDplayConfig{
    ...
}

//清晰的表明你设置的包的名称
@Configuration
@ComponentScan(basePackages="包名","包名2")
public class CDplayConfig{
    ...
}
```

>除了将包设置为简单的String类型之外，@ComponentScan还提供了另外一种方法，那就是将其指定为包中所包含的类或接口：

```java
@Configuration
@ComponentScan(basePackageClasses="CDPlayer.class","DVDPlayer.class")
public class CDplayConfig{
    ...
}
```

- 3、为组件命名

  - @Component(\*BeanName*)
  - @Named(\*BeanName*)
  
#### *2. 自动装配*

- 注解@Autowired

>自动装配就是让Spring自动满足bean依赖的一种方法。为了声明要进行自动装配，我们可以借助Spring的@Autowired注解

#### 通过Java代码装配bean

>有时候自动化配置的方案行不通，因此需要明确配置Spring。比如说，你想要将`第三方库中的组件装配到你的应用中`，在这种情况下，是没有办法在它的类上添加@Component和@Autowired注解的，因此就不能使用自动化装配的方案了。

- 注解@Bean

>@Bean注解会告诉Spring这个方法捋会返回一个对象，该对象要注册为Spring应用上下文中的bean。方法体中包含了最终产生bean实例的逻辑。

```java
@Configuration
public class CDplayConfig{
    //通过@Bean注解建立与容器的连接
    @Bean
    public CompactDisc sgtPeppers(){
        return new sgtPeppers();
    }

    @Bean
    public CDPlayer cdPlayer(){
        return new CDPlayer(sgtPeppers());
    }

    //在这里，cdPlayer()方法请求一个CompactDisc作为参数。当Spring调用cdPlayer()创建cdPlayerbean的时候，它会自动装配一个CompactDisc到配置方法之中。
    @Bean
    public CDPlayer cdPlayer(CompactDisc compactDisc){
        return new CDPlayer(compactDisc);
    }

}
```

### 高级装配

## 二、面向切面的Spring

>在软件开发中，散布于应用中多处的功能被称为`横切关注点`（cross-cuting concern）。通常来讲，这些横切关注点从概念上`是与应用的业务逻辑相分离的`（但是往往会直接嵌入到应用的业务逻辑之中）。`把这些横切关注点与业务逻辑相分离`正是面向切面编程（AOP）所要解决的问题。

### 定义AOP的术语

- 通知
  >通知定义了切面是什么以及何时使用。除了`描述切面要完成的工作`，通知还解决了`何时执行这个工作的问题`。它应该应用在某个方法被调用之前？之后？之前和之后都调用？还是只在方法抛出异常时调用？

  **切面通知的五种类**

  - **前置通知**（Before）：在目标方法被调用之前调用通知功能：
  - **后置通知**（After）：在目标方法完成之后调用通知，此时不会关心方法的输出是什么；
  - **返回通知**（After-returning）：在目标方法成功执行之后调用通知；
  - **异常通知**（After-throwing）：在目标方法抛出异常后调用通知；
  - **环绕通知**（Around）：通知包裹了被通知的方法，在被通知的方法调用之前和调用之后执行自定义的行为。
- 连接点

>连接点是在应用执行过程中能够`插入切面的一个点`。这个点可以是调用方法时、抛出异常时、甚至修改一个字段时。切面代码可以利用这些点插入到应用的正常流程之中，并添加新的行为。

- 切点

>如果说通知定义了切面的“什么”和“何时”的话，那么切点就定义了“何处”。`切点的定义会匹配通知所要织人的一个或多个连接点`。我们通常使用明确的类和方法名称，或是利用正则表达式定义所匹配的类和方法名称来指定这些切点。

- 切面（通知+切点）

>`切面是通知和切点的结合`。通知和切点共同定义了切面的全部内容—它是什么，在何时和何处完成其功能。

- 引入

>引人允许我们向现有的类添加新方法或属性。

- 织入

>织入是`把切面应用到目标对象并创建新的代理对象的过程`。切面在指定的连接点被织入到目标对象中。在目标对象的生命周期里有多个点可以进行织入：

- 编译期
- 类加载期
- 运行期

#### Spring 对AOP的支持

- 四种类型的AOP支持
  - 基于代理的经典Spring AOP
  - 纯POJO切面
  - @AspectJ注解驱动的切面
  - 注入式AspectJ切面

- AspectJ指示器

|AspectJ指示器|描述|
|---|---|
|arg()|限制连接点匹配参数为指定类型的执行方法|
|@args()|限制连接点匹配参数又制定注解标注的执行方法|
|execution()|用于匹配是连接点的执行方法|
|this()|限制连接点匹配AOP代理的bean引用为指定类型的类|
|target|限制连接点匹配目标对象为指定类型的类|
|@target()|限制连接点匹配特定的执行对象，这些对象对应的类要具有指定类型的注解|
|within|限制连接点匹配指定的类型|
|@within()|限制连接点匹配指定注解所标注的类型（当使用Spring AOP时，方法定义在由指定的注解所标注的类里）|
|@annotation|限定匹配带有指定注解的连接点|

- AspectJ切点表达式

```java
excution(* concert.Performance.perform(..))

    /*
        @parmconcert.Performance  方法所属的类名
        perform() 方法名
        ..     任意参数
    */
```

- 定义切面
  - @AspectJ注解
  >定义一个类为切面

  - AspectJ的五种定义通知的注解：
  
  |注解|通知|
  |--|---|
  |@After|通知方法会在目标方法返回或抛出异常后调用|
  |@AfterReturning|通知方法会在目标方法返回后调用|
  |@AfterThrowing|通知方法会在目标方法抛出异常后调用|
  |@Around|通知方法会得目标方法封装起来|
  |@Before|通知方法会在目标方法调用之前执行|

  - 注解@Pointcut
  >定义可重用的切点

  ```java
  import ...

  @AspectJ
  public class Audience{
      @Pointcut("execution(** concert.Performance.perform(..))")
      public void performance(){}

      @Before("performance()")
      public void silenceCellPhones(){
          System.out.println("Silencing cell phone");
      }

      @AfterReturning("performance()")
      public void applause(){
           System.out.println("CLAP CLAP!!");
      }
  }
  ```

- 注解@DeclareParents 引入新的功能
  >注解由三个部分组成
  - value属性指定了`哪种类型的bean要引入该接口`。在本例中，也就是所有实现Performance的类型。（标记符后面的**加号**表示是`Performance的所有子类型`，而不是Performance本身。
  - defaultImpl属性指定了`为引入功能提供实现的类`。在这里，我们指定的是DefaultEncoreable提供实现。
  - @DeclareParents注解所标注的`静态属性指明了要引入了接口`。在这里，我们所引入的是Encoreable接口。

```java
@Aspect
@Component
public class EncoreableIntroducer {

    @DeclareParents(value = "com.hcpigg.springdemo.Day0517.example.Performance+",defaultImpl = EncoreableImpl.class)
    public static Encoreable encoreable;
}
````