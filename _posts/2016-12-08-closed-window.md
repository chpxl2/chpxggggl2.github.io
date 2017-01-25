---
layout: post
title: "浏览器关闭事件"
date: 2016-05-08 20:35:48
image: '/assets/img/'
description: '已更新：'
main-class: 'js'
color: '#7AAB13'
tags:
- js
- jekyll
categories:
twitter_text: '浏览器关闭事件'
introduction: '有些朋友想在浏览器关闭的时候，弹出alert 、confirm或者prompt等。实验证明，这种做法是失败的，原因是浏览器关闭事件自动屏蔽执行js的某些方法，从而防止恶意攻击或者无法关闭浏览器的现象。'
---

## 项目背景

用户在关闭浏览器的时候，有的时候希望给用户一些提示，提示确认或其他；或者有时候需要执行一些操作例如清除cookie等等。

## 相关描述

在浏览器关闭的时候，弹出alert 、confirm或者prompt等。实验证明，这种做法是失败的，原因是浏览器关闭事件自动屏蔽执行js的某些方法，从而防止恶意攻击或者无法关闭浏览器的现象，针对这些事件的处理，一般都是写在浏览器底层。因此，你想在关闭浏览器的时候弹出alert提示框是不可能的。要是你对浏览器感兴趣，您可以去研究这些问题，同时也可以自己写一个简单的浏览器（ps网上应该有相关的方法，据说不是很难）。对于浏览器底层的东西，恕我才疏学浅，不是很了解！

## 方法

我们需要用到浏览器关闭事件。
js捕捉浏览器关闭事件，写法如下：
```
window.onbeforeunload =function(){return'您确定要离开pp的blog吗？';}

```
此时页面会有一个确认框弹出，用于用户点击留在此页或者确定离开；如果你想执行某项命令或者函数，也可以写在window.onbeforeunload = function(){ deletedCooike()}

## 解释
onbeforeunload与onunload事件。

共同点：都是在刷新或关闭时调用；都可以在在< script>脚本中通过window.onunload来指定或者在< body>里指定。

区别点：
1. onbeforeunload在onunload之前执行，它还可以阻止onunload的执行
2. onbeforeunload是在页面刷新或关闭时调用,onbeforeunload是正要去服务器读取新的页面时调用此时还没开始读取
3. 而onunload则已经从服务器上读到了需要加载的新的页面，在即将替换掉当前页面时调用
4. onunload是无法阻止页面的更新和关闭的。而onbeforeunload 可以做到

最后：页面加载时只执行onload页面关闭时先执行onbeforeunload，最后onunload页面刷新时先执行onbeforeunload，然后onunload，最后onload。




## Donation

If you liked my work, buy me a coffee <3

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UTMFZUHX6EUGE)

## License

This theme is free and open source software, distributed under the The MIT License. So feel free to use this Jekyll theme on your site without linking back to me or using a disclaimer.

If you’d like to give me credit somewhere on your blog or tweet a shout out to [@willian_justen](https://twitter.com/willian_justen), that would be pretty sweet.