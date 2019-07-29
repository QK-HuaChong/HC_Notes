# ECMAScript 6

## ECMAScript 简介

>ECMAScript 和 JavaScript 的关系是，前者是后者的规格，后者是前者的一种实现（另外的 ECMAScript 方言还有 JScript 和 ActionScript）。日常场合，这两个词是可以互换的。

## 1. let 和 const 命令

let所声明的变量，只在let命令所在的代码块内有效。

```js
    for(let i = 0; i < 5; i++){
        console.log(i);
    }
    console.log("循环外：" + i)
```

const声明的变量是常量，不能被修改

## 2. 字符串扩展

ES6为字符串扩展了几个新的API：

includes()：返回布尔值，表示是否找到了参数字符串。
startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。
