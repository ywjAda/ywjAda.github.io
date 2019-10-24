1. vue-router是什么
2. vue-router有哪几种方法
3. 怎么使用vue-router

单页面应用： 基于路由和组件![在这里插入图片描述](https://img-blog.csdnimg.cn/20191020172133206.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)

1. route： 一条路由
2. routes：一组路由
3. router： 管理路由
4. 客户端中的路由： dom元素显示或者隐藏。==》基于hash和基于HTML5 history api



# vue-router 
实现vue组件之间交互 --》 会被解析为 a href ⇒ 为什么不直接使用a??  ==单页面应用，只有主页面一个.html ,a标签无用==

# 实现路由
## 1. 基于hash实现
### 原理
监听onhashchange()事件， 仅hash符号之前的内容会被包含在请求中。



路径和组件==对应==起来，在页面中把组件渲染出来
1. 页面实现（HTML模板中）
<router-link> 定义页面中点击  :to =" 去哪”
<router-view>显示的地方

2. js配置路由
	1. 定义route。一条路由两部分组成： path和component
	2. 两条路由，组成routes
			const routes = [
			{ path: '/home', component: Home },
			{ path: '/about', component: About}
		]
	3. 对路由进行管理 =》创建路由
	const router = new VueRouter({
		routes
		})
3. 注入Vue根实例进行使用
const app = new Vue({
	router
	}).$mount('#app')

用户点击 router-link标签时，会去寻找to属性。它的to属性和js中配置的路径（path：'/home', component: Home） path 对应。找到匹配的组件，最后把组件渲染到<router-view>标签所在的地方   
		![在这里插入图片描述](https://img-blog.csdnimg.cn/20191020213552175.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019102111155568.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)

``出错点``
``Non-nested routes must include a leading slash character. Fix the following routes: ``
非嵌套路由必须包含前导斜杠字符
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191020222716146.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191020222736698.png)
### 动态路由
访问网站并登陆成功， 显示页面+名字 ==》 名字不同。user 是一个组件。不同用户【id不同】 =》同一个user组件中 =》 路由不能写死
vue-router 动态部分： 以：开头

```
route： {
	path：“user/:id”,
	component: user
}
```
### 步骤
1. 创建user.vue 组件
2. router中的index.js 引入 user 组件并进行使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021124023172.png)
3. App.vue中与路由建立连接
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021124145263.png)
## 原理
1. 整个vue-router注入到根实例
2. 组件内部，通过this.$route来获取到router实例
3. params属性获得动态部分。

动态路由来回切换，组件不发生变化，只能使用watch来监听$route的变化
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021131633408.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)
==嵌套路由 ===》 childrens 
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019102115484220.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021154808755.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)
==编程式导航==




## 2. h5的history实现
从图可以看出，通过hash方式进行路由会有一个丑陋的 # 。因此就有了基于history的方法实现
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021151655388.png)
### 1. history实现方法
声明是history模式
1. + mode：‘history’
匹配不到任何资源的时候，要返回一个页面【Error.vue】 避免返回404错误页面
2. {path： ‘*’， component：Error}
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021152459299.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)
没有啦！！开心
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021152416661.png)

### 2. history实现原理
1. 浏览器点击后退按钮或js调用history.back  => ==触发onpopstate事件==
2. pushState 往history对象里添加一个新的历史记录
3. replaceState是替换history对象中的当前历史

缺陷： 直接访问二级页面或在页面刷新，会出现404 错误 ==》 重定向
