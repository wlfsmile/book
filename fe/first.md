#### first

1. css的动画属性
+ transform 转换
+ transaction 过渡
+ animation 动画

2. ajax创建过程
**创建XMLHttpRequest对象，也就是创建一个异步调用对象**
**创建一个新的HTTP请求，并制定该HTTP请求的方法、URL及验证信息**
使用open()方法，XMLHttpRequest.open(method,URL,flag)
+ method:指定的HTTP的请求方法
+ URL：请求的地址
+ flag：布尔值，表示是否使用异步方式

**设置响应HTTP请求状态变化的函数（readyState,status）**
+ 0：未初始化状态，还未调用open()方法
+ 1：初始化状态，已经调用open()方法，正在发送请求
+ 2：(发送)send()方法完成，尚未收到响应
+ 3：(接收)已经接收到部分响应数据
+ 4：(完成)响应数据接收完成，可以在客户端使用

如果readyState属性值等于4，表示异步调用过程完毕，但是并不代表异步调用成功，所以通过status属性值判断，只有该属性值为200，代表调用成功

**发送HTTP请求**
通过send()方法，将HTTP请求发送到Web服务器上去

**获取异步调用返回的数据**

3. 箭头函数与普通函数的区别
+ 箭头函数是匿名函数，不能作为构造函数，不能使用new操作符
+ this，普通构造函数this指向一个新对象，而箭头函数则会捕获其所在上下文的this值，作为自己的this
+ 箭头函数不绑定arguments
+ 箭头函数使用的时候没有定义this绑定

4. 深拷贝与浅拷贝，以及如何实现深拷贝
**浅拷贝：**拷贝原对象的引用
**深拷贝：**拷贝出一个新的实例，新的实例和之前的实例互不影响
**深拷贝的实现：**
+ 使用jQuery的extend：jQuery.extend第一个参数可以是布尔值，用来设置是否深度拷贝的
+ 使用JSON.stringify以及JSON.parse：JSON对象parse方法可以将JSON字符串反序列化成JS对象，stringify方法可以将JS对象序列化成JSON字符串
+ 递归实现

```js
function deepCopy(initalObject,finalObject){
  var finalObject = finalObject || {}
  for(var key in initalObject){
    if(typeof initalObject[key] === "object"){
      finalObject[key] = (initalObj[key].constructor === Array) ? [] : {}  // 区分是数组还是对象
      deepCopy(initalObject[key],finalOjbect[key]) //调用自身函数方法
    }else{
      finalObject[key] = initalObject[key]
    }
  }
  return finalObject
}

```