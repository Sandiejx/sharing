# 3D transforms in CSS3

---

## About Me

@state: blue, @fragment

* **Sandy**
* 奇舞团前端
* 支持问答项目组

---

## 2D变换函数

@state: blue, @fragment

* rotate
* scale
* skew
* translate
* matrix

---

## demos

@state: black, @fragment

<iframe src="http://jsbin.com/nafoxu/307/embed?output" class="" id="" style="border: 1px solid rgb(170, 170, 170); width: 900px; min-height: 500px;"></iframe>


---

## 3D变换函数

@state: black, @fragment

* 3D位移 : translateZ() 和 translate3d()
* 3D旋转 : rotateX()、rotateY()、rotateZ() 和 rotate3d()
* 3D缩放 : scaleZ() 和 scale3d()
* 3D矩阵 : matrix3d()

---

## 3D geometric transforms

<iframe src="http://jsbin.com/dudojo/199/embed?output" class="" id="" style="border: 1px solid rgb(170, 170, 170); width: 900px; min-height: 600px;"></iframe>

---

## perspective

<iframe src="http://jsbin.com/dudojo/195/embed?output" class="" id="" style="border: 1px solid rgb(170, 170, 170); width: 900px; min-height: 600px;"></iframe>

```css
-webkit-perspective: 1000px;
```

---

## transform-style属性

@state: black, @fragment

<iframe src="http://jsbin.com/saxem/100/embed?output" class="" id="" style="border: 1px solid rgb(170, 170, 170); width: 900px; min-height: 600px;"></iframe>

```css
-webkit-transform-style: flat;
```

---

## transform-style属性

@state: black, @fragment

<iframe src="http://jsbin.com/yolix/197/embed?output" class="" id="" style="border: 1px solid rgb(170, 170, 170); width: 900px; min-height: 650px;"></iframe>

```css 
-webkit-transform-style: preserve-3d;
```

---

## 分析各个面

demo -> color_cube.html

<iframe src="http://jsbin.com/xoliza/20/embed?output" class="" id="" style="border: 1px solid rgb(170, 170, 170); width: 900px; min-height: 650px;"></iframe>

---

## magic cube

<iframe src="http://jsbin.com/yozihi/6/embed?output" class="" id="" style="border: 1px solid rgb(170, 170, 170); width:900px; min-height: 700px;"></iframe>

---

@fragment

## 总结

* 2D几何变换
* 3D几何变换
* 透视 
* perspective: 1000px;
* 变换类型 
* transform-style: flat;
* transform-style: preserve-3d;

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
