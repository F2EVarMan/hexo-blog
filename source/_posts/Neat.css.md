title: Neat.css
date: 2015-03-05 14:32:15
tags:
- CSS
categories:
- CSS
---
###Neat.css

Neat.css是基于normalize的 CSS Reset,兼容ie6+,及其他浏览器，由阿里妈妈打造.

normalize是尽量保持浏览器原有样式,这在很多实际web开发当中会出现bug.
而Neat 把margin,padding 重置为0,结合了Reset和Neat的优点.

Neat.css解决的问题
-解决低级浏览器常见Bug
-统一效果
-向后兼容
-考虑响应式
-考虑移动端

个人比较喜欢 Neat的font-family
字体的话又要考虑中英文,还要考虑系统问题
Neat统一了font-family的设置
```{bash}
/**
 * 1. 防止元素中「font-family」不能继承
 * 2. 西文字体和 OS X 字体写在前面
 * 3. Opera 12.1 之前版本不支持中文字体的英文名称
 * 4. 微软雅黑「\5FAE\8F6F\96C5\9ED1」,中易宋体「\5B8B\4F53」
 */
body,
button, /* 1 */
input, /* 1 */
select, /* 1 */
textarea  /* 1 */
{
    font-family: 'helvetica neue',tahoma,'hiragino sans gb',stheiti,'wenquanyi micro hei',\5FAE\8F6F\96C5\9ED1,\5B8B\4F53,sans-serif;
}
```
中文字体选择如下：
Windows 优先使用「微软雅黑」，如果没有则使用「中易宋体（SimSun）」。
OS X 优先使用「冬青黑体简体（Hiragino Sans GB）」，如果没有则使用默认的「华文黑体」。
Linux 优先使用「文泉驿微米黑」。
西文字体选择如下：
Windows 优先使用「Tahoma」。
OS X 优先使用「Helvetica Neue」