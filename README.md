# 总结
## ES5
##### javascript有哪几种数据类型
```
六种基本数据类型
* undefined
* null
* string
* boolean
* number
* symbol(ES6)
一种引用类型
* Object
```
## ES6
在使用新的ES6技巧时千万不要做过了头，使你的代码比你或者你的其他队友聪明
##### 什么是ES6，什么是Shims/Polyfills
##### 什么是块作用域:{}

```
let
	{
	console.log( a );	// undefined
	console.log( b );	// ReferenceError!

	var a;
	let b;
}
const
{
	const a = [1,2,3];
	a.push( 4 );
	console.log( a );		// [1,2,3,4]

	a = 42;					// TypeError!
}
```
##### 词法作用域和动态作用域，this和=>

```
动态作用域不关心它本身是怎样在哪里声明的，只关心它在哪里调用的，动态作用域的域链基于调用栈，而不是代码中的嵌套关系。
词法作用域关心的是函数在哪里声明的，动态作用域的概念和js中的this相同，this也关心函数在哪里调用的。
```
## REACT
## CSS

## 浏览器