---
title: 微信小程序部分手机无法拨打电话的解决的方案
date: 2018-05-31 18:21:17
tags: miniprogram
---
其他的代码省略，直接上js的代码

```
 wx.makePhoneCall({
        phoneNumber: message,
        success(){
          console.log("拨打电话成功！")
        },
        fail(err){
          console.log("222！",err)
          //不能拨打电话，直接直接打印出err和能拨打电话的的取消按钮的err是不一样的
          //wx.showModal({
            //title: '联系电话',
            //content:err,
            //showCancel:false
          //})

          if(err.errMsg == 'makePhoneCall:fail'){
            wx.showModal({
              title: '联系电话',
              content:message,
              showCancel:false
            })
          }
        }
      })

```

- 能拨打电话直接拨打，不能拨打电话就直接的给出一个提示框（没有拨打电话的功能，只是展示的作用的）
