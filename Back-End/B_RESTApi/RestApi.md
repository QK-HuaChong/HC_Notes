# RestApi

## REST介绍：

### &nbsp; REST（Representational State Transfer）含状态传输是一种软件架构风格

### **RESTFul = 有意义的 URL + 合适的 HTTP 动词**

## Rest体现在API设计主要有以下几点：

> * 通过URL来指定资源
> * 通过资源的表现形式来操作资源
> * 对资源的操作包括`获取`、`创建`、`修改`、`删除`，对应的HTTP协议提供GET、POST、PUT、DELETE方法。  

|方法|操作|
|---|:---|
|GET|获取资源|
|POST|插入资源或者更新现有的资源|
|DELETE|删除资源|
|PUT|插入资源或者更新现有的资源|
|OPTIONS|列举允许对资源进行的操作|
|HEAD|返回Response Header|

## 注意事项：

>URL不能包含动词

```txt
POST /en/zh/show

```

>URL中的名词表示资源集合，使用复数形式

```txt
GET http://www.wxample.com/projects
```

## 使用案例：

> * GET /users：获取所有的成员
> * POST /user：添加一个成员
> * GET /uses/ID：得到user_id为ID的成员信息
> * PUT /users/ID：更新user_id为ID的成员信息
> * DELETE /users/ID：删除user_id为ID的成员
> * GET /users/developer：得到所有的开发成员

## Spring Boot + RestApi

```java
@RestController
@RequestMapping("/user")
public class UserControllerAPI {

   private final UserService userService;

   @Autowired
   public UserControllerAPI(UserService userService) {
       this.userService = userService;
   }

   @RequestMapping(value = "/api", method = RequestMethod.GET)
   public PageResultBean<List<User>> getUserAll(PageResultBean page) {
       return new PageResultBean<>(userService.getUserAll(page.getPageNo(), page.getPageSize()));
   }

   @RequestMapping(value = "/api/{id}", method = ARequestMethod.GET)
   public ResultBean<User> getUserByPrimaryKey(@PathVariable("id") Integer id) {
       return new ResultBean<>(userService.selectByPrimaryKey(id));
   }

   @RequestMapping(value = "/api/{id}", method = RequestMethod.PUT)
   public ResultBean<Integer> updateUserByPrimaryKey(@PathVariable("id") Integer id,User user) {
       user.setId(id);
       return new ResultBean<>(userService.updateByPrimaryKeySelective(user));
   }

   @RequestMapping(value = "/api/{id}", method = RequestMethod.DELETE)
   public ResultBean<String> deleteUserByPrimaryKey(@PathVariable("id") Integer id) {
       return new ResultBean<>(userService.deleteByPrimaryKey(id));
   }

   @RequestMapping(value = "/api", method = RequestMethod.POST)
   public ResultBean<Integer> createUser(User user) {
       return new ResultBean<>(userService.insertSelective(user));
   }
}
```