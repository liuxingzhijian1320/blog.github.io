---
title: jq 文字上下滚动
date: 2018-05-31 18:20:37
tags: jquery
---
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>文字上下滚动轮播</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .lunbo {
            position: relative;
            width: 600px;
            height: 50px;
            border: 1px solid red;
            overflow: hidden;
        }

        ul {
            position: absolute;
            left: 0;
            top: 0;
            width: 600px;
            height: auto;
        }

        ul li {
            width: 600px;
            height: 50px;
            line-height: 50px;
            font-size: 20px;
            color: #333;
            text-align: center
        }
    </style>
</head>
<body>
<div>

		<ul class='lunbo'>
			<li>werw</li>
			<li>werw</li>
			<li>werw</li>
			<li>werw</li>
			<li>werw</li>
			<li>werw</li>
			<li>werw</li>
			<li>werw</li>
			<li>werw</li>
		</ul>
</div>
<script src="https://cdn.bootcss.com/jquery/2.2.2/jquery.js"></script>
<script>
  function lunbo(id, height) {
    var ul = $(id);
    var liFirst = ul.find('li:first');
    $(id).animate({ top: height }).animate({ "top": 0 }, 0, function () {
      var clone = liFirst.clone();
      $(id).append(clone);
      liFirst.remove();
    })
  }

  setInterval("lunbo('ul','-50px')", 1000)
</script>
</body>
</html>
```
