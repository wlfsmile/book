+ Doctype作用？严格模式与混杂模式的区别？
```
声明位于HTML文档中的第一行，用于告知浏览器的解析器用什么标准解析这个文档
```
+ 行内元素，块状元素，空（void）元素
```
(1)行内：a b span img input select strong...
(2)块状：div ul ol li dl h1 p ...
(3)空元素：br hr img link input meta

```
+ href src @import的区别
```
(1)href和src
href:超文本引用，用来链接引用外部资源。
src:引入资源，引入内容是页面必不可少的一部分。
(2)link 和 @import（外部引用css的方式）
link引用css时，在页面中载入时同时载入，@import需要网页完全载入以后加载
link是XHTML标签，无兼容问题，@import低版本浏览器不支持
link支持使用JavaScript操作DOM改变样式，@import不支持
```
+ 对浏览器内核的理解
```
+ 渲染引擎和JS引擎
(1)渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。
(2)JS引擎：解析执行JavaScript来实现网页的动态效果
最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。
```
+ 常见的浏览器内核
```
Trident:IE等
Gecko:Firefox等
Webkit:Chrome、Safari等
Presto:Opera，不过现在Opera使用的是Webkit内核
Blink:由谷歌开发，现在也是chrome的内核，实际上是由Webkit衍生而来
```
+ HTML语义化
```
根据内容的结构化，选择合适的标签，便于开发者阅读和写出更优雅的代码的同时让浏览器 的爬虫和机器很好的解析
语义化原因
(1)在没有CSS的情况下也容易阅读
(2)提高用户体验：例如alt、title等解释图片和名词信息
(3)有利于SEO：搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重
(4)便于其他设备解析
(5)便于开发和维护
```
+ cookie、session、sessionStorage、localStorage的区别
```

```