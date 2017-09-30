---
title: react生命周期
date: 2017-09-30 16:07:46
tags: react react生命周期
---

每个Component都提供了一些生命周期函数的钩子.理解react生命周期的每个钩子函数的意义和用途有利于我们掌握react和开发react项目.
生命周期方法前缀包含 will 表示该钩子函数会在该生命周期之前调用;
生命周期方法前缀包含 did  表示该钩子函数会在该生命周期之后调用;

一看一下 component 生命周期的图片:

![Mou icon](/uploads/react-component-lifecycle.png)

上图就是react component 的生命周期,从 组件挂载(mount)到更新(updating)再到销毁(unmount)的过程.


react component 的生命周期可以分为下面几类: mounting->updating>unmounting

### Mounting(挂载)
    下面这些方法将会在component实例被创建和插入到DOM后调用.
    * constructor()
    * componentWillMount()
    * render()
    * componentDidMount()
    
    
### Updating
    props/state 的变化都会导致更新.下面这些方法会在component重新渲染时调用.
    * componentWillReceiveProps()
    * shouldComponentUpdate()
    * componentWillUpdate()
    * render()
    * componentDidUpate()
    
  
  
### Unmounting
    该方法将会在component从DOM中移除时调用
    *componentWillUnmount()