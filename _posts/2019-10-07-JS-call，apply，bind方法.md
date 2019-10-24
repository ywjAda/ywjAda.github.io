## call、apply、bind方法各自的定义和异同
### 作用
call、apply、bind的作用是改变函数运行时this的指向。
==this==
函数的调用方法：
	1. 方法调用模式: 【函数被放在对象中当一个方法，调用属性时，this被绑定在当前对象上】
	当一个函数被保存为对象的一个方法是，调用这个表达式包含一个提取属性的动作，那么他就是被当作一个方法来调用。此时的this被绑定到这个对象
```javascript
var a = 1;
var obj = {
	a: 2;
	fn: function() {
		console.log(this.a)
	}
}                                   
obj.fn()     // 2            
```
 this 指 obj 这个 对象 ， obj.fn() 实际是obj.fn.call(obj)                        
 ==DOM对象绑定事件也属于方法调用模式==

```javascript
 document.addEventListener('click', function(e){
	console.log(this);
	setTimeout(function(){
		console.log(this);
	}, 200);
}, false);
```

点击页面依次输出 document和window对象
点击页面监听click事件，this指向事件源DOM对象：document。即obj.fn.apply(obj)
setTimeout内的函数是回调函数。即f1.call(null, f2)。f2指向window
	2. 函数调用模式：
	普通的函数调用，this被绑定到window
		1. 最普通的函数调用
```javascript
	function f1() {
			console.log(this);
		}
	f1(); // window
```
        2. 函数嵌套
	
```javascript
function f1() {
			function f2() {
				console.log(this);
			}
			f2()
		}
f1(); // window
```
		3. 把函数赋值后调用
```javascript
	  var a = 1;
	  var obj1 = {
		a: 2;
		fn:function(){
			console.log(this.a)
		}
	}
	var fn1 = obj1.fn
	f1() //1
```
obj1.fn是一个函数。此时fn1就是不带任何修饰的函数调用。function（）{console.log（this.a）}.call(undefined)。按理说打印出来的this应该是undefined。但浏览器有一条规则：
如果你传的context是null或者undefined。那么window对象就是默认的context【严格模式下默认context是undefined】
==注意与方法调用相区别==
			4. 回调函数
```javascript
		var a = 1;
		function f1(fn){
			fn();
			console.log(a) //1
		}
		f1(f2)
		function f2(){
			var a = 2
		}
```
		改写代码如下：
		

```javascript
var a = 1
		function f1(){
			(function (){var a = 2})()
			console.log(a) //1
		}
		f1()
```
仍旧是最普通的函数调用。f1.call(undefined).this指向window。打印出的是全局的a

			5. 构造器调用模式：
	new一个函数时，背地里会创建一个连接到prototype成员的新对象。同时this会被绑定到那个新对象上
```javascript	
function Person(name, age) {
	// 这里的this都指向实例
	this.name = name
	this.age = age
	this.sayAge = function(){
		console.log(this.age)
	}
}
var dot = new Person('Dot', 2)
dot.sayAge() //2
```


6. call
	call方法第一个参数绑定this的值。后面传入参数列表。当第一个参数为null、undefined时，默认指向window
 7. apply
	apply接收两个参数，第一个参数是要绑定的this的值，第二个参数是一个参数数组。同理当第一个参数为null、undefined时，默认指向window
	==call、apply用法几乎相同。唯一差别在于 【当函数需要传递多个变量时。apply可以接受一个数组作为参数输入。call则是接受一系列单独的变量==
	8. bind
	和call类似，第一个参数是this的指向，第二个参数开始是接收的参数列表。
	返回值是函数  bind接收的参数列表的使用
==返回值是函数==

```javascript
var obj= {
	name: 'Dot';
}
function printName(){
	console.log(this.name)
}
var dot = printName.bind(obj) 
console.log(dot) // function (){...}
dot() // Dot
```
bind 方法不会立即执行，而是返回一个改变了上下文this后的函数。而原函数printName中的this并没有改变，依旧指向全局对象window

10. 应用场景
	参数的使用
	
```javascript
	function fn(a, b, c) {
		console.log(a, b, c) ;
	}
	var f1 = fn.bind(null, 'Dot'); // function fn(a,b,c){...}
	// 第一个参数是this的值，为null或者为undefined时，this指向window
	fn('A', 'B', 'C'); //A B C	  
	f1('A', 'B', 'C'); //Dot A B
	f1('B', 'C'); //Dot B C
	fn.call(null, 'Dot'); //Dot undefined undefined
```
call 是把第二个及以后的参数作为fn方法的实参传进去，而f1方法的实参是在bind参数的基础上往后排

```javascript
var add = function(x) {
	return function(y) {
		return x+y;
	};
};
var f1 = add(1); // f1 为 function(y){...}
f1(3); //add(1)使x为1，f1(3)使y为3
```
自己实现一个bind方法

```javascript
if（！Function.prototype.bind）{
	Function.prototype.bind = function() {
		var self = this, //保存原函数
				context = [].shift.call(arguments), // 保存需要绑定的this上下文
				args = [].slice.call(arguments); // 剩余参数转换成数组
				return function（）{
				self.apply(context, [].concat.call(args, [].slice.call(arguments)));
		}
	}
}
```
call,apply实现继承
function Person（name，age）{
	this.name = name;
	this.age = age;
	this.sayName = function() {
		console.log(this.age)
	}
} 
function Female(){
	Person.apply(this, arguments); // Female通过apply里的this改变了this指向，直接继承了Person
}
var dot = new Female('Dot', 12) //dot 是Female的实例

11. 总结
	call，apply都是==改变上下文中的this==并==立即执行这个函数==
	bind方法可以让对应函数==想什么时候调就什么时候调用==，并且可以将==参数在执行的时候添加==
	在Es6的箭头函数下，call和apply将失效。
	对于箭头函数来说：
	1. 箭头函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。所以不需要var _this = this 这种丑陋的写法
	2. 箭头函数不可以当构造函数，也就不可以用new命令
	3. 箭头函数不可以用arguments对象，该对象在函数体内不存在，如果要用，可以用Rest参数代替
	4. 不可以用yield命令，箭头函数不能用作Generator函数

