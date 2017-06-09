---
title: js获取url的参数
date: 2016-06-02 16:01:50
tags: javascript
---

在开发中经常会遇到从url中获取参数的需求，解决的方法可以有很种，有些框架中已经封装了对应的方法给我们直接用就可以，比如angularjs中$location模块的search()方法就直接返回url中包含参数的对象，方便好用！

可是如果直接用原生js去获取呢？曾经我的做法是从url中找到第一个’?’后面的那部分，然后在切割组成json对象，但总感觉这种方法不够好，就是无法保证第一个’？’后面的那些就是我想要的参数字符串。

知道今天才发现a标签中有个属性search就给我们提高了参数部分的字符串了

#### 代码如下
``` bash
    var arr=urlParse('www.baidu.com?a=1&b=2');
    console.log(arr);//{"a":1,"b":2}
    
    function urlParse(url){
        var query={};
        var oA=document.createElement('a');
        oA.href=url;
        var arrParms=oA.search.slice(1).split('&');
        for(var i=0;i<arrParms.length;i++){
            var temArr=arrParms[i].split('=');
            query[decodeURIComponent(temArr[0])]=(decodeURIComponent(temArr[1]) || '');
        }
        return query;
    };
```

#### 关键的地方
``` bash
    var arrParms=oA.search.slice(1).split('&');
```

