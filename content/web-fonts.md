# Web Fonts 介绍

---
## 问柏盼

* unicode-range
* why you`ll love GitHub
* http://font.qiwoo.org/
* 在线制作iconfont的几个网站链接

---

## About Me

@state: blue, @fragment

* **Sandy**
* 奇舞团前端
* 支持问答项目组

---

## Web Fonts 简介

---

## 什么是Web Fonts

@state: black, @fragment

* 引用在线字体
* css3
* @font-face

---

## Web Fonts 的优点

@state: black, @fragment

* 放⼤大缩⼩小不失真
* 大小，颜色可以在css中设置，配合css3动画效果更佳
* 可以多次复用

[Demo] http://jsbin.com/gababa

---

## @font-face

@state: black, @fragment

@font-face 不同于其他 CSS 规则是选择器,⽽而是描述⼀一个 Web Font

```css
@font-face {
    descriptor: value;
    descriptor: value;
    ...
}
```

---

## font-family & src

```css
@font-face {
    font-family: 'MyFontFamily';
    src: local(MyFontFamily),
    url('font.eot?#iefix') format('embedded-opentype'),
	/*IE6+*/
	url('font.woff') format('woff'),
	url('font.ttf')  format('truetype'),
	url('font.svg#svgFontName') format(‘svg');
}
```

---

## unicode-range

```css
@font-face {
    font-family: 'MyFontFamily';
    src: url('font1.ttf')  format(‘truetype');
    unicode-range: U+2E80-FFFF, U+00-0F;
}

@font-face {
    font-family: 'MyFontFamily';
    src: url('font2.ttf')  format(‘truetype');
    unicode-range: U+00F-FFF;
}
```

---

## @font-face 属性

@state: black

* font-family
* src
* font-style 
* font-weight 
* font-stretch 
* unicode-range 
* ...

---

## 浏览器兼容性

@state: black, @fragment

* IE5.5~IE8,IE9+
* Firefox 3.5+
* Chrome,Safari,Opera
* iOS Safari
* Android Browser 2.1+
* Opera Mobile
* Chrome for Android 
* Firefox for Android 
* IE Mobile
* UC

---

## Web Fonts 包括的⼏几种字体

@state: black, @fragment

TrueType(.ttf), OpenType(.ttf, .otf) 
Embedded OpenType(.eot) //IE最早支持
SVG Font(.svg, .svgz)
Web Open Font Format(.woff, .woff2)

---

## 浏览器对几种字体的支持情况

图片。。。传上图床

---

## Web Fonts 两方面的应用

* 作为字体使用
* 作为icon使用

---

## 使⽤ Web Fonts 做字体的好处

@fragment

* 页⾯面美观、⾃自动适配⾼高清屏(使⽤用户看到的效果和设计⼀一致,更趋向于设计图的效果)
* 显⽰示⽣生僻字
* ⽀支持选中、复制、查找、修改⽅方便
* 对搜索引擎、翻译⼯工具、缩放、⽆无障碍设备原⽣生⽀支持

---

## 使⽤ Web Fonts

@fragment

### 本地使用

* 将拿到的字体转换成兼容浏览器的多个版本
* 通过 CSS 定义 @font-face 引⽤用对应的字体

### 在线字体服务
* [Google Fonts] https://www.google.com/fonts
* [Just Font] http://cn.justfont.com/
* [有字库	] http://www.youziku.com/


---

## 引用 Web Fonts

@fragment

```html
<h2 class=“title”>我是使用了 Web Fonts 的标题</h2>
```

```css
.title {
    font-family: ‘myFontFamily’;
}
```

---

## 作为字体使用的一些问题

@fragment

* 版权问题（盗版、授权费、授权费）
* 中文字体的问题（文件庞大-好几MB，字体转换）

---


## 字体压缩转换工具

@fragment

* 字体⼦子集 (embedded subset)
* 字蛛 http://font-spider.org/
* 显⽰示⽣生僻字
* http://font.qiwoo.org/
* Fontforge、ttf2eot、sfnt2woff、woff2_compress

---

## 作为 Icon 使用

---


## Icon Fonts 在线库

@fragment

https://icomoon.io/app/ 
http://fortawesome.github.io/Font-Awesome/icons/ 
http://iconfont.cn/
http://fontello.com/

---

## Icon Fonts 的使用

```html
<h2><span class=“icon icon-name”></span>IconFonts</h2>
```

```css
.icon {
     font-family: 'fonticon';
     speak: none;
     user-select: none;
}
 .icon-name:before {
     content: "\e900";
}
demo(jsbin) cart
```

---

## 自己制作的Icon

### 设计师提供⽮矢量图 - SVG 格式
* 对齐到像素
* 曲线闭合
* 色彩填充

### 在线导⼊,制作
* Icomoon
* Iconfont
* foontello

---


@state: blue

## Thanks

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
