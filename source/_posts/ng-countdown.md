---
title: angular 验证码倒计时60秒
date: 2018-05-31 18:05:57
tags: angular
---

HTML
```
<div class="form-group message-box form-style">
        <input class="form-control" type="text" id="" name="phone_code" ng-model="vm.user.phone_code" autocomplete="off" placeholder="验证码" required>
	    <button class="btn"  type="button" ng-click="vm.sendMessage()" ng-bind="paracont"  ng-disabled="vm.disabledClick"></button>
        <div class="m-t-xs text-left forget-text" ng-show="my_form.phone_code.$invalid && my_form.$submitted">
	        <small class="text-danger" ng-show="my_form.phone_code.$error.required">验证码</small>
        </div>
</div>
```
JS

```
$scope.paracont = "获取验证码";
vm.disabledClick = false;
vm.sendMessage = function(){
   var second = 60,
    timePromise = $interval(function(){
        vm.disabledClick = true;
        if(second <= 0){
            $interval.cancel(timePromise);
            second = 60;
        }else{
            second--;
            $scope.paracont = second + "秒后可重发";
            if(second == 0){
                $scope.paracont = "重发验证码";
                vm.disabledClick = false;
            }
        }
    },1000,60);
}
```


解释：angular中scope上面绑定的东西很多，一旦做复杂的和用插件的，插件的也是绑在scope，造成内存污染
这里的解决的办法就是猫在控制器里面的添加代码,如下

```
 $scope.vm={};
 var vm=$scope.vm;
```

在每个控制器的都添加，所有的操作都是以vm打头，将作用域绑定在vm上面


