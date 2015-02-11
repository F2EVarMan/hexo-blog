title: Less特性
date: 2015-02-11 14:09:07
tags:
- Less
categories:
- Less
---
###Less特性

#####变量

变量的作用就是把值定义在一个地方，然后在各处使用，这样能让代码更易维护：
```{bash}
// Variables
@link-color:        #428bca; // sea blue
@link-color-hover:  darken(@link-color, 10%);

// 用法
a,
.link {
  color: @link-color;
}
a:hover {
  color: @link-color-hover;
}
.widget {
  color: #fff;
  background: @link-color;
}
```
#####混合(Mixin)

在 LESS 中，混入是指在一个 CLASS 中引入另外一个已经定义的 CLASS，就像在当前 CLASS 中增加一个属性一样
```{bash}
// 定义一个border样式
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
//在其他样式中引用
#menu a {
  color: #111;
  .bordered;
}

.post a {
  color: red;
  .bordered;
}
```

#####嵌套规则
Less嵌套规则的写法是与HTML 中的 DOM 结构相对应的,可以很直观的管理区域的css
```{bash}
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
```
#####运算
less中的运算就是对数值型的 value（数字、颜色、变量等）进行加减乘除四则运算.
```{bash}
@base: 5%;
@filler: @base * 2;
@other: @base + @filler;

color: #888 / 4;
background-color: @base-color + #111;
height: 100% / 2 + @filler;
```
#####函数
Less 内置了多种函数用于转换颜色、处理字符串、算术运算等
```{bash}
@base: #f04615;
@width: 0.5;

.class {
  width: percentage(@width); // returns `50%`
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
```
####注释
Less中的注释与 JavaScript 中的注释方法一样,Less 中单行注释 (// 单行注释 ) 是不能显示在编译后的 CSS 中，所以如果你的注释是针对样式说明的请使用多行注释
```{bash}
/* 一个注释块
style comment! */
@var: red;

// 这一行被注释掉了！
@var: white;
```
####导入
可以导入一个 .less 文件，此文件中的所有变量就可以全部使用了,如果导入的文件是 .less 扩展名，则可以将扩展名省略掉
```{bash}
@import "library"; // library.less
@import "typo.css";
```
