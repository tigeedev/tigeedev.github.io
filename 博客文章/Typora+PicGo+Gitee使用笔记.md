---
title: Typora+PicGo+Gitee使用笔记
categories:
  - 充电学习
tags:
  - Hexo
  - 图床
date: 2021-02-08 14:57:01
img: https://gitee.com/tigeedev/blog-image/raw/master/img/20210209115603.png
---

# 一、前言

之前我的写作方案一直是：**Typora + OneDrive** 。因为这样所有操作都可以在本地进行，没有上传图片的烦恼

但是在博客写作中想要插入一些图片时，就需要将图片上传至图床生成 URL。网上一番探索后，最终挑选出以下几种方案：

1. 阿里云对象存储 [OSS](https://help.aliyun.com/product/31815.html)（一年9块）
2. Github图床 + [jsdelivr](https://www.jsdelivr.com/) 的 CDN 加速。参考文章：[Github+jsDelivr+PicGo 打造稳定快速、高效免费图床](http://www.itrhx.com/2019/08/01/A27-image-hosting/)
3. Gtiee图床（码云）

所以目前我也有了一套比较满意的写作方案： **Typora+ PicGo + Gitee**  。使用Typora编写markdown笔记，Gitee作为图床，PicGo用于自动上传图片。完美~

配置过程顺便做了笔记，留作以后参考。



# 二、本文工具介绍

1. [Gitee](https://gitee.com/) ：国内版的Github，功能跟Github基本一样，而且在国内访问非常快，用作图床再合适不过
2. [PicGo](https://picgo.github.io/PicGo-Doc/) ：一个用于快速上传图片并获取图片 URL 链接的工具，可以关联 Gitee 仓库，上传图片非常方便
3. [Typora](https://www.typora.io/) ：一款优雅的markdown编辑器，所见即所得的方式让人爱不释手。新版的Typora已经支持PicGo ，写作过程中插入图片便可直接上传至 Gitee

Markdown 是一种轻量级标记语言，Github中的帮助文档也是统一使用 Markdown 编写。语法十分简单，十分钟便可入门。推荐学习教程：[献给写作者的 Markdown 新手指南](https://www.jianshu.com/p/q81RER)



# 三、配置 Gitee

## 3.1 新建仓库

登录 gitee ，点击右上角的 + 号，新建仓库

<img src="https://gitee.com/tigeedev/blog-image/raw/master/img/20210208122810.png" alt="image-20210208122809749" style="zoom:80%;" />





## 3.2 新建仓库基本配置

输入仓库名称，选择公开仓库，勾选使用 Readme 文件初始化这个仓库，然后点击 "创建" 即可

![image-20210208124231943](https://gitee.com/tigeedev/blog-image/raw/master/img/20210208153031.png)



## 3.3 生成私人令牌（token）

点击设置-私人令牌-生成新令牌。注意**令牌只会显示一次，要注意保存，后面在 PicGo 中会用到。**如果忘记也可以删除重新生成。

![image-20210208132211648](https://gitee.com/tigeedev/blog-image/raw/master/img/20210208153055.png)



# 四、安装配置 PicGo

## 4.1 安装图床插件

由于 PicGo 本体并不支持 Gitee 图床，所以需要通过第三方图床插件来实现。找到 **gitee-uploader** 插件，安装成功图床中便会出现 gitee 一栏

注意：电脑中必须先安装 [node.js](https://nodejs.org/en/) 才能安装插件，安装完重启即可

![image-20210208133129721](https://gitee.com/tigeedev/blog-image/raw/master/img/20210208153146.png)



## 4.2 配置 gitee 图床

- repo：用户名/仓库名称，比如我自己的仓库 tigeedev/blog-Image
- branch：分支，填 master
- token：填入前面码云的私人令牌，搞丢了可以重新生成
- path：路径，一般写上 img
- customPath：这一项和下一项都不用填

然后点击确定，并设为默认图床

![image-20210208134202618](https://gitee.com/tigeedev/blog-image/raw/master/img/20210208153201.png)



## 4.3 激活PicGo-Server

2.2 版本之后，PicGo内部会默认开启一个小型的服务器，用于配合其他应用来调用PicGo进行上传。

打开 PicGo 设置页面，点击 "设置 Server" ，参考下图进行设置即可。

![image-20210208140449603](https://gitee.com/tigeedev/blog-image/raw/master/img/20210208153252.png)



到这一步，已经可以在 PicGo 中上传图片了。上传成功 PicGo 会有提示，也可以在 Gitee 仓库中查看



# 五、配置 Typora

用 Typora 写作时，如果插入的图片能直接上传到 Gitee 岂不是很方便？所以在 **Typora 0.9.84 及以上版本**已经支持了 PicGo

点击 **文件--偏好设置--图像**，插入图片时选择 "上传图片" ，然后下面选择本地 PicGo 的路径即可

![image-20210208143016808](https://gitee.com/tigeedev/blog-image/raw/master/img/20210208153236.png)



**验证图片上传**

点击 "验证图片上传" ，验证成功会返回如下结果。

![image-20210208143304889](https://gitee.com/tigeedev/blog-image/raw/master/img/20210208153315.png)

至此已经全部设置完成，以后在 Typora 中插入图片时，就可以自动上传到对应图床啦！



# 六、管理图片

**所有上传的图片都可以在 Gitee 仓库中查看， 也可以在 PicGo 的相册中进行管理**

不过可能是插件的原因，对相册中的图片进行的操作都会同步到 Gitee。也就是说**在相册中删除图片时，Gitee中的图片也会同步删除**，所以一定注意不要误删。

![image-20210208135110662](https://gitee.com/tigeedev/blog-image/raw/master/img/20210208221228.png)