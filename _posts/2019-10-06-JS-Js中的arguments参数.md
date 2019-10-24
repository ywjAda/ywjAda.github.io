# 类数组对象：arguments
封装实参的对象arguments
## 为什么要有arguments
JavaScript并没有重载函数的功能，但Arguments对象能够模拟重载。
JavaScript中每个函数都有Arguments对象实例arguments
arguments.length 为函数实参个数
arguments.callee 为引用函数自身

## arguments特性
==arguments和function生死相依==
## 使用方法
跟数组一样使用
### callee属性，返回正被执行的Function对象
==针对同个方法多处调用并且传递参数个数不一样时进行使用==
var sum = function（n） {
	if （1 == n）{
		return 1;
	} else {
		return n + arguments.callee(n-1);
	}
}
alert(sum(6)); // 21

### 1. 利用arguments实现方法的重载

```javascript
function add() {
	var len = arguments.length;
	var sum = 0;
	for(;len--;) {
		sum += arguments[len];
	}
	return sum;
}
console.log( add(1, 2, 3) );
console.log( add(1, 3) );
```
### 2. 利用callee实现递归
function factorial(num) {
	if(num <= 1) {
		return 1;
	} else {
		return num + arguments.callee(num-1);
	}
}

      

