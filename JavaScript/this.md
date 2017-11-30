### JavaScript——this

#### this情况
+ 在函数体外，this指的就是window对象
+ 在函数体内，谁调用函数this就指向谁
+ 在构造函数中，this指的是新创建的对象
+ 在html标签中，this指的是当前的这个标签元素
+ 在ES6中，对于箭头函数，要看它在哪里创建的，和当前函数的作用域

#### call与apply
+ apply和call，都是对象本身没有某个属性或者方法，去引用其他对象的属性或方法，也就是说两者都可以改变this的属性

##### 差异
apply(this的指向，数组/arguments)
call(this的指向，参数1，参数2，参数3)