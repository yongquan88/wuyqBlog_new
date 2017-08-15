---
title: 一个超级简单的redux例子
date: 2017-06-15 20:05:22
tags: redux
---

	随着js单页面应用开发日趋复杂，js需要管理的state（状态）也越来越复杂，
	这时候一般都会引用redux来做state的管理。下面用一个简单的例子来理解redux的api。

#### store的几个api
		* dispatch:用于action的分发，改变store里面的state
		* subscribe：注册listener，store里面state发生改变后，执行该listener
		* getState：读取store里面的state
		* replaceReducer：替换reducer，改变state修改的逻辑


```bash
	//引入store的创建方法
	import {createStore} from 'redux';

	//定义reducer,即state的改变逻辑
	function counter(state=0,action){
		let {type} = action;

		switch(type){
			case 'INCREMENT':
				return ++state;
			default:
				return state;
		}
	}

	//创建store
	let store = createStore(counter);

	$(document).click(ev=>{
		//定义action
		function IncrementAction(){
			return {
				type:'INCREMENT'
			}
		}
		//分发改action
		store.dispatch(IncrementAction());
	});

	//注册listener，当store里面的state改变的时候会执行
	store.subscribe(()=>{
		//获取改变后的state
		let state=state.getState();
		console.log(state);
	});
```