title: css字体
date: 2015-03-05 13:10:15
tags:
- CSS
- 字体
categories:
- CSS
---
### css字体
字体误区
-宋体非宋体,黑体非黑体
-宋体和黑体都是指一类字体
-Windows:中易宋体(SimSun),Mac:华文宋体(STSong)
-Windows:中易黑体(SimHei),Mac:华文黑体(STHei)

与设计师沟通时尽量用全称或者英文

书写css字体时不要只写中文,要保证英文字体在中文字体前面,浏览器渲染的时候是从前往后找的.
字体书写顺序还要保证Mac->Linux->Windows
不要PSD设计什么字体就在font-family里面设置什么字体

一种直接自动的字体设置方式
根据浏览器和所在系统自动设置字体
```{bash}
body{
	font-family:sans-serif;
}
```
还有一种尽量根据每一个系统设置最佳的字体
```{bash}
body{
	font-family:'Helvetica Neue',Arial,'Hiragina Sans GB','STheiti',
	'Microsoft YaHei',
	'WenQuanYi Micro Hei',
	sans-serif;
}
```

