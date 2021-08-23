---
title: SSH 无法连接 CentOS
categories:
  - 充电学习
tags:
  - ssh
date: 2021-03-11 20:56:49
img:
---



# 问题描述

服务器是阿里云，CentOS 7.3

今天刚完成备案，刚想接着折腾，结果发现 ssh 远程连接一直提示 Connection timed out（ping没问题）

**日志详情**

```xaml
$ ssh -v git@公网 IP
OpenSSH_8.4p1, OpenSSL 1.1.1i  8 Dec 2020
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Connecting to IP [IP] port 22.
debug1: connect to address IP port 22: Connection timed out

ssh: connect to host IP port 22: Connection timed out
```

**端口情况**

```
# sudo netstat -plnt

Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address    Foreign Address     State    PID/Program name    
tcp        0      0 0.0.0.0:80       0.0.0.0:*           LISTEN   2334/nginx: master  
tcp        0      0 0.0.0.0:22       0.0.0.0:*           LISTEN   2055/sshd
```



# 解决方法

连接不上可能是由于网络环境导致。之前 SSH 一直都正常连接，到学校才发现会 time out。所以校园网很可能是那个罪魁祸首

...

果不其然，用手机的 4G 开个热点就可以正常连接了。一点小问题折腾了一下午...草（一种植物）



# 参考链接

- [Linux Ubuntu 无法连接 ssh connect to host port 22: Connection timed out](https://ruby-china.org/topics/37035) 
- [校园网手机ssh连接vm虚拟机linux教程](https://blog.csdn.net/weixin_40943540/article/details/83108806?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_utm_term-1&spm=1001.2101.3001.4242)

