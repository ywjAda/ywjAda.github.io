 1. SEO是什么
 2. Vue为什么会出现SEO的问题
 3. 如何解决Vue的SEO



# Vue的SEO问题
##  1. SEO是什么
SEO（Search Engine Optimization）搜索引擎优化
 搜索引擎爬虫的基本原理就是 
 	1. 抓取url
 	2. 获取HTML源码并解析
 对网站进行
 	1. 站内优化和修复
 	2. 站外优化
 从而提高网站的网站关键词排名以及公司产品的曝光度
##  2. Vue为什么会出现SEO的问题
``Vue 是单页面应用，爬虫只能爬取到html页面的内容，无法爬取到js脚本里面的内容。单页面应用是通过js脚本改变页面的内容，并没有进行http的请求，爬虫爬取不到，就会造成SEO较差``
### 前端渲染 PK 后端渲染
后端渲染： PHP、Java、Python 的渲染机制
同构渲染： 前后端共用JS，介于前后端中的共有部分
前端渲染：JS来渲染页面大部分内容 ==》SPA单页面应用
					Vue就是JS框架，最大的特点就是单页面应用【不是每次通过url请求服务器，再通过浏览器渲染出页面，而是在首屏显示出内容之后，直接通过js动态修改页面的内容】

### 前端渲染遇到的问题 -- SEO 和 首屏问题
## 3.  如何解决Vue的SEO
既然在第二节已经提到了，前端渲染会出现两个问题：SEO和 首屏问题，所以直接将两个问题一起解决掉

### SEO的解决方案
### 1. 预渲染
https://zhuanlan.zhihu.com/p/29148760
改善少量营销页面
== prerender-spa-plugin 结合 vue-meta-info==


### 2. SSR 
https://cn.vuejs.org/v2/guide/ssr.html
#### 什么是服务器渲染
1. SEO对网站十分重要
2. 页面是异步获取内容 时

将一个组件渲染为服务器端的html字符串，将他们直接发送到浏览器，最后将这些静态标记“激活”为客户端完全可交互的应用程序
==组件渲染，服务器端HTML，发送到浏览器，静态标记==
#### 使用服务器渲染的好处
==>解决单页面应用的SEO问题
1. SEO  
对==同步==JS应用程序进行索取
抓取工具并不会等待异步完成后再抓取内容
#### 怎么使用服务器渲染
==> node.js后端使用了nuxt.js 进行服务器渲染
##### nuxt.js
1. webpack等配置全部封装好了
2. 无需node知识
3. 方便可用
安装 -》 写组件 -》 编译并启动服务 -》看效果
1. 安装
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191020154037557.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)


### 3. 路由采用h5 history模式
-- h5 的 history模式是vue-router的一种。因此直接看 vue-router
