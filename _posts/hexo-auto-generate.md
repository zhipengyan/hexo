title: hexo利用github webhooks自动发布文章
date: 2015-05-01 19:32:22
categories: hexo
tags: [hexo,webhooks]
---
>背景：买了vps后本想用wordpress搭个博客环境，但觉得wp太重了，最终选择了hexo静态博客系统。因为有了vps和域名，就不想托管在gitpages上了，不然也不去买vps和域名了。hexo本身是搭建在本地的，新建文章和发布文章都在本地操作，推送到git上面。我是直接搭建在vps上面的，这样就不那么方便了，不能为了写个文章要ssh到vps上编辑，然后再发布吧。折中后我是将hexo的source目录作为git仓库托管在github上，本地用markdown写好文章后，推到github中，然后再远程vps在source目录中拉去文章，再使用vps上的hexo进行hexo generate。这样子看来发个文章也还是蛮拼的，如果本地写好文章推到github上后，能自动发布文章就好了。网络上搜索了一下解决方案，确实可以实现，大多方法是用python去执行写好的shell脚本，因为想自己动手，所以就只能使用解决方案，不想用人家的代码，自己实现的才是最好（zuo）的。遂决定使用最近在学习的nodejs，趁机做个练习吧。

