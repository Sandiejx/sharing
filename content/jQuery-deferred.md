# 《关于deferred对象的简单介绍》

---

## About Me

@state: blue, @fragment

* **Sandyxjiang**
* ISUX - UI开发
* Qlippie项目组

---

## 简介

@state: blue, @fragment

* 从jQuery 1.5.0版本开始引入deferred对象
* 彻底改变了如何在jQuery中使用ajax

---

## 什么是deferred对象

@state: blue, @fragment

* 同步操作 -> eg.遍历一个大型数组
* 异步操作 -> eg.ajax读取服务器数据

* 回调函数(callback)

* 但是在回调函数方面，jQuery的功能非常弱。为了改变这一点，jQuery开发团队就设计了deferred对象。

**简单说，deferred对象就是jQuery的回调函数解决方案。**

---

## ajax操作的链式写法

---

## jQuery的ajax操作的传统写法

```javascript
$.ajax({
　　　　url: "test.html",
　　　　success: function(){
　　　　　　alert("哈哈，成功了！");
　　　　},
　　　　error:function(){
　　　　　　alert("出错啦！");
　　　　}
　　});
```
* [Demo1] http://jsfiddle.net/ruanyf/pdQYH/
* Tips: XHR对象

---

## $.ajax()返回的对象

* jQuery版本低于1.5.0，返回XHR对象，不能进行链式操作。
* jQuery版本高于1.5.0，返回deferred对象，可以进行链式操作。

---

## 新的写法

```javascript
	$.ajax("test.html")
　　 	.done(function(){ alert("哈哈，成功了！"); })
　　 	.fail(function(){ alert("出错啦！"); });
```
* done -> success
* fail -> error

* [Demo2] http://jsfiddle.net/ruanyf/dYKLJ/
* Tips: deferred对象

---

---

## 指定多个回调函数

* deferred对象允许你自由添加多个回调函数

```javascript
	$.ajax("test.html")
　　 	.done(function(){ alert("哈哈，成功了！");} )
　　 	.fail(function(){ alert("出错啦！"); } )
　　	.done(function(){ alert("第二个回调函数！");} );
```

* [Demo3] http://jsfiddle.net/ruanyf/CdKjn/
* Tips:回调函数可以添加任意多个，它们按照 添加顺序 执行

---

## 为多个操作指定回调函数

* deferred 对象允许你为多个事件指定一个回调函数，这是传统写法做不到的。 
* 引入一个新的方法$.when()

```javascript
	$.when($.ajax("test1.html"), $.ajax("test2.html"))
　　	.done(function(){ alert("哈哈，成功了！"); })
　　	.fail(function(){ alert("出错啦！"); });
```

* [Demo4] http://jsfiddle.net/ruanyf/CdKjn/
* Tips:这段代码的意思是，先执行两个操作 $.ajax("test1.html") 和 $.ajax("test2.html") ，如果都成功了，就运行 done() 指定的回调函数；如果有一个失败或都失败了，就执行 fail() 指定的回调函数。

---

## 普通操作的回调函数接口（上）

* deferred 对象的最大优点，就是它把这一套回调函数接口，从 ajax 操作扩展到了 所有操作 。也就是说，任何一个操作（不管是 ajax操作 还是 本地操作 ，也不管是 异步操作 还是 同步操作 ）都可以使用 deferred 对象的各种方法，指定回调函数。

```javascript
	var wait = function(){
　　var tasks = function(){
　　　　alert("执行完毕！");
　　};
　　setTimeout(tasks,5000);

	//指定回调函数
	$.when(wait())
	　　.done(function(){ alert("哈哈，成功了！"); })
	　　.fail(function(){ alert("出错啦！"); });
};
```
* [Demo5] http://jsfiddle.net/5wzrt/
* Tips:但是，这样写的话， done() 方法会立即执行，起不到回调函数的作用。
原因在于 $.when() 的参数只能是 deferred 对象，所以必须对 wait() 进行改写：

```javascript
	var dtd = $.Defferred();
	function wait(dtd){

	    var task = function(){
	        alert("执行完毕！");
	        dtd.resolve();    
	    };

	    setTimeout(tasks,5000);
	    return dtd;
	}


	//现在， wait() 函数返回的是 deferred 对象，这就可以加上链式操作了。
	$.when(wait(dtd))
　　	.done(function(){ alert("哈哈，成功了！"); })
　　	.fail(function(){ alert("出错啦！"); });

	
```
* [Demo6] http://jsfiddle.net/gfFPj/

---

## deferred.resolve()方法和deferred.reject()方法

* jQuery 规定， deferred 对象有三种执行状态—— 未完成 ， 已完成 和 已失败 。

* 如果执行状态是 "已完成"（resolved） ,调用 done() 方法指定的回调函数；
* 如果执行状态是 "已失败"（rejected） ，调用 fail() 方法指定的回调函数；
* 如果执行状态是 "未完成" ，则继续等待，或者调用 progress() 方法指定的回调函数（jQuery1.7版本添加）。

* 这两种方法可以用于程序员对 deferred对象 进行手动指定 执行状态 ，从而触发 done() , fail() 方法。

---

## deferred.promise()方法

```javascript
	var dtd = $.Deferred(); // 新建一个Deferred对象
	var wait = function(dtd){
	　　var tasks = function(){
	　　　　alert("执行完毕！");
	　　　　dtd.resolve(); // 改变Deferred对象的执行状态
	　　};
	　　setTimeout(tasks,5000);
	　　return dtd;
	};

	$.when(wait(dtd))
	    .done(function(){ alert("哈哈，成功了！"); })
	    .fail(function(){ alert("出错啦！"); });

	//加了一个resolve方法
	dtd.resolve();
```

* [Demo7] http://jsfiddle.net/nBFse/

以上代码在尾部加了一行 dtd.resolve(); ，直接改变了 dtd 对象的执行状态，导致 done() 方法立刻执行，跳出 “哈哈，成功了！” 的提示框，等5秒之后再跳出 “执行完毕！” 的提示框。

---

## deferred.promise()方法

为了避免这种情况， jQuery 提供了 deferred.promise() 方法。

它的作用是:

在原来的 deferred对象 上返回另一个 deferred对象 。
只开放与改变执行状态无关的方法（比如 done() 方法和 fail() 方法）
屏蔽与改变执行状态有关的方法（比如 resolve() 方法和 reject() 方法）
从而使得执行状态不能被改变。

```javascript
	var dtd = $.Deferred(); // 新建一个Deferred对象
	var wait = function(dtd){
	 　　var tasks = function(){
	 　　　　alert("执行完毕！");
	 　　　　dtd.resolve(); // 改变Deferred对象的执行状态
	 　　};

	　　　setTimeout(tasks,5000);
	　　　return dtd.promise(); // 返回promise对象
	};
	var d = wait(dtd); // 新建一个d对象，改为对这个对象进行操作
	$.when(d)
	    .done(function(){ alert("哈哈，成功了！"); })
	    .fail(function(){ alert("出错啦！"); });

	d.resolve(); // 此时，这个语句是无效的
```
* [Demo8] http://jsfiddle.net/Yur4R/

*在上面的这段代码中， wait() 函数返回的是 promise对象 。然后，我们把回调函数绑定在这个对象上面，而不是原来的 deferred对象 上面。

这样的好处是，无法改变这个对象的执行状态，要想改变执行状态，只能操作原来的deferred对象。

---

## deferred.promise()方法

* 但是，更好的写法应该是，将 dtd对象 变成 wait()函数 的内部对象：

```javascript
	var wait = function(dtd){
	var dtd = $.Deferred(); //在函数内部，新建一个Deferred对象
　　var tasks = function(){
　　　　	alert("执行完毕！");
　　　　　　dtd.resolve(); // 改变Deferred对象的执行状态
　　　　};

　　　　setTimeout(tasks,5000);
　　　　return dtd.promise(); // 返回promise对象
　　	};
　　$.when(wait())
　　.done(function(){ alert("哈哈，成功了！"); })
　　.fail(function(){ alert("出错啦！"); });
```
* [Demo9] http://jsfiddle.net/q9TvT/

---
## 普通操作的回调函数接口（中）

* 另一种防止执行状态被外部改变的方法，是使用 deferred对象 的建构函数 $.Deferred() ，直接把 wait() 传入：

```javascript
	$.Deferred(wait)
　　	.done(function(){ alert("哈哈，成功了！"); })
　　	.fail(function(){ alert("出错啦！"); });
```
* [Demo10] http://jsfiddle.net/ruanyf/CucGp/
Tips: 
* jQuery 规定， $.Deferred() 可以接受一个函数名（注意，是函数名）作为参数， $.Deferred() 所生成的 deferred对象 将作为这个函数的默认参数，并执行。

---

## 普通操作的回调函数接口（下）

* 除了上面两种方法以外，我们还可以直接在 wait对象 上部署 deferred 接口：

```javascript
	var dtd = $.Deferred(); // 生成Deferred对象
	var wait = function(dtd){
	　　var tasks = function(){
	　　　　alert("执行完毕！");
	　　　　dtd.resolve(); // 改变Deferred对象的执行状态
	　　};
	　　setTimeout(tasks,5000);
	};
	dtd.promise(wait);
	wait.done(function(){ alert("哈哈，成功了！"); })
	    .fail(function(){ alert("出错啦！"); });
	wait(dtd);
```
* [Demo11] http://jsfiddle.net/ruanyf/PF7Xf/
Tips: 
* 这里的关键是 dtd.promise(wait) 这一行
* 它的作用就是在 wait对象 上只部署 Deferred接口 ，不执行。所以才能直接在 wait 上面调用 done() 和 fail()

---

@fragment

## 总结

* 生成一个 deferred 对象
* deferred.done() 指定操作 成功 时的回调函数
* deferred.fail() 指定操作 失败 时的回调函数
* deferred.promise() 
	> 没有参数时，返回一个新的 deferred对象 ，该对象的运行状态无法被改变
	> 接受参数时，作用为在参数对象上部署 deferred接口
	> deferred.resolve() 手动改变 deferred对象 的运行状态为 "已完成" ，从而立即触发 done() 方法。
	> deferred.reject() 手动改变 deferred对象 的运行状态为 "已失败" ，从而立即触发 fail() 方法。
	> $.when() 为多个操作指定回调函数。
* deferred.then() ,可以把 done() 和 fail()一起写
```javascript
	$.when($.ajax( "/main.php" ))
	　　.then(successFunc, failureFunc );
```
	> 如果 then() 有两个参数，那么第一个参数是 done() 方法的回调函数，第二个参数是 fail() 方法的回调方法。
	> 如果 then() 只有一个参数，那么等同于 done() 

* deferred.always() 方法也是用来指定回调函数的，它的作用是，不管调用的是 deferred.resolve() 还是 deferred.reject() ，最后总是执行。

```javascript
$.ajax( "test.html" )
　　.always( function() { alert("已执行！");} );
```

---

@state: blue

## 谢谢大家！

<p style="font-size:6em"><i class="icon-smile"></i></p>



<style type="text/css">
.reveal h1 {font-size:2.4em;}
.reveal h2 {font-size:1.6em;}
.reveal img {max-width:100%;}
.reveal a:not(.image) { color: #ccc; color: rgba(255,255,255,0.8); }
.reveal a:not(.image):hover { color: #fff; }
.reveal .overlay {display:inline-block;width:auto;background:rgba(0,0,0,0.5);padding:0.5em 1em;margin:0;line-height:1.6;font-size:1.5em}

.browser-support {display: table; margin-top:2em!important;}
.browser-support img {display: block; margin: 0 auto}
.browser-support li {display: table-cell; vertical-align:top; text-align: center;font-size:1.5em; box-sizing:border-box;padding:0 0.2em;}
</style>