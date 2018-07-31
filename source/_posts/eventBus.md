---
title: vue 兄弟组件之间的通讯
date: 2018-05-31 18:09:17
tags: vue
---

- 新建src/bus.js

```
import Vue from 'vue'
var bus = new Vue()
export default bus
```

组件A：
1. 引入文件(注意文件路径)
```
  import bus from '../../bus.js'
```

```
	bus.$emit('avatar', '我是大哥')
```


组件B：
1. 引入文件(注意文件路径)
```
  import bus from '../../bus.js'
```

```
	bus.$on('avatar', (val)=>{
		console.info(val) //我是大哥
	})
```
