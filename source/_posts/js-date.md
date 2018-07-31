---
title: JS 根据今天的日期获取本周星期一与星期天的日期
date: 2018-05-31 18:02:29
tags: js
---
```
var now = new Date();
var nowTime = now.getTime() ;
var day = now.getDay();
var oneDayTime = 24*60*60*1000 ;
```
显示周一
```
var MondayTime = nowTime - (day-1)*oneDayTime ;
```
显示周日
```
var SundayTime =  nowTime + (7-day)*oneDayTime ;
```

初始化日期时间
```
var monday = new Date(MondayTime);
var sunday = new Date(SundayTime);
```


打印查看结果
```
console.log(monday) ;
console.log(sunday) ;
```




2.js 根据日期的方法获取当前这一周的周一（或者其他）

这是封装好的函数 直接调用，回调的返回周一的时间的 注意转化日期的格式
```
function getFirstDayOfWeek (date) {
    var day = date.getDay() || 7;
    return new Date(date.getFullYear(), date.getMonth(), date.getDate() + 1 - day);
};
```
