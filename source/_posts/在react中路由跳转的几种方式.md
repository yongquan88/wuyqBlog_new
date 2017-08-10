---
title: 在react中路由跳转的几种方式
date: 2017-08-10 20:04:28
tags: react react-router
---

 在react开发中，常用的3种方式：

 #### 第一种，也是最简单的方式，用react-router 提供的Link组件来跳转,Link组件实质是创建一个A标签，当点击的时候用router.push()去做单页面的跳转(ps 它与 <a href="#"></a>的跳转不一样 ，后者是多页面之间的跳转，会刷新整个页面)

 ```bash
 	import {Link} from 'react-router';

 	//for example,assuming you have the following route:
 	<Route path="/posts/:postID" component={Post} />
 	//you could use the following component to link to that route:
 	<Link to={`/posts/${post.id}`} />
 ```

 #### 第二种，使用官方提供的方式 this.context.router,不过在使用之前必须定义这个类的contextTypes。

 ```bash
 	...
 	export default class Abc extends Component {
 			...
 		this.context.router.push('/');
 	}
 	Abc.contextTypes= {
 		router: React.PropsTypes.object
 	}
 ```

 #### 第三种，使用react-router提供的withRouter高阶函数包装一下，使得能在this.props中获得router对象，同时也不用定义类的contextTypes。

 ```bash
 	...
 	import {withRouter} from 'react-router';
 	class Abc extends Component {
 		...
 		this.props.router.push('/');
 	}
 	export default withRouter(Abc);
 ```
 withRouter函数的其实就是把我们把传进去的组件从this.context把router对象放在组件的props里，方便我们使用。