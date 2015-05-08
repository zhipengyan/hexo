title: hexo利用github webhooks自动发布文章
date: 2015-05-01 19:32:22
categories: hexo
tags: [hexo,webhooks]
---
>背景：买了vps后本想用wordpress搭个博客环境，但觉得wp太重了，最终选择了hexo静态博客系统。因为有了vps和域名，就不想托管在gitpages上了，不然也不去买vps和域名了。hexo本身是搭建在本地的，新建文章和发布文章都在本地操作，推送到git上面。我是直接搭建在vps上面的，这样就不那么方便了，不能为了写个文章要ssh到vps上编辑，然后再发布吧。折中后我是将hexo的source目录作为git仓库托管在github上，本地用markdown写好文章后，推到github中，然后再远程vps在source目录中拉取文章，再使用vps上的hexo进行hexo generate。这样子看来发个文章也还是蛮拼的，如果本地写好文章推到github上后，能自动发布文章就好了。网络上搜索了一下解决方案，确实可以实现，大多方法是用python监听github发的webhooks请求，然哦胡去执行写好的shell脚本，因为想自己动手，所以就只能使用解决方案，不想用人家的代码，自己实现的才是最好（zuo）的。遂决定使用最近在学习的nodejs，也趁机做个练习，如果可能的话还可以集成到hexo中。

##一、实现手段
1.使用nodejs监听某个端口
2.hexo文章目录托管在github仓库中，设置webhooks（指向vps地址及1中所说的端口）
3.本地文章推送到远程仓库后，触发webhooks
4.nodejs监听的端口收到webhooks后，执行shell命令，进行hexo generate

##一、在vps中搭建hexo
估计看到这个文章的同学都是已经在本地或vps中搭建好了hexo的，所以这个搭建过程还是看其他的优秀文章或者看官方doc吧。

##二、将hexo文章目录托管到github远程仓库
hexo的默认文章目录为source/_posts ，我认为后面有可能还会添加其他东西，索性就把整个source托管到远程仓库了。

##三、为远程仓库添加webhooks
太困了，先睡觉吧，后面接着写。。.


