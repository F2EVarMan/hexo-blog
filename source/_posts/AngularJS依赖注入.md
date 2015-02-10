title: AngularJS依赖注入
date: 2015-02-10 09:37:57
tags:
- AngularJS
- 依赖注入
categories:
- AngularJS
---
###AngularJS依赖注入
一个对象通常有三种方式可以获得对其依赖的控制权：
(1) 在内部创建依赖；
(2) 通过全局变量进行引用；
(3) 在需要的地方通过参数进行传递。
依赖注入是通过第三种方式实现的。其余两种方式会带来各种问题，例如污染全局作用域，
使隔离变得异常困难等。依赖注入是一种设计模式，它可以去除对依赖关系的硬编码，从而可以
在运行时改变甚至移除依赖关系。
依赖注入会事先自动查找依赖关系，并将注入目标告知被依赖的资源，这样就
可以在目标需要时立即将资源注入进去
AngularJS使用 $injetor （注入器服务）来管理依赖关系的查询和实例化
在运行时，任何模块启动时 $injetor 都会负责实例化，并将其需要的所有依赖传递进去
#####推断式注入声明
如果没有明确的声明，AngularJS会假定参数名称就是依赖的名称。因此，它会在内部调用
函数对象的 toString() 方法，分析并提取出函数参数列表，然后通过 $injector 将这些参数注入
进对象实例
这个过程只适用于未经过压缩和混淆的代码，因为AngularJS需要原始未经压缩的
参数列表来进行解析
#####显式注入声明
AngularJS提供了显式的方法来明确定义一个函数在被调用时需要用到的依赖关系。通过这
种方法声明依赖，即使在源代码被压缩、参数名称发生改变的情况下依然能够正常工作。
可以通过 $inject 属性来实现显式注入声明的功能。函数对象的 $inject 属性是一个数组，
数组元素的类型是字符串，它们的值就是需要被注入的服务的名称。
```{bash}
var aControllerFactory =
function aController($scope, greeter) {
	console.log("LOADED controller", greeter);
// ……控制器
};
aControllerFactory.$inject = ['$scope', 'greeter']; // Greeter服务
	console.log("greeter service");
}
// 我们应用的控制器
angular.module('myApp', [])
	.controller('MyController', aControllerFactory)
	.factory('greeter', greeterService);
// 获取注入器并创建一个新的作用域
var injector = angular.injector(['ng', 'myApp']),
controller = injector.get('$controller'),
rootScope = injector.get('$rootScope'),
newScope = rootScope.$new();
// 调用控制器
controller('MyController', {$scope: newScope});
```
#####行内注入声明
AngularJS提供的注入声明的最后一种方式，是可以随时使用的行内注入声明。这种方式其
实是一个语法糖，它同前面提到的通过 $inject 属性进行注入声明的原理是完全一样的，但允许
我们在函数定义时从行内将参数传入。此外，它可以避免在定义过程中使用临时变量。
在定义一个AngularJS的对象时，行内声明的方式允许我们直接传入一个参数数组而不是一
个函数。数组的元素是字符串，它们代表的是可以被注入到对象中的依赖的名字，最后一个参数
就是依赖注入的目标函数对象本身。
```{bash}
angular.module('myApp')
	.controller('MyController', ['$scope', 'greeter', function($scope, greeter) {
}]);
```
由于需要处理的是一个字符串组成的列表，行内注入声明也可以在压缩后的代码中正常运
行。通常通过括号和声明数组的 [] 符号来使用它。