==浏览器有默认的双击缩放事件，为了判断用户第一次点击之后是想要触发事件还是双击缩放，就会等待300ms进行判断==
==通过fastClick在用户点击之后，立即触发模拟的click事件，然后阻止300ms 的默认事件来解决300ms延迟的问题==

# 1. 300毫秒延迟问题是什么问题
点击页面的时候，移动端浏览器并不是立即反应，而是会等300毫秒才出现点击效果。

## 产生原因
手指点击一个元素：touchstart【手指放到屏幕上时触发】-> touchmove【手指在屏幕上滑动触发】-> touchend【手指离开屏幕时触发】-> click【手指移动并从触摸到离开】

==双击缩放== 手指在屏幕快速点击两次会对网页进行缩放
						用户点击一次后，浏览器并不能判断用户是确实要打开，还是要进行双击操作。因此，就等待300毫秒，以判断用户是否再次点击了屏幕
						==浏览器会优先判断用户是否触发这些默认的行为==
## 解决方案
下面会讲解通过fast-slick来解决。但既然本身就是双击缩放造成的，那么就可以通过禁止双击缩放来避免这种问题
						
## 禁用缩放 ==> 双击无意义
```
<meta name="viewport" content="user-scalable=no">
<meta name="viewport" content="initial-scale=1,maximum-scale=1">
```
只是想禁止默认双击缩放行为，有时候还是想通过双指缩放

# 2. fast-click库解决300毫秒延迟问题的原理
## 原理
检测到touchend事件的时候，通过DOM自定义事件立即出发模拟一个click事件，并把浏览器在300ms之后真正的click事件阻止掉
==touchend后立即触发模拟的click事件，并把300ms真正的click事件阻止掉==
## 代码
FastClick.prototype.onTouchEnd = function(e) {
	// 如果不需要原生click元素
	if (!this.needsClick(targetElement)) {
	// 屏蔽原生事件
		e.preventDefault();
		// 触发模拟事件
		this.sendClick(targetElement， e);
	}
}

FastClick.prototype.sendClick = function(targetElement, event) {
 // 这里是一些状态检查逻辑
// 创建一个鼠标事件
 clickEvent = document.createEvent('MouseEvents');
  // 初始化鼠标事件为click事件 clickEvent.initMouseEvent(this.determineEventType(targetElement), true, true, window, 1, touch.screenX, touch.screenY, touch.clientX, touch.clientY, false, false, false, false, 0, null); 
  // fastclick的内部变量，用来识别click事件是原生还是模拟 clickEvent.forwardedTouchEvent = true; 
  // 在目标元素上触发该鼠标事件， targetElement.dispatchEvent(clickEvent);
  
就目前而言，FastClick 非常实际地解决 300 毫秒点击延迟的问题。唯一的缺点可能也就是该脚本的文件尺寸 (尽管它只有 10kb)。
# 3. fastClick的使用
1. 【安装】【自己需要的文件中】命令行 npm install fastclick --save
2. 【重启】重启服务器  npm run dev
3. 【导入+引用】main.js 中 导入 + 引用
	1. import fastClick from ‘fastClick’
	2. fastClick.attach(document.body)
