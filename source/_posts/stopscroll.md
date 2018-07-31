---
title: vue 遮罩层阻止默认滚动事件
date: 2018-05-31 18:08:25
tags: vue
---
针对vue项目中的操作：

####vue 遮罩层阻止默认滚动事件

在写移动端页面的时候,弹出遮罩层后，我们仍然可以滚动页面。
vue中提供 @touchmove.prevent 方法可以完美解决这个问题

```
<div class="dialog" @touchmove.prevent ></div>
```

第二种方法：

- 需要引入的jq大法。
- 点击弹出层的click事件时候，添加代码（给html和body添加一个className）

```
$('html').addClass('html-share');
$('body').addClass('body-share');
```

关闭弹出层事件，添加代码（移除这个className）

```
$('html').removeClass('html-share');
$('body').removeClass('body-share');
```


对应的css（这个css才是关键点）
```
.html-share,.body-share {
  overflow: hidden;
  height: 100%;
}
```
