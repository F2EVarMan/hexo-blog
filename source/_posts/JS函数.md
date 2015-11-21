title: JS函数
date: 2015-03-24 09:35:10
tags:
- JavaScript
- 函数
categories:
- JavaScript
---
###JavaScript函数
函数是一块JavaScript代码,被定义一次,但可以执行和调用多次.JavaScript中的函数也是对象,所以函数可以像其他对象那样操作和传递,所以也常叫JavaScript中的函数为函数对象。
这是一个标准的函数由函数名，参数列表，函数体组成:
```{bash}
function foo(x,y){
  if(typeof x == 'number' && typeof y ==='number'){
    return x + y;
  }else{
    return 0;
  }
}

foo(1,2); // 3
```
函数不同的调用方法:
```{bash}
  foo();//直接调用
  o.method();//对象方法
  new Foo();//构造器
  func.call(o);// call/apply/bind
```
创建函数 常用的两种方式就是函数声明和函数表达式
一个完整以function 开头定义一个函数叫函数声明
将一个函数赋值给一个变量叫做函数表达式
匿名函数自执行也是函数表达式
将函数对象作为一个返回值也是函数表达式
有名字的函数赋值给一个变量叫做命名式函数表达式

函数声明
```{bash}
  function add(a,b){
    a = +a;  //+ a 如果a是字符串会把a转化为number
    b = +b;
    if(isNaN(a) || isNaN(b)){
      return ;
    }
    return a + b;
  }
```
函数表达式 
```{bash}
// function variable
function add(a,b){
  // do something
}

//IFE(立即执行函数)
(function(){
  //do sth
})()

return function(){
  //do sth
}

//NFE(命名函数表达式)
var add=function foo(a,b){
  //do sth
}
```

函数声明和表达式的区别
函数声明和变量声明 会被前置但是 赋值给变量声明的函数不会被前置
函数声明不能被立即调用
命名式函数表达式有很多Bug,不推荐使用
```{bash}
  var num=add(1,2);
  console.log(num); //result: 3
  function add(a,b){
    a = +a;  //+ a 如果a是字符串会把a转化为number
    b = +b;
    if(isNaN(a) || isNaN(b)){
      return ;
    }
    return a + b;
  }
/*

 */
  var num=add(1,2);
  console.log(num); //报错,找不到函数
  var add=function(a,b){
    a = +a;  //+ a 如果a是字符串会把a转化为number
    b = +b;
    if(isNaN(a) || isNaN(b)){
      return ;
    }
    return a + b;
  }
```
用函数构造器创建函数并不常见，函数构造器创建的函数可以拿到全局变量 但是拿不到外层函数的局部变量
```{bash}
var func=new Function('a','b','console.log(a+b);');
func(1,2);//3
var func=Function('a','b','console.log(a+b);');
func(1,2);//3
```
this 全局的this 一般指向全局对象,在浏览器里面一般指window
```{bash}
  console.log(this.document === document); //true
  console.log(this === window);// true
  this.a=37;
  console.log(window.a);//37
```
一般函数的this 也是指向window  nodejs 指向 global
```{bash}
function f1(){
  return this;
}
f1() === window //true
function f2(){
  "use strict";// see strict mode
  return this;
}
f2() === undefined // true
```
函数如果作为一个对象的属性，常叫做对象的方法。
调用对象方法的时候一般this会指向对象
只要函数作为对象的方法调用,this就会指向对象
```{bash}
var o={
  pop:37,
  f:function(){
    return this.pop;
  }
};
console.log(o.f());// 37

var o={pop:37};
function independent(){
  return this.pop;
}
o.f=independent;
console.log(o.f);//37
```
对象原形链上的this,调用对象原形上的方法的时候,原形上的this还是指向当前调用对象
```{bash}
var o={f:function(){return this.a + this.b}};
var p=Object.create(o);
p.a=1;
p.b=4;
console.log(p.f()); //5
```
当使用New来创建一个构造器调用的时候 ,this 会指向函数的prototype .
最后函数的返回值如果没写return语句或者return 的是一个基本类型的话会将this返回 , 
如果最后return语句返回的是一个对象的话会将对象作为返回值
```{bash}
  function MyClass(){
    this.a=37;
  }
  var o=new MyClass();
  console.log(o.a);//37

  function c2(){
    this.a=37;
    return {a:38}
  }
  o=new c2();
  console.log(o.a);//38
```
call 和apply可以修改函数执行时里面的this
通过call方法第一个参数作为你想当作this的对象 ,后面的是想要去添加的参数
apply 传参时把参数作为数组传进去
```{bash}
  function add(c,d){
    return this.a + this.b + c + b;
  }
  var o={a:1,b:3};
  add.call(a,5,7);//1+3+5+7=16
  add.apply(o,[10,20]);//1+3+10+20=34

  function bar{
    console.log(Object.prototype.toString.call(this))
  };
  bar(7);// object number
```
bind 会按照之前绑定的 this 
```{bash}
  function f(){
    return this.a;
  }
  var g=f.bind({a:'test'});
  console.log(g());//test
  var o={a:37,f:f,b:b};
  console.log(o.f(),o.g());//37,test
```
函数属性 arguments
可以通过 函数对象的length属性 拿到 函数参数的长度 ,通过name属性拿到函数名字
实际传参的个数 可以通过 arguments.length拿到
arguments 是一个类数组的对象，他的原形并不是Array.prototype
可以通过索引 访问arguments对象 
如果参数没有传进来的话 实际上arguments和对应的参数是没有绑定关系的
在严格模式下 arguments 无法改写 参数
```{bash}
function foo(x,y,z){
  arguments.length;//2
  arguments[0];//1;
  arguments[0]=10;
  x;//10
  arguments[2]=100;
  z; //undefined
  arguments.callee === foo;//true callee 属性是 arguments 对象的一个成员，他表示对函数对象本身的引用，这有利于匿名函数的递归或确保函数的封装性
}
foo(1,2);
foo.length;//3
foo.name;//foo
```
