---
title: 深入解析css读书笔记一
date: 2022-06-07 10:13:55
tags: css
---

# Chapter 1. 层叠·优先级·继承

## 层叠
### 1. 样式表的来源：样式是从哪里来的，包括你的样式和浏览器默认样式等。
- 作者样式表 
- 用户代理样式表(浏览器自带)

### 2. 选择器优先级：哪些选择器比另一些选择器更重要。
![](https://s3.bmp.ovh/imgs/2022/06/07/ce80dbac74903d7e.png)

    简单说: id>类>标签  且选择器越多越精准那么优先级就越高.
0,0,0,0  ->  id,class,tag,important  其中important的优先级最高
### 3. 源码顺序：样式在样式表里的声明顺序。
    书写顺序之所以很重要，是因为层叠。优先级相同时，后出现的样式会覆盖先出现的样式

### 两条经验法则
    (1) 在选择器中不要使用ID。就算只用一个ID，也会大幅提升优先级。当需要覆盖这个选择器时，通常找不到另一个有意义的ID，于是就会复制原来的选择器，然后加上另一个类，让它区别于想要覆盖的选择器。
    (2) 不要使用!important。它比ID更难覆盖，一旦用了它，想要覆盖原先的声明，就需要再加上一个!important，而且依然要处理优先级的问题。
    这两条规则是很好的建议，但不必固守它们，因为也有例外。不要为了赢得优先级竞赛而习惯性地使用这两个方法。

## 继承
        如果一个元素的某个属性没有层叠值，则可能会继承某个祖先元素的值。比如通常会给<body>元素加上font-family，里面的所有祖先元素都会继承这个字体，就不必给页面的每个元素明确指定字体了。
    不是所有的属性都能被继承。默认情况下，只有特定的一些属性能被继承，通常是我们希望被继承的那些。它们主要是跟文本相关的属性：color、font、font-family、font-size、font-weight、font-variant、font-style、line-height、letter-spacing、text-align、text-indent、text-transform、white-space以及word-spacing。
        还有一些其他的属性也可以被继承，比如列表属性：list-style、list-style-type、list-style-position以及list-style-image。表格的边框属性border-collapse和border-spacing也能被继承。注意，这些属性控制的是表格的边框行为，而不是常用于指定非表格元素边框的属性。（恐怕没人希望将一个<div>的边框传递到每一个后代元素。）以上为不完全枚举，但是已经很详尽了。
    我们可以在适当的场景使用继承。比如给body元素应用字体，让后代元素继承该字体
![](https://s3.bmp.ovh/imgs/2022/06/07/19db97a13177d8bb.png)

### inherit &&  initial
- inherit =  继承父级元素的该层叠值
- initial =  声明的默认值 如 width = initial = auto

## 简写属性
> 是用于同时给多个属性赋值的属性。比如font是一个简写属性，可以用于设置多种字体属性。它指定了font-style、font-weight、font-size、font-height以及font-family。

    大多数简写属性可以省略一些值，只指定我们关注的值。但是要知道，这样做仍然会设置省略的值，即它们会被隐式地设置为初始值。这会默默覆盖在其他地方定义的样式。比如，如果给网页标题使用简写属性font时，省略font-weight，那么字体粗细就会被设置为normal

### 简写属性的顺序
    简写属性会尽量包容指定的属性值的顺序。可以设置border: 1px solid black或者border: black 1px solid，两者都会生效。这是因为浏览器知道宽度、颜色、边框样式分别对应什么类型的值。
    有些特殊的如 padding margin  记忆口诀 TRouBLe  top ->right ->bottom->left