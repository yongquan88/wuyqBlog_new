---
title: this指向分析
date: 2018-01-16 15:25:10
tags: this apply call bind
---

### 两个基本原则
    * this要在执行的时候才能确定值，定义时无法确定
    * 谁调用指向谁，没有谁调用就指向window

    
```bash
	//var name='i am window name';//window下的name
	var a={
		name:'wuyq',
		fn:function(){
			console.log(this.name);
		}
	}

	a.fn(); //this===a
	a.fn.call({name:'hello world'});  //this==={name:'hello world'}
	var fn1=a.fn;
	fn1(); //this===window
```


### this指向
	*1.作为构造函数执行 this.name...
	*2.作为对象属性执行 f.callname()
	*3.作为普通函数执行 testFn() this指向window
	


```bash
	//执行构造函数
		function Foo (name){
			//this={};
			this.name=name;
			// return this;
		}
		var f = new Foo('wuyq');
		f.name;

		//执行对象属性
		var obj={
			name:'wuyq',
			sex:'man',
			say:function(){
				console.log(this.name);
			}
		}
		obj.say();//this===obj

		// //作为普通函数执行
		function testFn(){
			console.log(this);
		}
		testFn();//this===window
```


### call apply bind 可以改变this指向


```bash
	function fn1(name){
			console.log(name);
			console.log(this);
			console.log(arguments);
		}
		fn1('hello');
		//call改变this指向
		fn1.call({x:100},'world','25');//this==={x:100}

		//apply改变this指向
		fn1.apply({x:200},['world','25']);//this==={x:200}

		//bind改变this指向  ps：.bind必须是函数表达式
		var fn2 =function (name){
			console.log(name);
			console.log(this);
		}.bind({y:300});
		fn2('wuyq');
```