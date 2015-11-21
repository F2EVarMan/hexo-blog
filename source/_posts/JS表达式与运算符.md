title: JS表达式与运算符
date: 2015-03-06 16:40:27
tags:
- JavaScript
- 表达式
- 运算符
categories:
- JavaScript
---
###JS表达式和运算符

#####表达式
在维基百科中 表达式是指能计算出值得任何可用程序单元
JS权威指南中  表达式是一种JS短语,可使JS解释器用来产生一个值.

######原始表达式 (常量,直接量(3.14,"test"),关键字(null,this,true),变量(i,k,j))

原始表达式可以和运算符  组成 符合表达式 如
```{bash}
10 * 20
```
######除了原始表达式以外,还有 数组,对象的初始化表达式
```{bash}
[1,2]   //等价于 new Array(1,2)
[1,,,2] //等价于[1,undefined,undefined,2]
{x:1,y:2} //等价于 var o=new Object();     o.x=1,o.y=2
```
######函数表达式
```{bash}
var fe=function(){};  //把命名函数赋值给变量
(function(){console.log('hello world');})() // 或者把函数 用括号括起来 直接调用
```
######属性访问表达式
```{bash}
var o={x:1}
o.x
o['x']
//可以通过 o.x 和 o['x'] 访问
```
######调用表达式
```{bash}
func();
//函数名加上括号来调用
```
######对象创建表达式
```{bash}
new Func(1,2)
new Object
//比如 用new 一个构造器或者函数
```
######运算符

运算符常用于表达式之间 
按照运算符操作数的数量 可以分为 一元  二元 三元 运算符
```{bash}
+ num + num 如果num是字符串会把num转化为number
a + b
c ? a : b
```
除了按照数量分  还有  

赋值运算符  x+=1
比较运算符 a == b
算术符  a - b
位运算符 a | b
逻辑运算符 exp1 && exp2
字符串 "a"+"b"


######特殊运算符

条件运算符     c?a:b 
逗号运算符      a,b     从左到右计算表达式的值 最终取最右边的 
delete    	 delete obj.x     删除对象上的属性
in    		 "document" in window     判断对象里面有没有这个 
instanceof	 obj instanceof func     判断对象类型基于原型链
new 		new className();     创建新对象
this 		return this 
typeof		typeof 100
void		void 0 

