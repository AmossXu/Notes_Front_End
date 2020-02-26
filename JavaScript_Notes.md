## JavaScript常用面试

### 数据类型
####usbno
- undefined
- string
- boolean
- number
- object

typeof()函数查看数据类型

### NaN  Not a number

- isNaN() 来检查是否是number
- NaN跟谁都不相等


### JS 作用域
- 全局作用域
- 函数作用域
- ES6块级作用域  let

ES6之前没有块级作用域  这会导致函数作用域覆盖了全局作用域；亦或者循环中的变量泄露为全局变量。

### 作用域链
子函数没有的找父级函数

```javascript
var a = 666;
function show(){
    var a = 12;
    function show2(){
        console.log(a);
    }
}
show();
```
打印出来为12

### 变量提升

### 严格模式
"use strict" 严格模式下不允许使用未定义的变量

### IIFE 匿名函数自执行（立即调用的函数）Immediately-Invoked Function Expression
- 处理变量污染形成函数作用域
```javascript
(function{
    console.log(a);
)();
```

### 闭包 closure
```javascript
function show(){
    var num = 666;
    return fuction(){
        console.log(num);
    }
}
var show2 = show();
show2();//上面的num还能用在这里 
```

```javascript
var arr = [];
for(var i =0;i<3;i++){
    arr[i] = function(){
        return i;
    }
}
console.log(arr[0]());// 输出为3
```
使用let可以解决 或 闭包

### DOM事件流
一般都是小到大（div->body)

### js里最灵活的   this
- 浏览器下
    - 全局this：Window
    - 函数里的this：
        - 直接调用：Window
        - 'use strict' : undefined
        - 解决：
                1.使用let
                2.箭头函数
                3.bind call apply
        - 函数内有函数：Window 
    - 对象下面：当前对象
    
### call apply bind

- call(代替this,parameter1,parameter2...) 
- bind()//不执行 加参数
- apply()//和call()几乎一样后面是[]数组

### js面向对象编程
创建对象三种方式
1. 单体模式 var xxx = {xxx:xxx,xxx:xxx}
2. 原型模式 属性放在构造函数里
```javascript
function Teacher(name,age){
    this.name = name;
    this.age = age;
}
Teacher.prototype.showName = function(){
    return this.name;
}
var xxx = new  Teacher('xxx',23);
xxx.showName();
```
3. 伪类模式  Class
```javascript
class Teacher{
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
    showName(){
        return this.name;
    }
}
var xxx = new  Teacher('xxx',23);
xxx.showName();
```

### js 面向对象-继承

- 单体模式
```javascript
var xxx = {
    name:'xxxx',
    age:13,
    showName:function(){
        return this.name;
    }
};

var student = Object.create(Teacher);
```
- ES6 类模式
```javascript
class Person(){
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
    showName(){
        return this.name;
    }
}
class Teacher extends Person{
    constructor(name,age,job){
        super(name,age);
        this.job = job;
    }
    showinfo(){
        return this.job+super.showName();
    }
}
```

### 数据处理和结束语


  - JSONP原理
     1.  js是可以跨域的
     2.  服务器返回的数据，show([12,3]);
     3.  本地方法定义
     4.  jsonp只能get
  - CROS
     1. 必须服务器端配合