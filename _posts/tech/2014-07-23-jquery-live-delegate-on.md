--- 
layout: post
title: jQuery中live，delegate，on的区别 
description: live和delegate都是由on实现的
category: tech
---
## on
on方法是一个很灵活的事件绑定方法，既可以绑定一个事件到某个dom上，也可以以事件冒泡的形式
绑定事件。具体使用方法，参见Goolge。

## live

live就是将绑定的事件以冒泡的形式绑定到document，是的，用live绑定所有时间都绑定到document
对象上。用on来模拟live就是这个样子：

```
    //live
    $('#id a').live('click', function(){})
    //on
    $(document).on('click', '#id a',function(){})
```
所有live绑定的事件，都放到document显然不妥，jQuery1.9 之后版本已经废弃这个方法了。

## delegate

delegate方法是将绑定的事件以冒泡的形式绑定到指定的父元素上。用on实现就是这个样子：

```
    //delegate
    $('#id').delegate('a','click',function(){})
    //on
    $('#id').on('click','a',function(){})
```
