title: ui-router(一)
date: 2015-02-02 15:52:34
tags:
- AngularJS
- 路由
- ui-router
categories:
- AngularJS
---
###ui-router(一)
如图一根据左侧nav,触发不同路由更改右侧的模板

![ui-router](/images/ui-router1.png)
根据上的界面设计，我们计划该页面能从一个页面导航到另外一个页面, 当点击个人信息时，我们将在右面显示个人信息的内容，点击其它导航菜单也会有类似的效果. 
首先我们需要创建5个页面，这其中包括4个模板和一个主页面
1.index.html
2.home.html
3.change.html
4.zone.html
5.info.html

html我们就简要带过了,看一下每个页面的代码

index.html
```{bash}
	<!DOCTYPE html>	
	<html lang="en" >
	<head>
		<meta charset="UTF-8">	
		<title>February 2nd,2015</title>
		<link rel="stylesheet" href="css/bootstrap.min.css">	
		<script src="lib/angular.min.js"></script>
		<script src="lib/angular-ui-router.js"></script>
		<script src="js/app.js"></script>
	</head>
	<body ng-app="myApp">
		<div class="container">
			<h1 class="text-center">Ui-router</h1>
			<div ui-view></div>
		</div>
	</body>
	</html>
```
index在body上 声明了an-app 并在下面的div声明了ui-view 说明这个是路由会替换的template
home.html

```{bash}
<div class="row">
	<div class="col-md-3">
		<ul class="nav nav-pills nav-stacked">
			<li role="presentation"class="active">
				<a href="#" class="btn btn-default" ui-sref="user">首页</a>
			</li>
			<li role="presentation">
				<a class="btn btn-default" ui-sref=".change">修改密码</a>
			</li>
			<li role="presentation">
				<a class="btn btn-default" ui-sref=".zone">空间</a>
			</li>
			<li role="presentation">
				<a class="btn btn-default" ui-sref=".info">个人信息</a>
			</li>
		</ul>
	</div>
	<div class="col-md-9">
		<div ui-view>
			<p>I'm Varman</p>
		</div>
	</div>
</div>
```
ui-sref指令声明了路由状态

change.html

```{bash}
<form  class="form-horizontal" role="form">
	<div class="form-group">
		<label  class="control-label col-md-2">旧密码:</label>
		<div class="col-md-10">
			<input type="password" class="form-control" placeholder="请输入旧密码"></div>
	</div>
	<div class="form-group">
		<label  class="control-label col-md-2">新密码:</label>
		<div class="col-md-10">
			<input type="password" class="form-control" placeholder="请输入新密码"></div>
	</div>
	<div class="form-group">
		<label  class="control-label col-md-2">确认密码:</label>
		<div class="col-md-10">
			<input type="password" class="form-control" placeholder="请再次输入新密码"></div>
	</div>
	<div class="form-group">
		<div class="col-md-10 col-md-offset-2">
			<button class="btn btn-defalut">确认修改</button>
		</div>
	</div>
</form>
```
zone.html

```{bash}
<div class="row">
    <div class="col-md-4">
        <div class="thumbnail">
            <img src="" alt="">
            <div class="caption">
                <h3>The picture</h3>
                <p>
                    F2E
                </p>
                <p>
                    <a href="http://weibo.com/varman" class="btn btn-primary">varman</a>
                    <a href="http://weibo.com/varman" class="btn btn-default">varman</a>
                </p>
            </div>
        </div>
    </div>
    <div class="col-md-4">
        <div class="thumbnail">
            <img src="" alt="">
            <div class="caption">
                <h3>The picture</h3>
                <p>
                    F2E
                </p>
                <p>
                    <a href="http://weibo.com/varman" class="btn btn-primary">varman</a>
                    <a href="http://weibo.com/varman" class="btn btn-default">varman</a>
                </p>
            </div>
        </div>
    </div>
    <div class="col-md-4">
        <div class="thumbnail">
            <img src="" alt="">
            <div class="caption">
                <h3>The picture</h3>
                <p>
                    F2E
                </p>
                <p>
                    <a href="http://weibo.com/varman" class="btn btn-primary">varman</a>
                    <a href="http://weibo.com/varman" class="btn btn-default">varman</a>
                </p>
            </div>
        </div>
    </div>
    <div class="col-md-4">
        <div class="thumbnail">
            <img src="" alt="">
            <div class="caption">
                <h3>The picture</h3>
                <p>
                    F2E
                </p>
                <p>
                    <a href="http://weibo.com/varman" class="btn btn-primary">varman</a>
                    <a href="http://weibo.com/varman" class="btn btn-default">varman</a>
                </p>
            </div>
        </div>
    </div>
    <div class="col-md-4">
        <div class="thumbnail">
            <img src="" alt="">
            <div class="caption">
                <h3>The picture</h3>
                <p>
                    F2E
                </p>
                <p>
                    <a href="http://weibo.com/varman" class="btn btn-primary">varman</a>
                    <a href="http://weibo.com/varman" class="btn btn-default">varman</a>
                </p>
            </div>
        </div>
    </div>
    <div class="col-md-4">
        <div class="thumbnail">
            <img src="" alt="">
            <div class="caption">
                <h3>The picture</h3>
                <p>
                    F2E
                </p>
                <p>
                    <a href="http://weibo.com/varman" class="btn btn-primary">varman</a>
                    <a href="http://weibo.com/varman" class="btn btn-default">varman</a>
                </p>
            </div>
        </div>
    </div>
</div>
```
info.html

```{bash}
<div class="jumbotron">
    <h1>
        Hello,everyone!
    </h1>
    <p>
        I'm f2e
    </p>
    <p>
        <a href="http://weibo.com/varman" class="btn btn-primary btn-lg">varman</a>
    </p>
</div>
```

接下来是主要内容在index页面加载了angularjs 和ui-router,以及自己写的app.js
在app.js中我们首先声明一下angular模块,并依赖了ui.router以便于使用ui-router

```{bash}
var myApp=angular.module('myApp',['ui.router'])
```
完后就要开始写路由状态了我们把路由统一写在config里把$sateProvider 和$urlRouterProvider 当作参数传了进去

```{bash}
myApp.config(function ($stateProvider,$urlRouterProvider){
	/*do……*/
	}
```
$urlRouterProvider.otherwise()用来声明默认路由状态

```{bash}
	$urlRouterProvider.otherwise('/user');
```
接下来就开始写每个状态所对应的url和template了
全部app.js代码
```{bash}
/*
声明angular模块 myApp，依赖ui.router
 */
var myApp=angular.module('myApp',['ui.router'])
/*
一般把路由状态写在配置当中,config可以在实际跑起来之前做一些配置工作
把$stateProvider和$urlRouterProvider作为参数传入，
这样就可以在这个应用程序中配置路由
 */
myApp.config(function ($stateProvider,$urlRouterProvider){
/*
如果没有路由能匹配当前页面url状态的话就会默认将路由至/user
 */
	
	$urlRouterProvider.otherwise('/user');
/*
声明路由状态及所对应的url 和template
 */	
	$stateProvider
		.state('user',{
			url:"/user",
			templateUrl:"tpls/home.html"
		})
/*
这里定义state状态的时候写了 "." 意为着 这是user下面的子页面属于嵌套路由
 */		
		.state('user.change',{
			url:"/change",
			templateUrl:"tpls/change.html"
		})
		.state('user.zone',{
			url:"/zone",
			templateUrl:"tpls/zone.html"
		})
		.state('user.info',{
			url:"/info",
			templateUrl:"tpls/info.html"
		})

})

```

done~这只是ui-router的初级应用
[github链接](https://github.com/F2EVarMan/study/tree/master/February2nd2015)


