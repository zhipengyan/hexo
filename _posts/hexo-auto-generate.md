title: hexo利用github webhooks自动发布文章
date: 2015-05-01 19:32:22
categories: hexo
tags: [hexo,webhooks]
---
>背景：买了vps后本想用wordpress搭个博客环境，但觉得wp太重了，最终选择了hexo静态博客系统。因为有了vps和域名，就不想托管在gitpages上了，不然也不去买vps和域名了。hexo本身是搭建在本地的，新建文章和发布文章都在本地操作，推送到git上面。我是直接搭建在vps上面的，这样就不那么方便了，不能为了写个文章要ssh到vps上编辑，然后再发布吧。折中后我是将hexo的source目录作为git仓库托管在github上，本地用markdown写好文章后，推到github中，然后再远程vps在source目录中拉取文章，再使用vps上的hexo进行hexo generate。这样子看来发个文章也还是蛮拼的，如果本地写好文章推到github上后，能自动发布文章就好了。网络上搜索了一下解决方案，确实可以实现，大多方法是用python监听github发的webhooks请求，然哦胡去执行写好的shell脚本，因为想自己动手，所以就只能使用解决方案，不想用人家的代码，自己实现的才是最好（zuo）的。遂决定使用最近在学习的nodejs，也趁机做个练习，如果可能的话还可以集成到hexo中。

##实现手段
1.使用nodejs监听某个端口
2.hexo文章目录托管在github仓库中，设置webhooks（指向vps地址及1中所说的端口）
3.本地文章推送到远程仓库后，触发webhooks
4.nodejs监听的端口收到webhooks后，执行shell命令，进行hexo generate

##在vps中搭建hexo
估计看到这个文章的同学都是已经在本地或vps中搭建好了hexo的，所以这个搭建过程还是看其他的优秀文章或者看官方doc吧。

##将hexo文章目录托管到github远程仓库
hexo的默认文章目录为source/_posts ，我认为后面有可能还会添加其他东西，索性就把整个source托管到远程仓库了。

##为远程仓库添加webhooks
打开托管hexo文章的github代码仓库页面，右边靠下点击settings，在下个页面中的Webhooks&Services选项中AddWebhoooks，Payload Url为自己vps建立的监听地址，Secret中填写一个密码，这个主要是为了验证是github对Payload Url发出的请求，同时也有密码验证，在监听的时候可以使用该密钥进行验证。否则任何访问该地址都会让你的hexo执行发布，感觉还是不放心。

##为vps编写监听服务
在写代码之前在网上看了下大家的解决方案，大多为使用python监听请求，然后去执行本地的shell脚本。我因为最近在学习nodejs，就想使用nodejs来实现，首先nodejs监听请求肯定是没问题的，问题是怎么去执行终端命令，本想也去写个shell让它来调用执行，后来发现了[shelljs](https://github.com/arturadib/shelljs)这个开源的项目，可以直接调用终端命令，索性就用这个了，也不用去写shell来调用了，直接代码中执行终端命令。我已经将我写好的代码放到github上去了，大家可以git clone直接使用[（我的代码）](https://github.com/zhipengyan/auto-publish-hexo)。写的比较简陋，可以发挥自己的闹洞进行修改完善。
###使用方法
1.
{% codeblock lang:bash %}
cd hexo安装路径
git clone https://github.com/zhipengyan/auto-publish-hexo
cd auto-publish-hexo
npm install
{% endcodeblock %}
2.打开目录下的config.json进行修改
{% codeblock lang:javascript %}
{
     "time_zone": "Asia/Shanghai", //所在时区，在log中显示时间了，vps一般不是本地时区
     "webhook_secret": "your secret", //github webhooks设置的secret
     "nodejs_version": "0.12", //使用的nodejs的版本
     "path": { //如果hexo的配置为默认的话不用修改下面的
       "hexo_path": "../", //hexo目录相对路径
       "hexo_source_path": "../source" //hexo source目录的相对路径，也就是文章目录
     },
     "listen_port": 8888 //监听的端口
}
{% endcodeblock %}
3.使用npm start或者node index.js运行

[（我的代码）](https://github.com/zhipengyan/auto-publish-hexo)