---
title: 滚动到某个区域实现动画
date: 2018-07-09 11:47:15
tags:
---

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>滚动到某个区域实现动画</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    .header {
        height: 1000px;
        background: red;
        width: 100%;
        opacity: 0.2;
    }

    .footer {
        height: 200px;
        background: gray;
    }

    .animated {
        background: red;
        transition: all 1s linear;
    }
</style>

<body>
    <header class="header"></header>
    <footer class="footer" id="footer"></footer>
</body>
<script>
    (function() {
        var footerDiv = document.getElementById("footer");
        var footerHeight = footerDiv.offsetHeight;
        window.addEventListener('scroll', () => {
          // 兼容的写法
            var scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;
            console.info('文档高度' + document.body.offsetHeight, scrollTop, window.innerHeight)
                //判断是否滚动到底部
            if (scrollTop + window.innerHeight + 0 + footerHeight >= document.body.offsetHeight) { //0 表示距离底部多少的距离的开始触发loadmore效果
                console.info('我要开始做动画片来')
                footerDiv.classList.add("animated");
            } else {
                footerDiv.classList.remove("animated");
            }
        });
    })()
</script>

</html>
```

> classList [MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/classList)
> scrollTop 的兼容写法 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollTop)
[can i use] (https://caniuse.com/#search=classList)
