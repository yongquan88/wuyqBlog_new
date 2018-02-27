---
title: 'Javascript设计模式之发布-订阅模式 '
date: 2018-02-27 16:42:54
tags: 设计模式 发布-订阅
---

发布-订阅模式又叫观察者模式,他定义了一种一对多的依赖关系,即当一个对象的状态发生改变的时候,所有依赖他的对象都会被得到通知
    
    
#### 直接上代码
   
```bash
    var createEventSys=function(){
        return {
            //通过on接口监听事件eventName
            //如果事件eventName被触发，则执行callback回调函数
            on:function(eventName,callback){
                //如果Event对象没有handles属性，则给Event对象定义属性handles，初始值为{}
                //handles属性是用来存储事件和回调函数的（即存储订阅的时间和触发事件后执行的相应函数方法）
                if(!this.handles){
                    this.handles={};
                }
                //如果handles中不存在时间eventName，则将事件存储在handles中，同时初始化改事件对应的回调函数集合
                if(!this.handles[eventName]){
                    this.handles[eventName]=[];
                }
                //往handles中的eventName对应的回调函数集合push回调函数callback
                this.handles[eventName].push(callback);
            },
    
            //触发时间 eventName
            emit:function(eventName){
                //如果事件eventName有订阅者，则依次执行事件eventName的订阅者相应的回调方法
                if(this.handles[arguments[0]]){
                    for(var i=0;i<this.handles[arguments[0]].length;i++){
                        this.handles[arguments[0]][i](arguments[1]);
                    }
                }
            },
    
            //移除事件 eventName
            remove:function(eventName,fn){
                //判断时间eventName是否存在fn这个观察者，如果有，则移除事件eventName的fn观察者
                if (this.handles[arguments[0]]) {
                    for(var i=0;i<this.handles[arguments[0]].length;i++){
                        var _fn=this.handles[arguments[0]][i];
                        if(_fn===fn){
                            this.handles[arguments[0]].splice(i,1);
                            break;
                        }
                    }
                }
            }
        }
    }
```
    
#### 使用
```bash
        var Event=createEventSys();

        Event.on('test',function(result){
            console.log(result);
        })
        Event.on('test',function(){
            console.log('test');
        })

        Event.on('test1',function(result){
            console.log(`test1:${result}`)
        })

        Event.emit('test','hello world~!');
        Event.emit('test1','welcome to GZ!');

        //ps 想要remove订阅者，就不能用匿名函数
        var testRemove=function(result){
            console.log('test remove'+result);
        }
        Event.on('test',testRemove);
        Event.emit('test','haha');
        Event.remove('test',testRemove);
        Event.emit('test','haha');

        //对象person1和对象person2拓展复用自定义系统
        var person1={};
        var person2={};
        Object.assign(person1,createEventSys());
        Object.assign(person2,createEventSys());

        person1.on('call1',function(){
            console.log('person1');
        })

        person2.on('call2',function(){
            console.log('person2');
        });

        person1.emit('call1');// 输出 person1
        person1.emit('call2');// 没有输出
        person2.emit('call1');// 没有输出
        person2.emit('call2');// 输出 person2
```
    
    
### 小结
    1.发布-订阅的优势很明显，做到了时间上的解耦和对象之间的解耦，
    从架构上看，MVC，MVVM都少不了发布-订阅的参与;
    2.发布-订阅同时也是有缺点存在的，创建订阅者本身要消耗一定的时间和内存，
    而且当你订阅一个消息以后，可能此消息最后都未发生，但是这个订阅者会始终存在于内存中。
    如果程序中大量使用发布-订阅的话，也会使得程序跟踪bug变得困难。