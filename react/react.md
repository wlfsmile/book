### React

#### React的简介及特点
> react不是一个框架，只是一个类库，只提供UI（view）层面的解决方法 

#### 虚拟DOM 
在react中，render执行的结果得到的并不是真正的DOM节点，仅仅是轻量级的JavaScript对象，也称作虚拟DOM。而虚拟DOM的核心思想就是最小化的DOM操作。

**一个对象：**虚拟DOM是一个基本的JavaScript对象
**两个前提：**JavaScript很快，直接操作DOM很慢
**三个步骤：**生成虚拟树，对比两棵树的差异，更新视图

##### 三个步骤
1. 生成虚拟树
**DOM节点：**节点类型，节点属性，子节点
使用JavaScript简单的实现一颗DOM树，然后给节点渲染方法，实现虚拟节点到真实DOM的转化

<img src="https://cloud.githubusercontent.com/assets/8521368/25689709/3fe7eaa8-30bd-11e7-8e00-45ec2e40726e.png" aligin="center">

2. 对比两棵树的差异(diff算法)
> 虚拟DOM只会对同一层级的元素进行对比

<img src="https://cloud.githubusercontent.com/assets/8521368/25689831/fe51cf0e-30bd-11e7-92fc-6fc69bcab700.png" aligin="center">

**2.1深度优先遍历，记录差异**
对新旧两棵树进行深度优先的遍历，这样每个节点都会有一个唯一的标记。并且每遍历一个节点就把该节点和新的树进行对比，如果有差异的话就记录到一个对象里面

<img src="https://cloud.githubusercontent.com/assets/8521368/25689882/5decd9ea-30be-11e7-8252-b164d6a642ae.png" aligin="center">

如，上面的div和新的div有差异，当前的标记是0，所以patches[0]=[{difference},{difference},...],同理p是patches[1]，以此类推。当整棵树便利完了之后，就可以获得一个完整的差异对象。

**2.2差异类型**
+ 替换
+ 增加/删除子节点
+ 修改节点属性
+ 文本内容改变

3. 更新视图
在第二步中可以得到整棵树的差异，就可以根据差异的不同类型，对DOM进行针对性的更新

**更新视图的方法**
+ `replaceChild()`
+ `appendChild()/removeChild()`
+ `setAttribute/removeAttribute()`
+ `textContent`

<img src="https://cloud.githubusercontent.com/assets/8521368/25689889/6922dddc-30be-11e7-882d-94c47f9c6390.png" aligin="center">

#### React组件
> 一个 React 应用就是构建在 React 组件之上的
**react组件的构成：**属性（props）、状态（state）、生命周期方法
**过程：**react组件可以接收参数，也可能有自身状态，一旦接收到的参数或者自身状态有所改变，react组件就会执行相应的声明周期方法，最后渲染

##### React组件的构建方法
1. **React.createClass：**传统，兼容性最好。react官方唯一指定的组件写法。调用几次组件，就会创建几次组件实例
2. **ES6 classes：**通过ES6标准的类语法的方式进行构建。也会创建组件实例
3. **无状态函数：**只传入props和context，不存在state，也没有生命周期，不会创建新实例，创建时始终保持一个实例，避免了不必要的检查和内存分配，做到了内存优化

##### React数据流
在react中，数据是自顶向下单向流动的，级从父组件到子组件

1. state
> state 是组件的当前状态，可以把组件简单看成一个“状态机”，根据状态 state 呈现不同的 UI 展示。
一旦状态（数据）更改，组件就会自动调用 render 重新渲染 UI，这个更改的动作会通过 this.setState 方法来触发。

setState是一个异步方法，一个生命周期内所有的setStata方法会合并操作

2. props
props是react用来让组件间相互联系的一种机制，类似于参数。props本身是**不可变的**。

2. props

#### 参考资料
[理解 Virtual DOM](https://github.com/y8n/blog/issues/5)
[深度剖析：如何实现一个 Virtual DOM 算法](https://github.com/livoras/blog/issues/13)
[图的遍历之 深度优先搜索和广度优先搜索](https://www.cnblogs.com/skywang12345/p/3711483.html)