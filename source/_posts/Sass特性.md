title: Sass特性
date: 2015-02-11 14:42:56
tags:
- Sass
categories:
- Sass
---
###Sass特性

#####变量
sass的变量是$开头，后面紧跟变量名，如果值后面加上!default则表示默认值。
```{bash}
//sass style
//-------------------------------
$fontSize: 12px;
body{
    font-size:$fontSize;
}
```

sass的默认变量一般是用来设置默认值，然后根据需求来覆盖的，覆盖的方式也很简单，只需要在默认变量之前重新声明下变量即可
在选择器中声明的变量会覆盖外面全局声明的变量。
```{bash}
//sass style
//-------------------------------
$baseLineHeight:        2;
$baseLineHeight:        1.5 !default;
body{
    line-height: $baseLineHeight; 
}

//css style
//-------------------------------
body{
    line-height:2;
}
```
特殊变量
一般我们定义的变量都为属性值，可直接使用，但是如果变量作为属性或在某些特殊情况下等则必须要以#{$variables}形式使用。
```{bash}
//sass style
//-------------------------------
$borderDirection:       top !default; 
$baseFontSize:          12px !default;
$baseLineHeight:        1.5 !default;

//应用于class和属性
.border-#{$borderDirection}{
  border-#{$borderDirection}:1px solid #ccc;
}
//应用于复杂的属性值
body{
    font:#{$baseFontSize}/#{$baseLineHeight};
}

//css style
//-------------------------------
.border-top{
  border-top:1px solid #ccc;
}
body {
  font: 12px/1.5;
}
```
多值变量
多值变量分为list类型和map类型，简单来说list类型有点像js中的数组，而map类型有点像js中的对象。
list
list数据可通过空格，逗号或小括号分隔多个值，可用nth($var,$index)取值
```{bash}
//一维数据
$px: 5px 10px 20px 30px;

//二维数据，相当于js中的二维数组
$px: 5px 10px, 20px 30px;
$px: (5px 10px) (20px 30px);
//sass style
//-------------------------------
$linkColor:         #08c #333 !default;//第一个值为默认值，第二个鼠标滑过值
a{
  color:nth($linkColor,1);

  &:hover{
    color:nth($linkColor,2);
  }
}

```
map
map数据以key和value成对出现，其中value又可以是list。格式为：$map: (key1: value1, key2: value2, key3: value3);。可通过map-get($map,$key)取值。
```{bash}
$heading: (h1: 2em, h2: 1.5em, h3: 1.2em);
//sass style
//-------------------------------
$headings: (h1: 2em, h2: 1.5em, h3: 1.2em);
@each $header, $size in $headings {
  #{$header} {
    font-size: $size;
  }
}
```
#####嵌套
sass的嵌套包括两种：一种是选择器的嵌套；另一种是属性的嵌套。我们一般说起或用到的都是选择器的嵌套。

选择器嵌套
所谓选择器嵌套指的是在一个选择器中嵌套另一个选择器来实现继承，从而增强了sass文件的结构性和可读性。
在选择器嵌套中，可以使用&表示父元素选择器
```{bash}
//sass style
//-------------------------------
#top_nav{
  line-height: 40px;
  text-transform: capitalize;
  background-color:#333;
  li{
    float:left;
  }
  a{
    display: block;
    padding: 0 10px;
    color: #fff;

    &:hover{
      color:#ddd;
    }
  }
}
```
属性嵌套
所谓属性嵌套指的是有些属性拥有同一个开始单词，如border-width，border-color都是以border开头
```{bash}
//sass style
//-------------------------------
.fakeshadow {
  border: {
    style: solid;
    left: {
      width: 4px;
      color: #888;
    }
    right: {
      width: 2px;
      color: #ccc;
    }
  }
}

```
@at-root
用来跳出选择器嵌套的
```{bash}
//sass style
//-------------------------------
//没有跳出
.parent-1 {
  color:#f00;
  .child {
    width:100px;
  }
}

//单个选择器跳出
.parent-2 {
  color:#f00;
  @at-root .child {
    width:200px;
  }
}

//多个选择器跳出
.parent-3 {
  background:#f00;
  @at-root {
    .child1 {
      width:300px;
    }
    .child2 {
      width:400px;
    }
  }
}

```
#####混合
sass中使用@mixin声明混合，可以传递参数，参数名以$符号开始，多个参数以逗号分开，也可以给参数设置默认值。声明的@mixin通过@include来调用。
```{bash}
//sass style
//-------------------------------   
@mixin opacity($opacity:50) {
  opacity: $opacity / 100;
  filter: alpha(opacity=$opacity);
}

//css style
//-------------------------------
.opacity{
  @include opacity; //参数使用默认值
}
.opacity-80{
  @include opacity(80); //传递参数
}
```
#####继承
sass中，选择器继承可以让选择器继承另一个选择器的所有样式，并联合声明。使用选择器的继承，要使用关键词@extend，后面紧跟需要继承的选择器。
```{bash}
//sass style
//-------------------------------
h1{
  border: 4px solid #ff9aa9;
}
.speaker{
  @extend h1;
  border-width: 2px;
}

//css style
//-------------------------------
h1,.speaker{
  border: 4px solid #ff9aa9;
}
.speaker{
  border-width: 2px;
}
```
#####函数
sass定义了很多函数可供使用，当然你也可以自己定义函数，以@fuction开始。sass的官方函数链接为：sass fuction，实际项目中我们使用最多的应该是颜色函数，而颜色函数中又以lighten减淡和darken加深为最，其调用方法为lighten($color,$amount)和darken($color,$amount)，它们的第一个参数都是颜色值，第二个参数都是百分比。
```{bash}
//sass style
//-------------------------------                     
$baseFontSize:      10px !default;
$gray:              #ccc !defualt;        

// pixels to rems 
@function pxToRem($px) {
  @return $px / $baseFontSize * 1rem;
}

body{
  font-size:$baseFontSize;
  color:lighten($gray,10%);
}
.test{
  font-size:pxToRem(16px);
  color:darken($gray,10%);
}

//css style
//-------------------------------
body{
  font-size:10px;
  color:#E6E6E6;
}
.test{
  font-size:1.6rem;
  color:#B3B3B3;
}
```
#####运算
sass具有运算的特性，可以对数值型的Value(如：数字、颜色、变量等)进行加减乘除四则运算。请注意运算符前后请留一个空格，不然会出错。
```{bash}
$baseFontSize:          14px !default;
$baseLineHeight:        1.5 !default;
$baseGap:               $baseFontSize * $baseLineHeight !default;
$halfBaseGap:           $baseGap / 2  !default;
$samllFontSize:         $baseFontSize - 2px  !default;

//grid 
$_columns:                     12 !default;      // Total number of columns
$_column-width:                60px !default;   // Width of a single column
$_gutter:                      20px !default;     // Width of the gutter
$_gridsystem-width:            $_columns * ($_column-width + $_gutter); //grid system width
```
#####条件判断及循环
@if判断
@if可一个条件单独使用，也可以和@else结合多条件使用
```{bash}
//sass style
//-------------------------------
$lte7: true;
$type: monster;
.ib{
    display:inline-block;
    @if $lte7 {
        *display:inline;
        *zoom:1;
    }
}
p {
  @if $type == ocean {
    color: blue;
  } @else if $type == matador {
    color: red;
  } @else if $type == monster {
    color: green;
  } @else {
    color: black;
  }
}

//css style
//-------------------------------
.ib{
    display:inline-block;
    *display:inline;
    *zoom:1;
}
p {
  color: green; 
}
```
三目判断
语法为：if($condition, $if_true, $if_false) 。三个参数分别表示：条件，条件为真的值，条件为假的值。
```{bash}
if(true, 1px, 2px) => 1px
if(false, 1px, 2px) => 2px
```
for循环
for循环有两种形式，分别为：@for $var from <start> through <end>和@for $var from <start> to <end>。$i表示变量，start表示起始值，end表示结束值，这两个的区别是关键字through表示包括end这个数，而to则不包括end这个数。
```{bash}
//sass style
//-------------------------------
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}

//css style
//-------------------------------
.item-1 {
  width: 2em; 
}
.item-2 {
  width: 4em; 
}
.item-3 {
  width: 6em; 
}
```
@each循环
语法为：@each $var in <list or map>。其中$var表示变量，而list和map表示list类型数据和map类型数据。sass 3.3.0新加入了多字段循环和map数据循环。
```{bash}
//sass style
//-------------------------------
$animal-data: (puma, black, default),(sea-slug, blue, pointer),(egret, white, move);
@each $animal, $color, $cursor in $animal-data {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
    border: 2px solid $color;
    cursor: $cursor;
  }
}

//css style
//-------------------------------
.puma-icon {
  background-image: url('/images/puma.png');
  border: 2px solid black;
  cursor: default; 
}
.sea-slug-icon {
  background-image: url('/images/sea-slug.png');
  border: 2px solid blue;
  cursor: pointer; 
}
.egret-icon {
  background-image: url('/images/egret.png');
  border: 2px solid white;
  cursor: move; 
}
```