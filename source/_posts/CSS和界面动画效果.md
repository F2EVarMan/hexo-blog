title: CSS和界面动画效果
date: 2015-03-02 14:20:18
tags: 
- CSS
- 动画效果
categories:
- CSS
---
### CSS和界面动画效果
目前主流的动画实现方式
- JQuery Animate(setInterval) : 容易使用,兼容性好,低效.
- CSS Transition :硬件加速,移动端兼容,高效.
- requestAnimationFrame : 易用,充分发挥浏览器性能

影响动画的效果因素
浏览器的渲染方式: Layout -> Paint ->Composite
- 频繁重绘,改变颜色、背景图等.
- 频繁触发Layout导致回流,改变位置影响文档流.
Link:[csstriggers](http://csstriggers.com/)

为什么不使用$.animate()
JQuery无法解决频繁触发Layout导致的抽动
```{bash}
var h1=element1.clientHeight;//red
element1.style.height=(h1 * 2) +'px';//write

var h2=element2.clientHeight;
element2.style.height=(h2 * 2)+'px';

var h3=element3.clientHeight;
element3.style.height=(h3 * 2)+'px';

```
$.animate()方法基于setInterval，容易导致堆积回调，最终导致跳帧.

既然硬件加速这么厉害,为什么不这样?
```{bash}
*,*:before,*:after{
	transform:translate3d(0,0,0);
	}
```
- 不是所有的CSS属性都能获得GPU加速
- GPU传输的开销，Webkit需要手动触发
- Firefox/IE为所有动画都采取硬件加速
- will-change 属性

CSS3动画的注意事项
- ::before &  ::after
- CSS transition对translate/scale/rotate 缺乏独立的控制
- CSS animation 的动画曲线会应用到所有变化属性上
- 手写稍微复杂点的 keyframes像噩梦
- API :$elm.on('transitioned',function(){})
  $elm.on('animationstart',function(){})

  JQuery 动画 !=JS 动画
  按时间变化 -> 按每帧变化