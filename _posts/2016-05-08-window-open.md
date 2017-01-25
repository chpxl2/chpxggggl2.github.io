---
layout: post
title: "window.open浏览器拦截"
date: 2016-05-08 20:34:26
image: '/assets/img/'
description: '已更新：'
main-class: 'jekyll'
color: '#B31917'
tags:
- js
categories:
twitter_text: 'window.open'
introduction: '当window.open为用户触发事件内部或者加载时，不会被拦截，一旦将弹出代码移动到ajax或者一段异步代码内部，马上就出现被拦截的表现了!'
---

## 现象
最近在做项目的时候碰到了使用window.open被浏览器拦截的情况，搞得人无比郁闷啊，虽然在自己的环境可以对页面进行放行，但是对用户来说，不能要求用户都来通过拦截。何况当出现拦截时，很多小白根本不知道发生了啥，不知道在哪里看被拦截的页面，简直悲催啊~~

另外，可以发现，当window.open为用户触发事件内部或者加载时，不会被拦截，一旦将弹出代码移动到ajax或者一段异步代码内部，马上就出现被拦截的表现了。

## 原因分析
当浏览器检测到非用户操作产生的新弹出窗口，则会对其进行阻止。因为浏览器认为这不是一个用户希望看到的页面。各浏览器对拦截时机的判断不一致，而对于放在ajax回调中的代码，反应又不相同了，这里就不再赘述。但是，被浏览器拦截我们代码中要弹出的窗口并不是程序员所希望的。

## 深入研究
我的项目是需要用window.open去下载，但是在下载之前我要获取先获取进度，也就是说我的window.open必须要放在进度100%的回调里。
```
function getProcess(){
    $http.get(GENERAL_CONFIG.BASE_URL + GENERAL_CONFIG.API_VERSION+"/processglobalbar/"+vm.task_id)
        .success(function(data){
            var progress = data.value;
            if(progress>100 || progress==100){
                MaskLayer.setActiveBarWidth(380,100);
                $interval.cancel(vm.timer);
                $timeout(function () {
                    MaskLayer.remove();
                    $window.open(GENERAL_CONFIG.BASE_URL + GENERAL_CONFIG.API_VERSION + "/reportglobal/"+ vm.task_id);   //他是在回调里面的，被拦截了就不能下载了，囧啊~后来没有办法我才加了‘_self'。他还是会被拦截，但是是可以下载的。
                },1000);
            }else{
                var width = parseInt(progress* 380/100);
                MaskLayer.setActiveBarWidth(width,progress);
            }
        })
        .error(function(data){
            if(data.error){
                toastr.error(data.error,'error');
                $interval.cancel(vm.timer);
                MaskLayer.remove();
            }
        });
}

```
## Donation

If you liked my work, buy me a coffee <3

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UTMFZUHX6EUGE)

## License

This theme is free and open source software, distributed under the The MIT License. So feel free to use this Jekyll theme on your site without linking back to me or using a disclaimer.

If you’d like to give me credit somewhere on your blog or tweet a shout out to [@willian_justen](https://twitter.com/willian_justen), that would be pretty sweet.