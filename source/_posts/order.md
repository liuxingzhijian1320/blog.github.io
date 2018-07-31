---
title: 一行命令
date: 2018-05-30 23:00:25
tags: config
---

### 原始命令

``` bash

  hexo new '文章名称'

  hexo clean

  hexo g

  hexo d

```

### 一行命令的配置
打开 `package.json` 的文件

```bash

    "scripts": {
        "build": "hexo clean && hexo g && hexo d"
    },

```

执行操作

``` bash

  npm run build
```

