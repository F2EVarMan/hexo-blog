title: AngularJS 表单验证
date: 2015-01-30 15:34:23
tags: 
- AngularJS  
- 表单验证
- Form
categories:
- AngularJS
---
###AngularJS表单验证
平常的表单验证主要面临几个问题:

- 数据的绑定
- 验证Form中的Element,如:input,select,textarea
- 错误信息如何展示
- 异步校验
- 拦截没有验证通过的表单提交

 AngularJS input表单域中提供了这几个验证选项:
 1. Required	验证某个表单是否为空
```{bash}
	<input type="text" required>
```
2.Minimum length	至少要有{number}个字符
```{bash}
	<input type="text"  ng-minlength=2>
```
3.Maximum length	最多有{number}个字符
```{bash}
	<input type="text" ng-maxlength=128>
```
4.Matches a pattern	匹配某个正则表达式
```{bash}
	<input type="text" ng-pattern=*/a-zA-Z/*>
```
5.Email	    匹配Email地址
```{bash}
	<input type="email" name='email' ng-model="entity.email">
```
6.Number 	验证表单项为数字
```{bash}
	<input type="number"  name="age" ng-model="entity.age">
```
7.Url 	验证表单项为合法的url地址
```{bash}
	<input type="url" name="homepage" ng-model="entity.weibo_url">
```

####在表单中控制变量,借助表单的属性对表单做出实时响应,
（可以使用 formName.inputFieldName.property）这样的格式来访问这些属性

formName.inputFieldName.$pristine (判断用户是否修改了表单,未修改则为true)

formName.inputFieldName.$dirty(只要用户修改过表单就返回 true)

formName.inputFieldName.$valid(判断表单内容是否合法,内容合法返回 true)

formName.inputFieldName.$invalid(表单内容不合法则返回true)

formName.inputFieldName.$error(包含表单所有验证内容及他们是否合法的信息,验证失败返值为true  ,通过验证为false)

####angularjs处理表单时还会根据表单当前状态添加一些css：

.ng-pristine,.ng-dirty,.ng-valid,.ng-invalid


