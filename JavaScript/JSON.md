### JavaScript——JSON

> JSON是一种使用JavaScript对象和数组直接量编写轻量级且易于解析的数据结构。

#### JSON对象方法
##### JSON.stringify()
+ 将JavaScript对象序列化为JSON字符串

```js
var wlf = {
    name: 'wlf',
    age: '20',
    sex: '女'
};

JSON.stringify(wlf); //{"name":"wlf","age":"20","sex":"女"}
```

+ 过滤结果（第二个参数）
```js
var wlf = {
    name: 'wlf',
    age: '20',
    sex: '女'
};

JSON.stringify(wlf,["name","age"]); //{"name":"wlf","age":"20"}
```

+ 字符串缩进（第三个参数，可为数值和字符串）,控制结果中的缩进和空白格
```js
var wlf = {
    name: 'wlf',
    age: '20',
    sex: '女'
};

JSON.stringify(wlf,null,4); 
/*
{
    "name": "wlf",
    "age": "20",
    "sex": "女"
}
*/
JSON.stringify(wlf,null,"--");
/*
{
--"name": "wlf",
--"age": "20",
--"sex": "女"
}
*/
```

+ toJSON
> 有时候，JSON.stringify()不能满足对某些对象进行自定义序列化的需求，这时候就可以给对象定义toJSON()方法，返回其自身的JSON数据格式

```js
var wlf = {
    name: 'wlf',
    age: '20',
    sex: '女',
    toJSON:function(){
       return this.name;
    }
};
console.log(JSON.stringify(wlf)) //"wlf"
```

##### JSON.parse()
+ 将JSON数据解析为JavaScript对象

```js
var wlf = {
    name: 'wlf',
    age: '20',
    sex: '女'
};

var jsonText = JSON.stringify(wlf);

var wlfCopy = JSON.parse(jsonText);
```