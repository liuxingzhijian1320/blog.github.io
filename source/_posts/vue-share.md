---
title: vue 微信分享的实现
date: 2018-05-31 18:11:54
tags: vue
---
1. 新建 assets/script/wecaht.share.js

```


function getScript() {
  return new Promise((resolve, reject) => {

    $.ajax({
      url: 'https://res.wx.qq.com/open/js/jweixin-1.0.0.js',
      dataType: "script",
      cache : true,
    }).done(function() {
      resolve(window.wx)
    })
    .fail(function(error) {
      reject( error );
    });

  })
}

function act() {
  return new Promise((resolve, reject) => {
    // console.log(window.location.href)
    $.ajax({
      url: 'http://wechat.demo.com/token/getWechat',//后台索要的算法签名
      // type: 'get',
      dataType: 'jsonp',
      data: {
        url: encodeURIComponent(window.location.href.split('#')[0]),
      },
    }).done(function(ret) {
      resolve(ret)
    }).fail(function(ret) {
        reject( ret );
      })
  })
}



export function wechatShare(shareDate) {
  return new Promise(async function(resolve, reject) {

    try{
      let isWechat=navigator.userAgent.indexOf('MicroMessenger')>-1 //判断为微信浏览器
      if(!isWechat){
        return resolve('not weichat')
      }
      if(!window.wx){
        await getScript();
      }


      var defaultData = {
        title: `分享的标题`,
        content: `内容`,
        link: `${window.location.href}`,
        logo: `${require('../images/share.png')}`, //分享出来的图片的
        success: function (res) {

        },
      }
      let data = { ...defaultData, ...shareDate }
      let ret = await act()
      wx.config($.extend({
        // debug:1,
        jsApiList: ['onMenuShareAppMessage', 'onMenuShareTimeline'],
      }, ret))

      wx.ready(function () {
        wx.onMenuShareTimeline({
          title: data.content,
          desc: '',
          link: data.link,
          imgUrl: data.logo,
          dataUrl: '',
          success: data.success,
          cancel: function () {},
        })
        wx.onMenuShareAppMessage({
          title: data.title,
          desc: data.content,
          link: data.link,
          imgUrl: data.logo,
          dataUrl: '',
          success: data.success,
          cancel: function () {},
        })
        wx.onMenuShareQQ({
          title: data.title,
          desc: data.content,
          link: data.link,
          imgUrl: data.logo,
          dataUrl: '',
          success: data.success,
          cancel: function () {},
        })
      })

    }catch(error){
      reject( error );
    }
  })

}

```

2.  main.js

```
import { wechatShare } from 'src/assets/scripts/wechat.share'; //这里我脚手架配置过Alias，没有配过可直接相对路径来寻找
window.wechatShare  = wechatShare
```
3. 每个组件的调用方法

```
wechatShare({
	title: '组件的标题',
	 content: '内容',
	 link: `${window.location.origin}/user/collegeIndex`,
	 logo: `${require('src/assets/images/share.png')}`,
	});
```
