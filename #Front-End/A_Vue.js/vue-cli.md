# vue-cli

## vue-cli介绍

在开发中，需要打包的东西不止是js、css、html。还有更多的东西要处理，这些插件和加载器如果我们一一去添加就会比较麻烦。

幸好，vue官方提供了一个快速搭建vue项目的脚手架：vue-cli

安装命令：

```shell
    npm install -g vue-cli
```

## 搭建webpack项目

```shell
    vue init webpack
```

## 单文件组件

每一个.vue文件，就是一个独立的vue组件。

而单文件组件中包含三部分内容：

* template：模板，支持html语法高亮和提示
* script：js脚本，这里编写的就是vue的组件对象，看到上面的data(){}了吧
* style：样式，支持CSS语法高亮和提示

每个组件都有自己独立的html、JS、CSS，互不干扰，真正做到可独立复用。
