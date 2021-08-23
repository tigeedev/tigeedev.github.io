---
title: Hexo 博客的常用配置
categories:
  - 充电学习
tags:
  - Hexo
comments: true
date: 2021-02-08 14:56:28
img: https://gitee.com/tigeedev/blog-image/raw/master/img/20210208173741.png
---

## 一、hexo常见命令

### 1.1 新建文章

输入以下命令后会在 `hexo\source\_posts` 目录下生成 `.md` 文件，打开即可直接编辑。当执行 hexo generate 命令时，文章会被编译到 public 目录下，生成静态页面

**新建文章**

```
$ hexo new "postName"
```

**本地预览**

```
hexo clean #清除缓存
hexo s -g #生成静态页面并本地预览
```



### 1.2 文章发布

写完文章，并进行本地预览后，就可以将文章发布到服务器端了

每次部署的三个步骤：

```
hexo clean
hexo generate
hexo deploy
```

命令简写：

```
hexo clean #清除缓存
hexo d -g #生成并上传
```



### 1.3 其他常用命令

```
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server  #启动本地预览
hexo deploy #将目录部署到服务器
hexo help  # 查看帮助 
hexo version  #查看Hexo的版本
```





## 二、hexo 文章格式

> 文章格式可以让文章的信息更完整

### 2.1 hexo 文章常用格式

```
---
title: 文章标题
categories:
  - 文章分类(添加一个即可)
tags:
  - 标签1
  - 标签2
comments: false
date: 2021-02-08 14:56:28
img:
---
```



### 2.2 hexo 文章模板的自定义

每次使用 `hexo new "postName"` 新建一篇文章时，默认只有title、date、tags这几个属性。

我们可以修改 `hexo\scaffolds\post.md` 文件，自定义文章格式的模板，修改后的内容如下：

```css
---
  title: {{ title }}
  date: {{ date }}
  categories: ['分类1','分类2']
  tags: ['标签1','标签2']
  comments: false
  img:
---
```

  

参考文章：[hexo 博客的常见配置](https://www.qianguyihao.com/2020-09-21-hexo-config/) 