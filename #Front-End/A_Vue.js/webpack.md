# webpack

## 简介

>Webpack 是一个前端资源的打包工具，它可以将js、image、css等资源当成一个模块进行打包。

## 学习Webpack，你需要先理解四个核心概念

### 入口(entry)

>webpack打包的启点，可以有一个或多个，一般是js文件。webpack会从启点文件开始，寻找启点直接或间接依赖的其它所有的依赖，包括JS、CSS、图片资源等，作为将来打包的原始数据

### 输出(output)

>出口一般包含两个属性：path和filename。用来告诉webpack打包的目标文件夹，以及文件的名称。目的地也可以有多个。

### 加载器（loader）

>webpack本身只识别Js文件，如果要加载非JS文件，必须指定一些额外的加载器（loader），例如css-loader。然后将这些文件转为webpack能处理的有效模块，最后利用webpack的打包能力去处理。

### 插件(plugins)

>插件可以扩展webpack的功能，让webpack不仅仅是完成打包，甚至各种更复杂的功能，或者是对打包功能进行优化、压缩，提高效率。

## 模块引用与注册

* 引用：import Vue from '../node_modules/vue/dist/vue';

* 要使用import，就需要在js文件中添加export导出语句：export default loginForm;

## webpack 配置

### 配置入口

```js
    module.exports={
    entry:'./src/main.js',  //指定打包的入口文件
}
```

### 配置出口

```js
    module.exports={
    entry:'./src/main.js',  //指定打包的入口文件
    output:{
        // path: 输出的目录，__dirname是相对于webpack.config.js配置文件的绝对路径
        path : __dirname+'/dist',  
        filename:'build.js'//输出的js文件名
    }
}
```

### 执行打包

```shell
    npx webpack --config webpack.config.js
```
