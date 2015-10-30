---
title: '保持footer在页面最底部'
description: 'keep footer always at bottom of page'
tag: html,css,layout
date: 2015-10-30 21:00
id: SJ1jwLNl
---

页面的footer栏, 需要始终保持在整个页面的最底部:

* 如果body内容不足一个屏幕, footer在最底部
* 如果body内容超过一个屏幕, footer依然保持在整个页面的最下面

![](http://tankywoo-wb.b0.upaiyun.com/bottom-footer-the-problem.gif)

<small>[图片来源][1]</small>

---

参考1: [How to keep footers at the bottom of the page][1]

HTML:

	<div id="container">
	  <div id="header"></div>
	  <div id="body"></div>
	  <div id="footer"></div>
	</div>

CSS:

	html,
	body {
	  margin:0;
	  padding:0;
	  height:100%;
	}
	#container {
	  min-height:100%;
	  position:relative;
	}
	#header {
	  background:#ff0;
	  padding:10px;
	}
	#body {
	  padding:10px;
	  padding-bottom:60px;   /* Height of the footer */
	}
	#footer {
	  position:absolute;
	  bottom:0;
	  width:100%;
	  height:60px;   /* Height of the footer */
	  background:#6cf;
	}

这里注意几点:

* container 需要设置定位是relative. 否则当页面超过一个屏幕时, footer会固定在屏幕最下, 而不是页面最下.
* body 需要设置padding-bottom, footer 需要设置 height. 这也是为一个相对受限的地方. 否则 footer 会挡住 body 最下面.
* 接着反驳上面一点, 上面两条是参考链接里提到的. 其实footer不需要设置高度, 直接auto, 然后body设置的padding-bottom足够footer以及它的margin.

现在 tfcs 就是用的这个布局. 因为footer有border-top和margin, body和footer设置了padding-bottom和height, 中间会有重叠的部分.

---

参考2: [Make the Footer Stick to the Bottom of a Page][2]

HTML:

	<div id="container">
	  <div id="header"></div>
	  <div id="body"></div>
	  <div class="push"></div>
	</div>
	<div id="footer"></div>

CSS:

	* {
	  margin: 0;
	}
	html, body {
	  height: 100%;
	}
	#container {
	  min-height: 100%;
	  height: auto !important; /* This line and the next line are not necessary unless you need IE6 support */
	  height: 100%;
	  margin: 0 auto -155px; /* the bottom margin is the negative value of the footer's height */
	}
	#footer, .push {
	  height: 155px; /* .push must be the same height as #footer */
	}

这里要注意几点:

* 和上面不同, 这里的container只包裹了header和body, footer和container平级
* container的margin-bottom设置负数, 数值和footer以及push高度一致

好像我的wiki的yasimple主题用的是这种布局

---

其它参考:

* [CSS to make HTML page footer stay at bottom of the page with a minimum height](http://stackoverflow.com/questions/643879/css-to-make-html-page-footer-stay-at-bottom-of-the-page-with-a-minimum-height)
* [w3school - position属性](http://www.w3school.com.cn/cssref/pr_class_position.asp)
* [How to keep footers at the bottom of the page][1] [Demo](http://matthewjamestaylor.com/blog/bottom-footer-demo.htm)
* [Make the Footer Stick to the Bottom of a Page][2] [Demo](http://ryanfait.com/sticky-footer/)
* [How To Keep Your Footer At The Bottom Of The Page With CSS](http://www.cssreset.com/demos/layouts/how-to-keep-footer-at-bottom-of-page-with-css/)


[1]: http://matthewjamestaylor.com/blog/keeping-footers-at-the-bottom-of-the-page
     "How to keep footers at the bottom of the page"
[2]: http://ryanfait.com/resources/footer-stick-to-bottom-of-page/
     "Make the Footer Stick to the Bottom of a Page"
