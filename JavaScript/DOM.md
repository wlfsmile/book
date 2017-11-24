### JavaScript——DOM与DOM优化

###DOM

#### nodeType属性（表明节点类型12个）
+ element
+ attribute
+ text
+ cdata section
+ comment
+ document等
 
#### 操作节点（增、删、移动、创建、复制、查找等）
##### 创建
+ createDocumentFragment() //创建一个DOM片段
+ createElement() //创建一个具体的元素
+ createTextNode() // 创建一个文本节点

##### 添加、移除、替换、插入
+ appendChild()
+ removeChild()
+ replaceChild()
+ insertBefore() //在已有的子节点前插入一个新节点

##### 查找
+ getElementByTagName() // 通过标签名
+ getElementByName() //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
+ getElementById() //通过元素id，唯一性
+ querySelector() //返回匹配的第一个元素
+ querySelectorAll() //返回一个NodeList的实例

##### 复制
+ cloneNode()

#### 由各节点构成的DOM
+ node：抽象表示文档中一个独立的部分
+ document：表示整个文档，是一组分层节点的根节点
+ element：表示文档中所有的HTML或XML元素
+ nodeType的其他

### DOM优化
