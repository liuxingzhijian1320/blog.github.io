---
title: 教你在微信中给Vue单页应用设置标题
date: 2018-05-31 18:12:26
tags: vue
---

原因：
1. 设置title，解决微信改不了title的bug
2. 可以给每个页面设置标题
实现的方法如下，新建文件
assets/script/settiltle.js

```
/**
 1. 设置title，解决微信改不了title的bug
 */
export default function setTitle(title) {
  document.title = title;
  let userAgent = window.navigator.userAgent.toLowerCase();
  let isiOS = userAgent.indexOf('applewebkit') >= 0;
  let isWechat = userAgent.indexOf('micromessenger') >= 0;
  if (isiOS && isWechat) {
    let iframe = document.createElement('iframe');
    iframe.src = 'https://www.baidu.com/favicon.ico';
    iframe.style.display = 'none';
    document.body.appendChild(iframe);
    iframe.onload = function() {
      setTimeout(function() {
        iframe.remove();
      }, 0)
    }
  }
}
```

// main.js
 先引入的settitle的js的文件

```
import setTitle from '../assets/script/settitle.js'; // 设置页面标题
window.setTitle = setTitle //挂在window的上面。全局可直接使用的额
```
有俩中实现的方法来修改title的
一：既然上面的已经挂在的window的上面了，每个组件就可以在在mounted,created,activated等钩子中设置title的

```
setTitle（'我是标题'）
```

二：监听的路由的变化的，对页面的titile进行实时的更改的
对路由稍作修改如下

```
const router = new Router({
	 routes: [
	     {
	      path: '/solution/andiosfixed',
	      name: 'andiosfixed',
	      meta: {
	        title: 'ios对fixed兼容', //重点在meta的这里，其他的都是例子的
	      },
	      component: AndIosFixed
	    } ]
    }）
```
[vue-router meta的介绍](https://router.vuejs.org/zh-cn/advanced/meta.html)   <===
```
// 路由变化
router.afterEach(function (to) {
  if (to.meta && to.meta.title) {
    //console.info(to.meta.title)
    setTitle(to.meta.title);
  }
})

export default router;
```
[vue-router afterEach的介绍](https://router.vuejs.org/zh-cn/advanced/navigation-guards.html)

以上的2中方法可以实现的安卓和ios的微信修改title的方法，如您有更好的建议和意见请留言，谢谢支持。

