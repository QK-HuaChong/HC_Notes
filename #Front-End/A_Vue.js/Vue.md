# Vue.js

## MVVM 模式

* M：即Model，模型，包括数据和一些基本操作
* V：即View，视图，页面渲染结果
* VM：即View-Model，模型与视图间的双向操作（无需开发人员干涉）

>而MVVM中的VM要做的事情就是把DOM操作完全封装起来，开发人员不用再关心Model和View之间是如何互相影响的：

* 只要我们Model发生了改变，View上自然就会表现出来。
* 当用户修改了View，Model中的数据也会跟着改变。

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

* 文本
    >数据绑定最常见的形式就是使用“Mustache”语法（双大括号）的文本插值：

```html
    <span>Message:{{ msg }}</span>
```

* 插值闪烁
  >使用{{}}方式在网速较慢时会出现问题。在数据未加载完成时，页面会显示出原始的{{}}，加载完毕后才显示正确数据，我们称为插值闪烁。

* v-text
    >将数据输出到元素内部，如果输出的数据有HTML代码，会作为普通文本输出

```html
    <div id="app">
        <span v-text="text"></span>
    </div>

    <script>
        new Vue({
        el: '#app',
        data: {
            text: '你好，中国',
        }
        })
    </script>

* v-html
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

* 属性中的值
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

### 条件语句

* **v-if** And **v-else** And **v-else-if**
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

* 通过key管理可复用的元素
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

### 样式绑定

* 绑定HTML class
    >我们可以传给`v-bind:class`一个对象，以动态地切换 class

```html
    <div id = "computed_props">
        <div v-bind:class="{ active: use }"><sapn>样式绑定</span></div>
        <input type="checkbox" v-model="use" id="cb">
    </div>

    <script>
        var vm = new Vue({
            el: '#example',
            data: {
                user: false,
            }
        })
    </script>
```

* 绑定内联样式
  >`v-bind:style` 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。CSS 属性名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用单引号括起来) 来命名
  
```html

    <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

    data: {
        activeColor: 'red',
        fontSize: 30
    }

    <!--直接绑定到一个样式对象通常更好-->
    <div v-bind:style="styleObject"></div>
    data: {
        styleObject: {
            color: 'red',
            fontSize: '13px'
        }
    }
```

### 事件绑定

>v-on 指令，它用于监听 DOM 事件

```html
    <div id="app">
        <p>The button above has been clicked {{ counter }} times.</p>
        <button v-on:click="counter += 1">+1</button>
        <button v-on:click="counter -= 1">-1</button>
    </div>

    <script>
        var vm = new Vue({
            el : '#app',
            data : {
                counter : 0,
            }
        })
    </script>
```

>`v-on` 还可以接收一个需要调用的方法名称。

```html
    <div id="app">
        <button v-on:click="greet">Greet</button>
    </div>

    <script>
        var vm = new Vue({
            el : '#app',
            data : {
                name:'Jhonaon'
            },
            methods : {
                greet:function(){
                    alert('Hello ' + this.name + ' !')
                }
            }
        })
    </script>
```

* 事件修饰符

|描述|方法|
|---|:---|
阻止单击事件继续传播|\<a v-on:click.stop="doThis"></a>
提交事件不再重载页面|\<form v-on:submit.prevent="onSubmit"></form>
修饰符可以串联|\<a v-on:click.stop.prevent="doThat"></a>
只有修饰符|\<form v-on:submit.prevent></form>
添加事件监听器时使用事件捕获模式、即元素自身触发的事件先在此处理，然后才交由内部元素进行处理|\<div v-on:click.capture="doThis">...</div>
只当在 event.target 是当前元素自身时触发处理函数、即事件不是从内部元素触发的|\<div v-on:click.self="doThat">...</div>
点击事件将只会触发一次|\<a v-on:click.once="doThis"></a>

### **双向数据绑定**

  >`v-model`指令用来在 input、select、text、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。

```html
    <div id="app">
        <h3 v-text="title"></h3>
        <input v-model="title" />
    </div>
    <script>
        var vm = new Vue({
            el : '#app',
            data : {
            title : '一带一路',
            }
        })
    </script>
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

### 过滤器

>Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化

```html
    <div id="app">
        {{ message | capitalize }}
    </div>
    <script>
        new Vue({
        el: '#app',
        data: {
            message: 'runoob'
        },
        filters: {
            capitalize: function (value) {
            if (!value) return ''
            value = value.toString()
            return value.charAt(0).toUpperCase() + value.slice(1)
            }
        }
        })
    </script>
```

## 五、组件

### 全局注册

>Vue.component

```js
    Vue.component('my-component-name', {
     // ... 选项 ...
})
```

### 局部注册

```js
    new Vue({
        el: '#app',
        components: {
            'component-a': ComponentA,
            'component-b': ComponentB
        }
    })
```

### data 必须是有一个函数

>一个组件的 data 选项必须是一个函数，因此每个实例可以维护一份被返回对象的独立的拷贝

```js
    data: function () {
        return {
            ...
        }
}
```

### props 向组件传递数据

>Prop 是你可以在组件上注册的一些自定义特性。当一个值传递给一个 prop 特性的时候，它就变成了那个组件实例的一个属性

```js
    Vue.component('blog-post', {
        props: ['title'],
        //以对象形式列出 prop
        props:{
            //名称：类型
            'title':String,
        },
        template: '<h3>{{ title }}</h3>'
    })
```

### 自定义事件

>子组件要把数据传递回去，就需要使用自定义事件

* 使用 $on(eventName) 监听事件
* 使用 $emit(eventName) 触发事件

```html
    <div id="app">
        <div :style="{ fontSize: postFontSize + 'em' }">
            <pigg-text v-for="post in posts"
                v-bind:key="post.id"v-bind:post="post"
                v-on:enlarge-text="postFontSize += 0.1"
                v-on:ensmall-text="postFontSize -= 0.1">
            </pigg-text>
        </div>
    </div>

    <script>
        var vm = new Vue({
            el:'#app',
            data:{
                posts: [
                    { id: 1, title: 'My journey with Vue' },
                    { id: 2, title: 'Blogging with Vue' },
                    { id: 3, title: 'Why Vue is so fun' }
                ],
                postFontSize: 1
            },
            components:{
                'pigg-text':{
                    props:['post'],
                    template:`<div><h3>{{post.title}}</h3><button v-on:click="$emit('enlarge-text')">Enlarge text</button><button v-on:click="$emit('ensmall-text')">Ensmall text</button></div>`
                }
            }
        })
    </script>
```

## 六、插槽

### 单个插槽

>除非子组件模板包含至少一个 ```<slot>``` 插口，否则父组件的内容将会被丢弃。当子组件模板只有一个没有属性的插槽时，父组件传入的整个内容片段将插入到插槽所在的 DOM 位置，并替换掉插槽标签本身。

```html
    <div id="app">
        <slot-span>你好</slot-span>
    </div>

    <script>
    var vm = new Vue({
        el:'#app',
        components:{
            'slot-span':{
                template:`<span><slot></slot></span>`
            }
        }
    })
    </script>
```

### 具名插槽

>``<slot>`` 元素可以用一个特殊的特性 name 来进一步配置如何分发内容。多个插槽可以有不同的名字。具名插槽将匹配内容片段中有对应 slot 特性的元素。仍然可以有一个匿名插槽，它是默认插槽，作为找不到匹配的内容片段的备用插槽。如果没有默认插槽，这些找不到匹配的内容片段将被抛弃。

```html
    <app-layout>
        <template v-slot:header><h2>Title on header</h2></template>
        <template v-slot:default><p>Context</p></template>
        <template v-slot:footer><a href="www.baidu.com">百度链接</a></template>
    </app-layout>

    <script>
    var vm = new Vue({
        el:'#app',
        components:{
            'app-layout':{
                template:`<div class="container">
                    <header><slot name="header"></slot></header>
                    <main><slot></slot></main>
                    <footer><slot name="footer"></slot></footer>
                </div>`
            }
        }
    })
    </script>

```

### 作用域插槽

>1、使用作用域插槽将子组件中的数据传递出去
>2、使用场景： 子组件做循环显示，或者子组件的某一部分由外部指定的时候，就使用作用域插槽。

```html
    <div id='app'>
        <xi-list :lists='xiyouji' odd-bgcolor="#D3DCE6" even-bgcolor="#E5E9F2" listStyle=none>
            <template v-slot:default='show'>{{show.list.name}}</template>
        </xi-list>
        <xi-list :lists='hongloumeng' odd-bgcolor="#D3DCE6" even-bgcolor="#E5E9F2" listStyle=none>
            <template v-slot:default='show'>{{show.list.name}}</template>
        </xi-list>
    </div>

    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                xiyouji:[
                    {id:1,name:'孙悟空'},
                    {id:2,name:'猪八戒'},
                    {id:3,name:'沙和尚'},
                    {id:4,name:'唐僧'},
                    {id:5,name:'小白龙'},
                ],
                hongloumeng:[
                    {id:1,name:'林黛玉'},
                    {id:2,name:'薛宝钗'},
                    {id:3,name:'贾宝玉'},
                    {id:4,name:'史湘云'},
                    {id:5,name:'贾元春'},
                ],
            },
            components:{
                'xi-list':{
                    props:{
                        lists:Array,
                        oddBgcolor: String,
                        evenBgcolor: String,
                    },
                    template:`<div>
                                    <ul>
                                        <li v-bind:style="styleli" v-for="(list,index) in lists" style="line-height:2.2;list-style-type:none;" :style="index % 2 === 0 ? 'background:'+oddBgcolor : 'background:'+evenBgcolor">
                                            <slot v-bind:list="list"></slot>
                                        </li>
                                    </ul>
                                </div>`,
                }
            }
        })
    </script>
```

## 自定义指令

>代码复用和抽象的主要形式是组件。然而，有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令

## vue-cli

在开发中，需要打包的东西不止是js、css、html。还有更多的东西要处理，这些插件和加载器如果我们一一去添加就会比较麻烦。

幸好，vue官方提供了一个快速搭建vue项目的脚手架：vue-cli

安装命令：

```cmd
    npm install -g vue-cli
```

### 单文件组件

每一个.vue文件，就是一个独立的vue组件。

而单文件组件中包含三部分内容：

* template：模板，支持html语法高亮和提示
* script：js脚本，这里编写的就是vue的组件对象，看到上面的data(){}了吧
* style：样式，支持CSS语法高亮和提示
