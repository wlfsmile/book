### JavaScript——Ajax以及跨域

### Ajax

> 全称——asynchronous JavaScript and xml,主要是用来实现客户端与服务器端的异步通信效果，实现页面的局部刷新。

#### 创建过程
```js
var xhr = null; //创建对象
if(window.XMLHttpRequest){
    xhr = new XMLHttpRequest()
}else{
    xhr = new ActiveXObject("Microsoft.XMLHTTP");
}

xhr.open("方式","URL","是否异步"); //初始化信息，启动一个请求以备调用，并不会真正发送请求
xhr.setRequestHeader("Header":"Value"); //设置http头信息
xhr.send(null); //发送请求

xhr.onreadystatechange = function(){ //onreadystatechange用来检测每次变化后的readyState的值。确保跨浏览器的兼容性
    if(xhr.readyState == 4){ //readyState表示请求/响应过程的当前活动阶段 =4表示已经接收到全部到相应数据，可以在客户端使用了
        if((xhr.status  >= 200 && xhr.status < 300)||xhr.status == 304){
            alert(xhr.responseText);
        }else{
            alert("Request was unsuccessful"+xhr.status);
        }
    }
}

``` 

+ 创建XMLHttpRequest对象,也就是创建一个异步调用对象
+ 创建一个新的HTTP请求,并指定该HTTP 请求的方法、URL 及验证信息
+ 设置响应HTTP请求状态变化的函数
+ 发送HTTP请求
+ 获取异步调用返回的数据
+ 使用JavaScript和DOM实现局部刷新

### 跨域
#### 同源策略
> 同源策略是对XHR的一个主要约束，它为通信设置了```相同的域、相同的端口、相同的协议```这一限制，试图访问上述限制之外的资源，都会引发安全错误，除非采用被认可的跨域解决方案。

+ DOM同源策略：禁止对不同源页面DOM进行操作。（iframe，不同域名的iframe是限制互相访问的）
+ XMLHttpRequest同源策略：禁止使用XHR对象向不同源的服务器地址发起HTTP请求

#### 解决方法
##### 跨域资源共享（CORS）
推荐阮一峰的[跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)
+ 需要浏览器和服务器同时支持

###### 
##### JSONP
###### 基本原理
通过动态创建script标签，然后利用src属性进行跨域。  
js直接用XHR请求不同域的资源是不行的，但是却可以在页面上引入不同域上的js脚本文件
```js
<script>
    function dosomething(jsondata){
        //处理获得的json数据
    }
</script>
<script src="http://wlf.com/data.php?callback=dosomething"></script> //http://wlf.com/data.php返回的不许说一个能执行的js文件
```
jQuery
```js
<script>
    $.getJSON('http://wlf.com/data.php?callback=?',function(jsondata){//jquery会自动生成一个全局函数来替换callback=?中的问号，之后获取到数据后又会自动销毁
        //处理获得的json数据
    })
</script>
```

##### 服务器代理
> 浏览器有跨域限制，但是服务器不存在跨域问题，所以可以由服务器请求所要域的资源再返回给客户端。

##### document.domain来跨子域
+ 针对主域名相同，子域名不同的情况（iframe）
+ 一个页面框架（iframe／frame）之间（父子或同辈），是能够获取到彼此的window对象的，但是这个 window 不能拿到方法和属性

```js
//https://www.qiutc.me/a.html
<script>
    function onLoad(){
        var iframe = document.getElementById('iframe');
        var iframeWindow = iframe.contentWindow; // 这里可以获取 iframe 里面 window 对象，但是几乎没用
        var doc = iframeWindow.document; // 获取不到
    }
</script>
<iframe src="https://www.qiutc.me/b.html" onload="onLoad()"></iframe>
```
使用后
```js
//https://www.qiutc.me/a.html
<script>
    document.domain = 'qiutc.me';
    function onLoad(){
        var iframe = document.getElementById('iframe');
        var iframeWindow = iframe.contentWindow; // 这里可以获取 iframe 里面 window 对象，并且得到方法和属性
        var doc = iframeWindow.document; // 获取到
    }
</script>
<iframe src="https://www.qiutc.me/b.html" onload="onLoad()"></iframe>

//https://www.qiutc.me/b.html
<script>
    document.domain = 'qiutc.me';
</script>
```

##### window.name
> window对象有个name属性，该属性有个特征：即在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个window.name的，每个页面对window.name都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的，并不会因新页面的载入而进行重置。

##### postMessage
> ```window.postMessage(message(发送的消息，字符串), targetOrigin(接收消息的那个window对象所在的域))``` 方法是html5新引进的特性，可以使用它来向其它的window对象发送消息，无论这个window对象是属于同源或不同源。

```js
// 主页面  blog.qiutc.com
<script>
    function onLoad() {
        var iframe =document.getElementById('iframe');
        var iframeWindow = iframe.contentWindow; //获取window对象
        iframeWindow.postMessage("I'm message from main page."); //想不同域的页面发送消息
    }
</script>
<iframe src="https://www.qiutc.me/b.html" onload="onLoad()"></iframe>

// b 页面
<script>
    window.onmessage = function(e) { //注册message事件接收消息
        e = e || event;  //获取事件对象
        console.log(e.data);  //通过data属性得到传送的消息
    }
</script>
```