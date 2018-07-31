---
title: vue 验证码倒计时60s
date: 2018-05-31 18:04:47
tags: vue
---
```
 <div class="input-div" v-show="formData.phone">
	 <input type="text" class="input code" name="code" v-model.trim="formData.code" placeholder="验证码">
     <button @click="getCode(formData)" class="code-btn" :disabled="!show">
         <span v-show="show">获取验证码</span>
         <span v-show="!show" class="count">{{count}} s</span>
     </button>
</div>
```

```
const TIME_COUNT = 60;
 data(){
      return {
        formData: {
          phone:'',
          code:'',
        },
        show: true,
        count: '',
        timer: null,
      }
    },

	methods:{
		getCode(formData){
		    if (!this.timer) {
	            this.count = TIME_COUNT;
	            this.show = false;
	            this.timer = setInterval(() => {
	              if (this.count > 0 && this.count <= TIME_COUNT) {
	                this.count--;
	              } else {
	                this.show = true;
	                clearInterval(this.timer);
	                this.timer = null;
	              }
	            }, 1000)
	          }
		}
	}


```
