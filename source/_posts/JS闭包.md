title: JS闭包
date: 2015-03-25 09:42:06
tags:
- JavaScript
- 闭包
categorise:
- JavaScript
---
###JavaScript 闭包
在计算机科学中，闭包（Closure）是词法闭包（Lexical Closure）的简称，是引用了自由变量的函数。这个被引用的自由变量将和这个函数一同存在，即使已经离开了创造它的环境也不例外。所以，有另一种说法认为闭包是由函数和与其相关的引用环境组合而成的实体。闭包在运行时可以有多个实例，不同的引用环境和相同的函数组合可以产生不同的实例。
          --维基百科
JavaScript中的函数也是对象,函数也可以作为返回值和传参,函数里也可以嵌套,函数里面嵌套函数，内部函数里面如果引用了外部函数变量，变量就不会被回收。（闭包）
outer() 是一般函数,对于一般函数当函数调用结束以后,函数内部的局部变量就会被释放
```{bash}
  function outer(){
    var localVal=30;
    return localVal;
    }
    outer();//30

//变量不会被回收
    function outer(){
      var localVal=30;
      return function(){
        return localVal;
      }
    }

    var func=outer();
    func();//30
```
在前端方面闭包是很常见的
比如处理一些事件的点击,可能会在函数里面嵌套事件绑定,事件绑定里面可能就会用到外层的局部变量
```{bash}
!function(){
  var localData="localData here";
  document.addEventListener('click',function(){
    console.log(localData)
  })
}
```
在$.ajax方法中success的回调方法也可能用到外层函数的变量,因为有闭包存在,回调函数才可以访问到外层的变量
```{bash}
!function(){
  var localData="localData here";
  var url="http://f2evarman.github.io";
  $.ajax({
    url:url,
    success:function(){
      console.log(localData)
    }
  })
}
```
闭包也容易带来一些误解和错误
```{bash}
document.body.innerHTML="<div id="div1">aaa</div>"
+"<div id="div2">bbb</div><div id="div3">ccc</div>";
for(var i=0;i<4;i++){
  document.getElementById('div'+i).
  addEventListener('click',function(){
    alert(i);// 4
  })
}
```
这段代码本身的意思是想循环绑定事件，当点击aaa的时候输出1,bbb的时候输出2.可实际每次点击任何div返回的都是4
这就是因为闭包的原因,绑定事件是一个回调函数,当点击时候回调函数才会动态去拿到i的值,i的值在整个初始化循环之后就已经是4了
(for循环就跟作用域有关了在for循环的外面仍然可以拿到i的值,值是最后一次循环)

```{bash}
document.body.innerHTML="<div id="div1">aaa</div>"
+"<div id="div2">bbb</div><div id="div3">ccc</div>";
for(var i=0; i<4;i++){
  !function(i) {
    document.getElementById('div' + i).
    addEventListener('click', function() {
      alert(i); // 1,2,3
    })
  }(i)

}
```
在每一次循环的时候,用一个立即执行的匿名函数把内部函数包装起来,并且把每次遍历的i传到匿名函数里面.
在匿名函数里面再用参数i到内部函数里面去引用,这样当每次点击的时候就会取自每一个闭包环境下面的I,这个i就来源于每一次循环时候的赋值i

闭包还有另一个好处就是可以封装变量,函数有自己的作用域,定义的局部变量外部是不可以访问到的.
闭包的特性可以让我们去封装一些比较复杂的函数逻辑,expor.getUserId就可以在函数初始化以后还能访问到函数里面的变量
```{bash}
  (function(){
    var _userId=23492;
    var _typeId='item';
    var export={};
    function converter(userId){
      return +userId;
    }
    export.getUserId=function(){
      return converter(_userId)
    }
    export.getTypeId=function(){
      return _typeId;
    }
    window.export=export;
  }())
```
JavaScript之所以有闭包这个概念是因为它是一个第一类函数特性的语言,可以把函数当作对象传递，作为返回值.
闭包使用起来灵活方便,也不可避免,可以使用闭包做一些封装
闭包会导致一个作用域环境在函数调用结束后仍然没有办法被释放掉,不合理使用闭包会产生空间浪费
