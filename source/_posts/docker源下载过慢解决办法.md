---
title: docker源下载过慢解决办法
tags: 教程
categories: Linux
thumbnail: "https://pic.imgdb.cn/item/663c472f0ea9cb1403e4c285.png"
---

# 首先换源

换完源以后还是不能的下载的话参考下面的教程

# DNS的修改

通常我们知道，修改dns的几个途径

- /etc/resolv.conf
- /etc/netplan/01-netcfg.yaml

修改上面两个文件，一般情况下，可以解决，但是在一次使用新安装的ubuntu22.04的时候，发现，无论怎么修改，dig解析域名都是往127.0.0.53发送，哪怕在缓存中的已经生效

在Docker容器拉取的过程中会发现无法进行容器的拉取，我们可以采用的方法就是修改DNS服务器

首先查看DNS服务器是什么

~~~bash
cat /etc/resolv.conf
#直接进行编辑即可
vim /etc/resolv.conf
#只需要更改nameserver中对应的DNS服务器地址即可
~~~

修改完对应的DNS服务器重启服务器即可

~~~bash
reboot
~~~

