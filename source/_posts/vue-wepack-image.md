---
title: webpack，vue，图片(懒加载)之间关系
date: 2018-05-31 18:13:28
tags: vue
---
以vue来解释

- 例子1 (获取的背景图)
```
<div v-for='item,index in list'>
	<div class='demo' :style="{backgroundImage:`url(${item.cover})`}" ></div>
</div>
```

- 例子2 （获取的图片）

```
<div v-for='item,index in list'>
	<img :src="item.cover">
</div>
```

- 例子3 （本地的图片的）

```
<div v-for='item,index in new Array(5)'>
	<img :src="`${require(`src/assets/images/img-${index+1}.png`)}`">
</div>
```

- 例子4 （本地的背景图）

```
<div v-for='item,index in new Array(5)'>
	<div class="img-kinds" :style="{backgroundImage:`url(${require(`./images/img-${index}@2x.png`)})`}"></div>
</div>
```

- [懒加载文档](https://www.npmjs.com/package/vue-lazyload)
//main.js
```
npm install  vue-lazyload -D
```
```
import VueLazyload from 'vue-lazyload'
```
```
Vue.use(VueLazyload, {
  preLoad: 1.3,
  error: require('src/assets/fileloaderassets/lazy-image.jpg'),
  loading: require('src/assets/fileloaderassets/lazy-image.jpg'),
  attempt: 1
})

```
```
<div class=avatar v-lazy:background-image="`${item.cover}`"></div>
```
```
<img v-lazy='item.avatar'  />
```
