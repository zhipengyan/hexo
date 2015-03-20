title: DIV垂直居中的方法
date: 2015-03-19 20:11:34
categories: 前端
tags: [HTML,CSS]
---
>因为想做前端，目前手中的工作渐渐地越离越远，尝试着去做了一次面试。虽然在面试之前也是早起晚睡地准备了好几天，但毕竟没有太多的实战经验，遇到的一些面试题很熟悉，但是就是说不出来，平时工作是遇到问题就查资料，做完了也没有记住。所以还是要积累一下，把知道的讲出来才是真的知道！

言归正传我们来了解一下这道题目的几种解法

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
{% endcodeblock %}
{% codeblock lang:HTML %}
<div class="outerdiv">
    <div class="innerdiv">
    </div>
</div>
{% endcodeblock %}

最终效果如下图

##使用绝对定位的DIV
