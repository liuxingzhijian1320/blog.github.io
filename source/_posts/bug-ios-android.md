---
title: 解决安卓的input的弹出的软键盘遮住文本
date: 2018-05-31 18:07:15
tags: bug
---
ios的软键盘弹出会把整个文本区域抵上来，但是安卓会覆盖部分的文本，很不友好的
先上效果图：
安卓：
![这里写图片描述](bug-ios-android/1.png)

实现的方法就是display：flex的实现，如果有表单，千万不要使用的position的方法，这样安卓肯定会挂掉。

形式一：外部一个container 里面有个content，但是content是绝对居中的，第一反应是position，但是有表单的话，就要放弃这种方法。

**注：有表单就该使用 flex的方法**
```
.container {
	display: flex;
    align-items: center;
    justify-content: center;
}
.content {
	width:100px;
	height:100px;
}
```

形式二：

```
 <article id="h5applyvip">
    <header class="header"></header>
    <div class="content">
      <form class="form">
        <input type="text" class="input" name="name" v-model.trim = "formData.name">
        <input type="text" class="input" name="name" v-model.trim = "formData.name" >
        <input type="text" class="input" name="name" v-model.trim = "formData.name" >
        <input type="text" class="input" name="name" v-model.trim = "formData.name" >
      </form>
    </div>
    <footer class="footer"  @click="openClick(formData)">   <!--立即开通-->
      <img src="./images/open-btn@2x.png" alt="" class="open-btn">
    </footer>
  </article>
```

```
 #h5applyvip {
    width: 100%;
    min-height: 100vh;   //撑满整个屏幕
    display: flex;
    flex-direction: column;  //竖向排列
    .header {
      width: 7.5rem;
      height: 3.1rem;  //头部的定死高度
    }
    .content {
      flex: 1;    //content是撑满
      width: 100%;
    }
    .footer {
      height: 1.1rem;  //脚部的定死高度
      width:100%;
    }
  }
```

上面的这种方法 可以实现另外一中的效果 （sticky footer）


参考资料：
http://caniuse.com/#search=flex-direction”
http://www.runoob.com/w3cnote/flex-grammar.html
