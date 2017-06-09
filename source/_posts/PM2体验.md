---
title: PM2体验
date: 2016-05-30 11:31:41
tags: PM2
---

前段时间折腾了一下Amazon EC2 的免费服务,然后想着顺便把之前的node联系项目部署上去,我是通过ssh连接服务去启动我的服务，可是当我断开ssh连接的时候服务就关掉了，郁闷。
后台经老大介绍 pm2 这个工具，顺便也体验了下pm2 cluster….

### PM2介绍
pm2 是一个带有负载均衡功能的node应用的进程管理器。当你要把你的独立代码利用全部的服务器上所有cpu，并保证进程永远活在，0秒加载，pm2是完美的。

#### 主要特性:
   * 内建负载均衡(使用Node cluster 集群模块)
   * 后台运行
   * 0秒停机重载 ps：我理解的意思是维护升级的时候不需要停机
   * 具有Ubuntu和CentOS 的启动脚本
   * 停止不稳定的进程（避免无限循环）
   * 控制台检测
   * 提供 HTTP API
   * 远程控制和实时的接口API ( Nodejs 模块,允许和PM2进程管理器交互 )

### PM2安装
``` bash
    npm install -g pm2
```

### PM2的使用
    
* pm2 start app.js -i 4 #后台运行pm2，启动4个app.js的进程（具体的进程会依赖于cpu的核心数目，也可以传'max'或者 '0'参数，系统会根据cpu的核数来启动最多的进程）
* pm2 start app.js --name appname #命名进程
* pm2 list #显示所有进程状态
* pm2 monit #监视所有进程
* pm2 logs #显示所有进程日志
* pm2 stop all #停止所有进程
* pm2 stop id/name #停止某个进程
* pm2 restart all #重启所有进程
* pm2 delete id/name #杀死特定的进程
* pm2 delete all #杀死全部进程

更多更详细的内容请到官网 [PM2](http://pm2.keymetrics.io/docs/usage/quick-start/)