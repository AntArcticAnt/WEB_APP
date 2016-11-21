# WEB_APP
A mobile Reader software project learned from mooc

引擎:LHS RHS
作用域=规则=用来查找变量的规则=管理引擎在当前作用域和嵌套的子作用域下
标识符=函数,变量

词法作用域:(编写的作用域,最基础的,全局???)
第一阶段叫做词法化:源代码解析成电脑看得懂的东西(词法作用域由写程序的人决定的)
//欺骗词法



逐级嵌套的作用域,查找变量


函数作用域:属于这个函数的全部变量都可以在整个函数的范围内使用以及复用.(自身必须能)
最小特权原则:模块和api.内部的东西无法被外部访问.


函数作用域:无论函数哪里被调用,也无论它如何被调用,它的词法作用域都只由函数被声明时所处的位置决定(它的词法作用域):

词法作用域只会查找一级标识符,外层用对象属性访问规则.
foo.bar.baz   词法作用域只会查找foo变量,bar和baz 用对象属性访问规则.


		

 // 预解析和提升

	// fn1(); //2
	// var fn1 = function(){
	// 	alert(3);
	// }
	
	// function fn1(){
	// 	alert(1);
	// }
	
	// fn1();//3
	
	
	// function fn1(){
	// 	alert(2);
	// }





立即执行函数表达式:函数被当作函数表达式(一个球)而不是一个标准的函数声明来处理
标准的函数声明(有函数名污染作用域) 		被当作函数表达式

var a=2;                                      var a=2;
function foo(){                           (function foo(){
	var a=3;								     var a=3;  
	console.log(a);                          console.log(a);

}                                            })();
foo();

console.log(a);                           console.log(a);


区别:他们的名称标识符将会绑定在何处:

		声明中:foo被绑定在所在的作用域

		自执行的函数表达式:foo被绑定在函数表达式自身的函数中,而不是所在的作用域中.(不会污染作用域)


		(function foo(){。。}（）)
		表达式:作为函数表达式意味着foo只能在。。所代表的位置中被访问（递归？？）,外部作用域则不行.








由于函数包含在一对()括号内部,因此成为了一个表达式.(一个表达式)(一个表达式)
通过在末尾加上另外一个()可以立即执行这个函数.
(function foo (){})();
(function(){})();
(function(){...}())
immediately invoked function expression

用法2:
		进阶用法:把它们当做函数调用并传递参数进去.   //用于改进风格

var a=2;
(functionIIFE(global){

var a=3;
console.log(a);  //3
console.log(window.a); //2

})(window);

用法3:
		将需要运行的函数放在第二位,在IIFE执行之后当做参数传递进去(UMD:universal module definition)

var a=2;
(function IIFE(def){
	def(window);

})(function def(global){
	var a=3;
	console.log(a);   //3
	console.log(global.a)    //2
})



	for (var i = 0; i < 10; i++) {
			console.log(i)
		}
在for循环的头部直接定义了变量i,(i是被绑定在外部作用域)
if同理



闭包:在定时器,事件监听器,ajax请求,跨域,任何异步任务中,只要使用了回调函数,实际上就是在使用闭包.

for (var i=1;i<5;i++){
	setTimeout(function timer(){
	console.log(i);
	},i*1000)
}


模块:
function CoolModule(){
	var something="cool";
	var another=[1,2,3];

	function doSomething(){
	console.log(something);
	}

	function doAnother(){
	console.log(another.join("!"))
	}

	return {
	doSomething:doSomething,
	doAnother:doAnother
	};
}


var foo=CoolModule();
foo.doSomething();     //cool
foo.doAnother();       //1!2!3!



单例模式:

var foo=(function CoolModule(){
	var something="cool";
	var another=[1,2,3];

	function doSomething(){
	console.log(something);
	}

	function doAnother(){
	console.log(another.join("!"))
	}

	return {
	doSomething:doSomething,
	doAnother:doAnother
	};
})();
foo.doSomething();

