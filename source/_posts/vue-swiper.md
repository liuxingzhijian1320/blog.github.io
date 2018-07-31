---
title: vue+swiper实现组件化开发
date: 2018-05-31 18:19:26
tags: vue plugins
---
1. swiper的组件

```
<template>
    <div class="swiper-container">
        <div class="swiper-wrapper">
            <div class="swiper-slide" v-for="item in swiper"><img :src="item.room_src" alt=""></div>
            <!--<div class="swiper-slide" v-for="item in test"><img :src="item.room_src" alt=""></div>-->
        </div>
    </div>
</template>
<script>
  import Swiper from 'swiper'

  export default {
    name: 'swiper',
    data() {
      return {
        mySwiper: null,
//        test: [
//          "https://rpic.douyucdn.cn/acrpic/171024/288016_0921.jpg",
//          "https://rpic.douyucdn.cn/acrpic/171024/748396_0924.jpg",
//          "https://rpic.douyucdn.cn/acrpic/171024/453751_0922.jpg",
//          "https://rpic.douyucdn.cn/acrpic/171024/79663_0920.jpg"
//        ]
      }
    },
    props: ['swiper'],  //swiper的就是test这个数据传递来的
    methods: {
      _initSwiper() {
        this.mySwiper = new Swiper('.swiper-container', {
          autoplay: 5000,//可选选项，自动滑动
        })
      },
      _updateSwiper() {
        this.$nextTick(() => {
          this.mySwiper.update(true);  //swiper update的方法
        })
      },
      swiperUpdate() {
        if (this.mySwiper) { //节点存在
          this._updateSwiper(); //更新
        } else {
          this._initSwiper(); //创建
        }
      },
    },

    watch: {
      //通过props传来的数据 和 组件一加载节点就创建成功 二者不是同步，实时监听的swiper(传递的值)的变化
      swiper() {
        this.swiperUpdate();
      }
    },
    mounted() {
      this.swiperUpdate(); //页面一加载拉去数据创建节点
    }
  }
</script>
<style lang="scss" scoped>
    .swiper-container {
        width: 100%;
        height: 4rem;
        margin-top: 0.9rem;
        .swiper-wrapper {
            width: 100%;
            height: 100%;
            .swiper-slide {
                background-size: cover;
                width: 100%;
                height: 4rem;
                img {
                    width: 100%;
                    height: 100%;
                }
            }
        }
    }


</style>

```

2. home.vue 调用的组件方法

//html

```
    <swiper :swiper="roomList.slice(6,10)" ></swiper>
```
//js

```
  import swiper from 'components/swiper/swiper'

 components: {
      swiper
    },
```


问题：如果单纯的调用_initSwiper的方法，会发现页面是不能滚动的，但是页面随便修改东西，然后保存的swiper又可以滚动的，这个个原因是初始swiper的节点没有创建成功，值页面有穿进去的，一层一层的可以打印swiper的值为空的，当修改东西值就能传递进去的，所以的这里的我们需要通过判断节点是否成功来update siwper的方法
