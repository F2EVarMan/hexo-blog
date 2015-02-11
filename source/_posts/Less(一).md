title: Less(一)
date: 2015-02-10 14:16:15
tags:
- Less
categories:
- Less
---
###Less(一)
Less 是一门 CSS 预处理语言，它扩充了 CSS 语言，增加了诸如变量、混合（mixin）、函数等功能，让 CSS 更易维护、方便制作主题、扩充。

Less 可以运行在 Node、浏览器和 Rhino 平台上。网上有很多第三方工具帮助你编译 Less 源码
如下:
```{bash}
@base: #f938ab;

.box-shadow(@style, @c) when (iscolor(@c)) {
  -webkit-box-shadow: @style @c;
  box-shadow:         @style @c;
}
.box-shadow(@style, @alpha: 50%) when (isnumber(@alpha)) {
  .box-shadow(@style, rgba(0, 0, 0, @alpha));
}
.box {
  color: saturate(@base, 5%);
  border-color: lighten(@base, 30%);
  div { .box-shadow(0 0 5px, 30%) }
}
```
编译为css后：
```{bash}
.box {
  color: #fe33ac;
  border-color: #fdcdea;
}
.box div {
  -webkit-box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
}
```
####使用Less
Less 可以通过 npm 在命令行上运行；在浏览器上作为脚本文件下载；或者集成在广大的第三方工具内
######安装
在服务器端最容易的安装方式就是通过 npm （node.js 的包管理器），将less安装到全局，方法如下：
```{bash}
$ npm install -g less
```
######命令行用法
安装 Less 后，就可以在命令行上调用 Less 编译器了，如下：
```{bash}
$ lessc styles.less > styles.css
```
若要输出压缩过的 CSS，只需添加 -x 选项。如果希望获得更好的压缩效果，还可以通过 --clean-css 选项启用 Clean CSS 进行压缩。

######客户端用法
在浏览器上跑 less.js 非常方便开发，但是不推荐用于生产环境。
在客户端使用 Less.js 是最容易的方式，并且在开发阶段很方便，但是，在生产环境中，性能和可靠性非常重要，
```{bash}
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```
下载 less.js 并通过 <script></script> 标签将其引入，放置于页面的 <head> 元素内
```{bash}
<script src="less.js" type="text/javascript"></script>
```

	(建议使用Koala来进行自动编译和压缩,方便快捷,下一篇将会介绍Koala)