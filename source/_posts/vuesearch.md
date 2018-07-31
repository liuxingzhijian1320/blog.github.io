---
title: VUE 实现边输入便搜索
date: 2018-05-30 22:52:21
tags: vue
---



搜索分类2种情况，一般的是当用户输入完，点击确定的按钮在向后发送请求，还有一种就是的我一边输入，一边向后台发送请求，但是会产生一个性能的问题，就是一直发请求造成页面的卡顿，这里就是使用截流函数,当用户每次点击键盘之间超过300ms就发送请求，否则不请求


## Quick Start



### search.vue

``` bash
<template>
  <div id="search">
    <input type="text" class="search" placeholder="搜索" v-model.trim="title" />
  </div>
</template>
```

``` bash
<script>
// 节流函数
const delay = (function() {
  let timer = 0;
  return function(callback, ms) {
    clearTimeout(timer);
    timer = setTimeout(callback, ms);
  };
})();
export default {
  name: 'search',
  data() {
    return {
      title: '',
      search:[]
    };
  },
  watch: {
  //watch title change
    title() {
      delay(() => {
        this.fetchData();
      }, 300);
    },
  },
  methods: {
    async fetchData(val) {
      const res = await this.fetch({
        url: '写上你的URL',
        method: 'GET',
        params: { title: this.title },
      });
      this.search = res.data.list;
    },
  },
  mounted() {},
};
</script>
```

More info: [vue 实现边输入边搜索功能](https://mp.csdn.net/mdeditor/78933252)
