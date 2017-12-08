### JavaScript——Ajax

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

#### 同步和异步
##### 同步
+ 