---
title: Nginx在同一个域名下配置多个项目
categories:
  - 充电学习
tags:
  - 服务器
  - nginx
comments: false
date: 2021-08-20 19:39:49
---

## 前言

服务器可以部署多个项目，在只有一个域名的情况下，可以给不同的项目分配不同的二级域名来进行访问。

## 配置过程

### 1. 添加二级域名

- 添加A记录到主机
- 同一个域名可以解析出N个二级域名

<img src="https://tigeedev.oss-cn-hangzhou.aliyuncs.com/img/20210820184102.png" alt="image-20210820184059426" style="zoom:80%;" />

### 2. 配置nginx

- nginx 中另添加一个 `server` 
- 修改后重启nginx
  - 先使用 `nginx -t` 测试语法是否正确
  - 使用命令 `nginx -s reload` 重新加载配置文件

```
    # hexo博客
    #
    server {
        listen       80;
        server_name  www.tigeedev.com;

        location / {
            root   /var/hexo;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

    # 商城项目
    #
    server {
        listen       80;
        server_name  shop.tigeedev.com;

        location / {
            root   /var/mall;
            index  index.html index.htm;
            try_files $uri $uri/ /index.html; #使用history模式进行路由
        }
    }
```

## 参考文章

- [Nginx同一个域名配置多个项目](https://blog.csdn.net/cc_want/article/details/83780435)

