title: JS语句
date: 2015-03-11 16:41:01
tags:
- JavaScript
- 语句
categorise:
- JavaScript
---
###JavaScript 语句
JavaScript程序由语句组成,语句遵循特定的语法规则

#####block
block块语句,常用于组合0-多个语句.语句用一对花括号定义.
JavaScript有函数作用域,全局作用域但是没有块级作用域所以在for循环外面依然可以拿到I的值 

#####var
```{bash}
var a=b=1;   // b 相当于是全局变量
```
#####try catch   
try catch提供了一个异常补获机制
先执行 try 中的语句,如果发生异常会执行catch 中的语句,不管有没有异常都会执行finally
```{bash}
try{
//do sth
}catch{

}finally{

}
```
#####function
function用来创建函数对象
```{bash}
function fd(){

}   //  函数声明

var fe=function(){

}   // 函数表达式
```
#####for in  
遍历对象中的属性(for in 对象受原型链影响)
```{bash}
var p;
var obj={x:1,y:2}

for(p in obj){

}
```
#####switch
```{bash}
switch(val){
case 1:

case 2:

default:

}
```
#####循环
for/do while

with修改当前作用域不建议使用with
```{bash}
with({x:1}){
     console.log(x);
}
```

#####严格模式
一种特殊的执行模式,修复语言不足,增强安全性.
-不允许使用with
-所有变量必须声明,赋值给未声明的变量报错,而不是隐式创建全局变量
-eval中的代码不能创建eval所在作用域下的变量,函数.而是为eval单独创建一个作用域,并在eval返回时丢弃.
-函数中的特殊对象arguments是静态副本,而不是像非严格模式那样,修改arguments或修改参数变量会互相影响
-删除configurable=false的属性时报错,而不是忽略
-禁止八进制字面量,如010(八进制的8)
-eval,arguments变为关键字,不可作为变量名,函数名等
-一般函数调用时(不是对象的方法调用,也不使用apply/call/bind等修改this)this指向null,而不是全局对象
-若使用apply/call,当传入Null或undefined时,this将指向null或undefined,而不是全局对象
-试图修改不可写属性(writable=false),在不可扩展的对象上添加属性时报TypeError,而不是忽略
-arguments.caller,arguments.callee被禁用
