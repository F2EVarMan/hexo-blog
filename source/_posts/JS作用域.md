title: JS作用域
date: 2015-03-26 16:22:16
tags:
- JavaScript
- 作用域
categories:
- JavaScript
---
###JavaScript 作用域
js中最常见的是全局作用域
这里我们在最外层生成的变量a,这就是全局变量a，
在这个全局范围内我们的for循环里面有var item 定义了一个变量item，
我们可能会以为他是在for循环里面可见对外不可见，实际上这是错误的理解。
在javascript里是没有块级作用域的，不管是for循环还是while里面定义的变量实际上跟for循环外面定义的变量是没有差别的.
函数作用域
比如这里我们的一个匿名立即执行的函数表达式,我们在执行的时候会生成一个局部变量b，但是在函数外面我们是拿不到这个变量的，这说明函数有自己独立的作用域
除了全局作用域和函数作用域以后,还有一个eval作用域,这种作用域比较特殊，在JavaScript中是没有函数作用域的.
```{bash}
var a=10;
(function(){
  var b=20;
})();
console.log(a); // 10
console.log(b); // b in not defined

for(var item in {a:1,b:2}){
  console.log(item)
}
console.log(item); //item still scope

eval("var a=1;")
```
作用域链
作用域的访问本后也有一个作用域链的机制,
```{bash}
  function outer2(){
    var local2=1;
    function outer1(){
      var local=1;
      // 可以访问到local1,local2 或者global3
    }
    outer1();
  }
  var global3=1;
  outer2();
  function outer(){
    var i=1;
    var func=new Function("console.log(typeof i)")
    func(); //undefined
    outer();
  }
```
这里我们定义了一个局部变量local1，在local1下面可以访问到local1，也可以向上访问到Local2，也就是所谓的闭包，
我们可以访问到函数外层的局部变量，还可以向上访问到全局变量global3
如果使用new function  构造器 字符串的形式调用函数的时候实际上是访问不到构造器定义位置所在的变量I
```{bash}
(function(){
  //do sth
  var a,b;
})()

!function(){
  //do sth
  var a,b;
}()
```
利用函数作用域的特性,我们经常看到很多类库或者代码，最外层如果没有一些模块化的工具的话很有可能会这样一个匿名函数。
这样可以把函数里面的变量变成函数的局部变量而不是全局变量，这样防止大量的全局变量和其他类库引发冲突，除了开头用括号括起来，也会有一些开头是!或者+号，这样都是可以的，他的作用就是把函数变成函数表达式，而不是函数声明，如果去掉！以一个function开头javascript会把它理解为函数声明，会把他前置处理掉，最后留下一个括号会报语法错误
