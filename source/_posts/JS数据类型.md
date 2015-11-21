title: JS数据类型
date: 2015-03-06 15:05:13
tags:
- JavaScript
- 数据类型
categories:
- JavaScript
---
###JS数据类型
JS是弱类型语言,定义变量时候无需指定类型.
var num = 32;

完后也可以把字符串 赋值给这个变量
```{bash}
num = "this is a string";

32 + 32  // 64
“32” + 32  // "3232"
“32” - 32  // 0
```
JS因为不需要指定类型 ,在一些运算的时候有很多隐式转换

#####先看一下JS数据类型

5种原始类型和一种对象类型
原始类型 (number string boolean null undefined) object 对象(function array date ...)

根据不同类型,有一些不同隐式转换方式
对于 a == b
如果类型相同就相当于 === 严格等于
如果类型不同会尝试类型转换
null == undefined 相等

number == string （会尝试把字符串转换成数字  ） //  1 == "1.0" true

boolean == ? (一边是布尔值 不管另一边是什么 首先会把布尔值转换成数字 true转换为1 false 转换为 0)

object == number | string (如果一边是对象另一边是Number 或者string  会尝试把对象转换为基本类型 其他的情况的话就会是false)

在原始类型中 Number string boolean 都有包装对象
比如 

  var str ="string" 这是一个基本类型 在JS 中当你尝试给这样的类型增加属性时  js会将他转换为包装对象
 相当于 new 一个 string   但是 当使用完以后 会被销毁 因为这是一个临时对象


#####类型 检测
 
     typeof  运算符会返回一个字符串  适合函数对象和基本类型
```{bash}
     typeof 100   // number
     typeof true  // boollean
     typeof function //function
     typeof (undefined)  // undefined
     typeof new Object() // object
     typeof [1,2]     //object
     typeof NAN     // number
     typeof null     //object   
```
   instanceof  对于判读对象类型 常用的是  instanceof 
          obj instanceof object
           会判断 左边的对象 的原型链上是否有 右边的构造函数的 prototype 属性（任何构造函数都会有一个prototype对象属性 这个对象属性将用作 使用new 构造函数 这种构造方式来构造出对象的原形 ）
JS是用引用来判断对象的  在跨iframe 的对象上不能用instanceof

Object.prototype.toString 也可以判断一些类型 
比如  Object.prototype.toString.apply([]); === "[object Array]"

constructor  会指向构造这个对象的 构造函数 (constructor可以被改写)

typeof  适合基本类型以及Function  遇到null 失效 会返回object 可以用 === 来判断是否等于 null



