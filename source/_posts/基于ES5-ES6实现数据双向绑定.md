---
title: 基于ES5/ES6实现数据双向绑定
date: 2019-04-02 16:22:19
tags: defineProperty Proxy
---

首先理解双向数据绑定与单向数据绑定的含义和区别：
*双向绑定：视图（View）的变化能实时让数据模型（Model）发生变化，而数据的变化也能实时更新到视图层。
*单向数据绑定：只有从数据模型到视图这一方向的改变关系。

实现双向数据绑定有两种方式 ES5 的 defineProperty 和 ES6 的 Proxy。

### ES5 的 defineProperty 实现，直接上代码

```bash
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script>
    var obj={title:''};
    //对obj的title进行拦截处理
    Object.defineProperty(obj,'title',{
      get:function(){
        return title;
      },
      set:function(newValue){
        title=newValue;
        document.querySelector('#value').innerHTML = newValue // 更新视图层
        document.querySelector('input').value = newValue // 数据模型改变
      }
    });
    function onKeyUp(event) {
      obj.value = event.target.value
    }
  </script>
</head>
<body>
  <p>
    值是：<span id="value"></span>
  </p>
  <input type="text" onkeyup="onKeyUp(event)">
</body>
</html>
```

### ES6 的 Proxy

随着 vue3.0 放弃了支持 IE 浏览器，而且 Proxy 兼容性越来越好，能支持 13 中劫持操作。
因此 vue3.0 选择使用 Proxy 来实现双向数据绑定，而不再使用 Object.defineProperty。

```bash
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<title>Document</title>
<script>
  var obj = new Proxy({},{
    get:function(target,key,receiver){
      return Reflect.get(target,key,receiver);
    },
    set:function(target,key,value,receiver){
      if(key==='title'){
        document.querySelector('#value').innerHTML = value
        document.querySelector('input').value = value
      }
      return Reflect.set(target,key,value,receiver);
    }
  })

  function onKeyUp(event) {
    obj.title = event.target.value
  }

</script>
</head>
<body>
<p>
  值是：<span id="value"></span>
</p>
<input type="text" onkeyup="onKeyUp(event)">
</body>
</html>

```
