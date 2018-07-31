---
title: 多条件和模糊搜索
date: 2018-07-11 16:33:16
tags:
---

- html

```
<div class="content">
    <div class="right">

      <select name="sex" width='100' v-model="formData.sex">
        <option value="" selected>请选择</option>
        <option value="1">男</option>
        <option value="2">女</option>
        <option value="3">不是人</option>
      </select>

      <input type="text" v-model="formData.phone" placeholder="电话(精准搜索)">

      <input type="text" v-model="formData.name" placeholder="姓名(模糊搜索)">

      <button @click="search(formData)">提交数据</button>
    </div>
    <div class="left">
      <ul>
        <li v-for="(item,index) in  realList" :key="index">
          {{item.name}} || {{item.phone}} || {{item.sex | filterSex}}
        </li>
      </ul>
    </div>
  </div>

```

- js

```
export default {
  name: 'styleTest',
  data() {
    return {
      formData: {
        name: '',
        phone: '',
        sex: '',
      },
      realList: [],
      list: [
        {
          name: '张址',
          phone: 18715023011,
          sex: 1,
        },
        {
          name: '张三',
          phone: 18715023012,
          sex: 2,
        },
        {
          name: '李四',
          phone: 18715023013,
          sex: 1,
        },
        {
          name: '赵武',
          phone: 18715023014,
          sex: 2,
        },
        {
          name: '晋南',
          phone: 18715023015,
          sex: 1,
        },
        {
          name: '张东',
          phone: 18715023016,
          sex: 2,
        },
      ],
    };
  },
  filters: {
    filterSex(val) {
      switch (val) {
        case 1:
          return '男';
          break;
        case 2:
          return '女';
          break;
        case 3:
          return '不是人';
          break;
        default:
          return '男';
      }
    },
  },
  computed: {
    // realList() {
    //   let { name, phone, sex } = this.formData;
    //   if (name && phone && sex) {
    //     return this.list;
    //   }
    // },
  },
  created() {
    this.search({});
  },
  methods: {
    search({ name, phone, sex }) {
      this.realList = this.list.filter(item => {
        let matchName = true; // 姓名 筛选
        let matchSex = true; // 性别 筛选
        let matchPhone = true; // 号码 筛选

        if (sex) {
          matchSex = item.sex == sex;
        }

        if (phone) {
          // console.info(Object.prototype.toString.call(phone));
          matchPhone = item.phone == phone;
        }

        if (name) {
          // 模糊搜索;
          const keys = name
            .toUpperCase() // 转大写
            .replace(' ', '') // 删掉空格
            .split(''); // 切割成 单个字

          matchName = keys.every(key => item.name.toUpperCase().includes(key));
        }
        return matchName && matchPhone && matchSex;
      });
    },
  },
};

```
