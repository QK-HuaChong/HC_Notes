# Vue.js

## 一、Vue实例

### 创建一个Vue实例

```js

    var vm = new Vue({
        //选项
    })
```

### 数据与方法

```js
    var data = {a:1}

    var vm = new Vue({
        data:data
    })
```

## 二、模板语言

### 插值

- 文本
    >数据绑定最常见的形式就是使用“Mustache”语法（双大括号）的文本插值：

```html
    <span>Message:{{ msg }}</span>
```

- Html
    >使用v-html 指令用于输出html代码：

```html
    <div id="app">
        <div v-html="msg"></div>
    </div>

    <script>
new Vue({
  el: '#app',
  data: {
    message: '<span style="color:red">This should be red</span>'
  }
})
</script>
```

- 属性中的值
    >HTML 属性中的值应使用v-bind指令。

```html
    <button v-bind:disabled="isButtonDisabled">Button</button>

    <script>
        var app = new Vue({
            el:'#app,
            data:{isButtonDisabled:true,}
        })
    </script>
```

## 三、指令

>指令（Directives）是带有v-前缀的特殊特性。指令特性的值预期是单个JavaScript表达式（v-for是例外情况，稍后我们再讨论）。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于DOM。

- 条件语句
  - **v-if** And **v-else** And **v-else-if**
    >v-if 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染。也可以用 v-else 添加一个“else 块”

```html
    <h3 v-if="today == 'Sunday'">周日</h3>
    <h3 v-else-if="today=='Monday'">周一</h3>
    <h3 v-else-if="today=='Tuesday'">周二</h3>

    <script>
        var app = new Vue({
            el:'#app,
            data:{
                today:'Sunday',
            }
        })
    </script>
```

- 通过key管理可复用的元素
    >所以Vue为你提供了一种方式来表达“这两个元素是完全独立的，不要复用它们”。只需添加一个具有唯一值的key属性即可

```html
    <template v-if="loginType === 'username'">
        <label>Username</label>
        <input placeholder="Enter your username" key="username-input">
    </template>

    <template v-else>
        <label>Email</label>
        <input placeholder="Enter your email address" key="email-input">
    </template>

    <script>
        var app = new Vue({
            el:'#app,
            data:{
                loginType:'username',
            }
        })
    </script>
```

- 双向数据绑定
  >v-model 指令用来在 input、select、text、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。

```html
    <div id="app">
        <h3>{{ title }}</h3>
        <input v-model="title" />
    </div>
```

## 四、计算属性

### computed 指令

> 处理一些复杂逻辑使用

```html
    <div id="example">
        <p>Original message: "{{ message }}"</p>
        <p>Computed reversed message: "{{ reversedMessage }}"</p>
    </div>

    <script>
        var vm = new Vue({
            el: '#example',
            data: {
                message: 'Hello'
            },
            computed: {
                // 计算属性的 getter
                reversedMessage: function () {
                // `this` 指向 vm 实例
                return this.message.split('').reverse().join('')
                }
            }
        })
    </script>
```

### computed 与 methods的比较

>可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的依赖缓存，只有`相关依赖发生改变时才会重新取值`。而使用 methods ，在重新渲染的时候，函数`总会重新调用执行`。

### 侦听器

```html
    <div id = "computed_props">
         千米 : <input type = "text" v-model = "kilometers">
         米 : <input type = "text" v-model = "meters">
    </div>
    <script>
        var vm = new Vue({
            el: '#computed_props',
            data:{
                kilometers : 0,
                meters:0
                },
            watch:{
                kilometers:function(val){
                    this.kilometers = val;
                    this.meters = this.kilometers * 1000;
                },
                meters : function (val) {
                    this.kilometers = val/ 1000;
                    this.meters = val;
                }
            }
        });
    </script>
```

### 样式绑定

- 绑定HTML class
    >我们可以传给 v-bind:class 一个对象，以动态地切换 class：