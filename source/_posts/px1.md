---
title: 1px的解决方案
date: 2018-05-31 17:54:04
tags: css
---
1px在ios上面看的非常粗的，基本就是2px的效果，但是android显示的却是真是的1px的效果。
目前项目中频率最高的解决方案有2种。
1. 使用伪类的方案

```
<div class="one-border-after"></div>

 .one-border-after {
     position: relative;
  }
  .one-border-after:after {
     position: absolute;
     content: '';
     display: block;
     left: 20px;
     right: 20px;
     top: 100px;
     height: 1px;
     background-color: #000;
     transform: scaleY(0.5);
  }
```

2. box-shadow的方案

```
<div class="one-border"></div>

 height: 1px;
 background: none;
 box-shadow: 0 0.5px 0 #000;

```

建议使用的第一种只增加css代码，不会增加节点出来
