title: DIV垂直居中的方法
date: 2015-03-19 20:11:34
categories: 前端
tags: [HTML,CSS]
---
>因为想做前端，目前手中的工作渐渐地越离越远，尝试着去做了一次面试。虽然在面试之前也是早起晚睡地准备了好几天，但毕竟没有太多的实战经验，遇到的一些面试题很熟悉，但是就是说不出来，平时工作是遇到问题就查资料，做完了也没有记住。所以还是要积累一下，把知道的讲出来才是真的知道！

言归正传我们来了解一下这道题目的几种解法
>我实现的[例子](http://sunnyyan.com:8080/lab/post/div-vertical-center.html)

##使用表格样式解决
将外部容器的display属性设置为table-cell，并设置其属性vertical-align：middle;
{% codeblock lang:CSS %}
.outerdiv {
    width: 100px;
    height: 100px;
    outline: sloid 1px red;
    display: table-cell;
    vertical-align: middle;
}
.innerdiv{
    width: 30px;
    height: 30px;
    outline: sloid 1px green;
}
{% endcodeblock %}
{% codeblock lang:HTML %}
<div class="outerdiv">
    <div class="innerdiv">
    </div>
</div>
{% endcodeblock %}

##使用绝对定位的DIV
要居中的div的postion设置为absolute，然后top设置为50%，但这个时候仅仅顶边是处于中间的位置，所以要让自身再往上偏离自身高度的一般，这里给margin-top一个负值。还有一个需要注意的是外部div的display默认为static，这个时候其内部的div的postion是相对外部最近的一个容器的，不一定是第一个外部的div，要给outerdiv的postion设置一个值，根据其所处的场景来定。
{% codeblock lang:CSS %}
.outerdiv {
    width: 100px;
    height: 100px;
    outline: sloid 1px red;
    position: relative;
}
.innerdiv{
    position: absolute;
    top: 50%;
    margin-top: -30px;
    outline: sloid 1px green;
}
{% endcodeblock %}
{% codeblock lang:HTML %}
<div class="outerdiv">
    <div class="innerdiv">
    </div>
</div>
{% endcodeblock %}

##插入一个DIV做填补
其实思路是在上方或下方插入div进行占位，当然就是占一半50%咯，这样需要居中的div的顶边或者底边刚好停在中线上，然后占位的div做一个负margin，偏移量就是自身高度的一半，让自己上去或者下来一般就ok了。这里我们就在上方进行插入一个空div来占位，下方的话一样的，自己看着来就行。
{% codeblock lang:CSS %}
.outerdiv {
    width: 100px;
    height: 100px;
    outline: sloid 1px red;
}
.innerblockdiv{
    height: 50%;
    margin-bottom: -15px;
}
.innerdiv{
    outline: sloid 1px green;
    width: 30px;
    height: 30px;
}
{% endcodeblock %}
{% codeblock lang:HTML %}
<div class="outerdiv">
    <div class="innerblockdiv">
    </div>
    <div class="innerdiv">
    </div>
</div>
{% endcodeblock %}

##top、bottom为0上下margin为auto
设置固定高度，上下margin设置为auto，top和bottom为0，position为absolute。当然outerdiv的position不能为默认的static。
{% codeblock lang:CSS %}
.outerdiv {
    width: 100px;
    height: 100px;
    outline: sloid 1px red;
}
.innerdiv{
    position: absolute;
    top: 0;
    bottom: 0;
    margin: auto;
    outline: sloid 1px green;
    width: 30px;
    height: 30px;
}
{% endcodeblock %}
{% codeblock lang:HTML %}
<div class="outerdiv">
    <div class="innerblockdiv">
    </div>
    <div class="innerdiv">
    </div>
</div>
{% endcodeblock %}

方法就是这几种，参考了[这篇文章](http://www.qianduan.net/css-to-achieve-the-vertical-center-of-the-five-kinds-of-methods.html),当然方法应该还有其他的，我还没去探索，另外这几种方法的优缺点我还没有仔细考量，参考的文章中做了介绍，大家可以去看下。我也分别实验了集中方法，还是写出来心安。
