title: AngularJS指令
date: 2015-02-05 17:50:15
tags:
- AngularJS
- 指令
categories:
- AngularJS
---
###AngularJS指令
指令定义
对于指令，可以把它简单的理解成在特定DOM元素上运行的函数，指令可以扩展这个元素
的功能。
学习指令最快的途径就是亲自使用它
当AngularJS编译HTML时就会调用指令调用指令意味着执行指令背后与之相关联的JavaScript代码， 这些代码是我们用指令定义写出来的
通过AngularJS模块API中的 .directive() 方法， 我们可以通过传入一个字符串和一个函数来注册一个新指令。其中字符串是这个指令的名字，指令名应该是驼峰命名风格的，函数应该返回一个对象。directive()方法返回的对象中包含了用来定义和配置指令所需的方法和属性。
```{bash}
	var myApp=angular.module('myApp',[]);
	myApp.directive('myDirective',function(){
		return{
			restrict: String,
			priority: Number,
			terminal: Boolean,
			template: String or Template Function:
			function(tElement, tAttrs) {...},
			templateUrl: String,
			replace: Boolean or String,
			scope: Boolean or Object,
			transclude: Boolean,
			controller: String or
			function(scope, element, attrs, transclude, otherInjectables) { ... },
			controllerAs: String,
			require: String,
			link: function(scope, iElement, iAttrs) { ... },
			compile: // 返回一个对象或连接函数，如下所示：
			function(tElement, tAttrs, transclude) {
			return {
			pre: function(scope, iElement, iAttrs, controller) { ... },
			post: function(scope, iElement, iAttrs, controller) { ... }
			}
		}	
			
		})
```
返回对象里定义了指令的全部行为
一个JavaScript对象由键和值组成。当一个给定键的值被设置为一个字符串、布
尔值、数字、数组或对象时，我们把这个键称为属性。当把键设置为函数时，
我们把它叫做方法

######restrict 
restrict 是一个可选的参数。它告诉AngularJS这个指令在DOM中可以何种形式被声明。默
认AngularJS认为 restrict 的值是 A ，即以属性的形式来进行声明。
	可选值 E(元素 element)
		A(属性 attribute)
		C(类名 class)
		M(注释)

		(这些选项可以单独使用，也可以混合在一起使用)

######priority		
 优先级参数可以被设置为一个数值。大多数指令会忽略这个参数，使用默认值0，但也有些
场景设置高优先级是非常重要甚至是必须的.例如， ngRepeat 将这个参数设置为1000，这样就可
以保证在同一元素上，它总是在其他指令之前被调用

######terminal
这个参数用来告诉AngularJS停止运行当前元素上比本指令优先级低的指令。但同当前指令优先级相同的指令还是会被执行。

######template
一段HTML文本或一个可以接受两个参数的函数，参数为 tElement 和 tAttrs ，并返回一个代表模板的字符
串。

######templateUrl
一个代表外部HTML文件路径的字符串 或   一个可以接受两个参数的函数，参数为 tElement 和 tAttrs ，并返回一个外部HTML文件
路径的字符串

(在本地开发时调用模板需要启动本地服务器)

######replace
replace 是一个可选参数，如果设置了这个参数，值必须为 true ，true意味着将会对元素进行替换因为默认值为 false 。默认值意味着模板会被当作子元素插入到调用此指令的元素内部

######scope
scope会创建一个隔离作用域,隔离作用域内加上绑定策略的话可以同指令外部的作用域进行数据绑定
为了让新的指令作用域可以访问当前本地作用域中的变量，需要使用下面三种别名中的一种:
	1.@ 使用 @ 符号将本地作用域同DOM属性的值进行绑定。指令内部作用域可以使用外部作用域的变量
	2.=   与父scope中的属性进行双向数据绑定
	3.&   传递一个来自父scope中的值稍后调用

######tansclude
transclude 嵌入 嵌入通常用来创建可复用的组件，典型的例子是模态对话框或导航栏
只有当你希望创建一个可以包含任意内容的指令时， 才使用 transclude: true 

######controller
controller 参数可以是一个字符串或一个函数。 当设置为字符串时， 会以字符串的值为名字，
来查找注册在应用中的控制器的构造函数我们可以将任意可以被注入的AngularJS服务传递给控制器。

######controllerAs
controllerAs 参数用来设置控制器的别名， 可以以此为名来发布控制器， 并且作用域可以访
问 controllerAs 。这样就可以在视图中引用控制器，甚至无需注入 $scope 

require （字符串或数组）
require 参数可以被设置为字符串或数组， 字符串代表另外一个指令的名字。 require 会将控
制器注入到其值所指定的指令中，并作为当前指令的链接函数的第四个参数。

require 参数的值可以用下面的前缀进行修饰，这会改变查找控制器时的行为：
?
如果在当前指令中没有找到所需要的控制器，会将 null 作为传给 link 函数的第四个参数。
^
如果添加了 ^ 前缀，指令会在上游的指令链中查找 require 参数所指定的控制器。
?^
将前面两个选项的行为组合起来，我们可选择地加载需要的指令并在父指令链中进行查找。
没有前缀
如果没有前缀，指令将会在自身所提供的控制器中进行查找，如果没有找到任何控制器（或
具有指定名字的指令）就抛出一个错误
