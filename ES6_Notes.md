### 字符串模板 Template String
```javascript
let xxx='你好',yyy = '不好';

let printt = `今天你 ${xxx} ${yyy} 啊`
```

### Tagged Templates  带标签的模板字符串

```javascript
let xxx='你好',yyy = '不好';

let printt = kitchen`今天你 ${xxx} ${yyy} 啊`

function kitchen(strings,...values){
    console.log(strings);
    console.log(values);
}
```
输出结果strings为字符values为模板字符xxx和yyy的值

### 判断字符串是否包含
xxxx.statsWith('xxx');返回true false
同理endWith   includes

### Deafault Paramet 默认参数
```javascript
function breakfast(dessert='xx',drink='yy'){
    return '${dessert} ${drink}';
}
```
xx yy 为默认

### 展开操作符Spread ...
展开数组 ['1','2']变为1 2
用法用例 console.log(...array);

### 剩余操作符 ...
```javascript
function breakfast(dessert,drink,...foods){
    console.log(dessert,drink,foods);
}
breakfast('1','2','3','4');
```
输出为1 2 ['3','4'];
多余的参数将以数组的形式放在foods数组里；

### 函数名字
xxx.name

###  箭头函数 Arrow Functions
```javascript
let breakfast = dessert =>dessert;

var breakfast = function breakfast(dessert){
    return dessert;
}
```
上述两种定义breakfast方法是一样的
方法一中的dessert为传入参数如有多个参数可以写为(param1,param2)=>{
    操作;
}
### 对象属性名
```javascript
let food = {};

food.dessert = 'xxx';
food['hot drink'] = 'xxx';// 带空格的属性名
```

### 对比是否相等
Object.is(param1,param2);

### 对象属性复制
```javascript
let breakfast = {};

Object.assign(
breakfast,
{
    xx:'xx';
}
)
```
第一个参数为赋值的目标
第二个参数是赋值的值

### Object.setPrototypeOf 改变prototype

Object.setPrototypeOf(需要改变的方法名,改变其对象);

### __proto__
let xxx  = {
    __proto__:xxxxx(对象名);
}
OR
xxx.__proto__=xxxxx;

### 迭代器
迭代器是一个伴随着迭代器模式（Iterator Pattern）而生的抽象概念，其目的是分离并统一不同的数据结构访问其中数据的方式，从而使得各种需要访问数据结构的函数，对于不同的数据结构可以保持相同的接口。

#### 下面是一段ES5的语法创建的迭代器
```javascript
function createIterator(items) {
    var i = 0;
    return {
        next: function() {
            var done = (i >= items.length);
            var value = !done ? items[i++] : undefined;
            return {
                done: done,
                value: value
            };
        }
    };
}
var iterator = createIterator([1, 2, 3]);
console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 2, done: false }"
console.log(iterator.next()); // "{ value: 3, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
// 之后的所有调用
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

在上面这段代码中，createIterator()方法返回的对象有一个next()方法，每次调用时，items数组的下一个值会作为value返回。当i为3时，done变为true；此时三元表达式会将value的值设置为undefined。最后两次调用的结果与ES6迭代器的最终返回机制类似，当数据集被用尽后会返回最终的内容

　　上面这个示例很复杂，而在ES6中，迭代器的编写规则也同样复杂，但ES6同时还引入了一个生成器对象，它可以让创建迭代器对象的过程变得更简单。
　　
### 生成器 Generators
生成器是一种返回迭代器的函数，通过function关键字后的星号(*)来表示，函数中会用到新的关键字yield。星号可以紧挨着function关键字，也可以在中间添加一个空格
```javascript
// 生成器
function *createIterator() {
    yield 1;
    yield 2;
    yield 3;
}
// 生成器能像正规函数那样被调用，但会返回一个迭代器
let iterator = createIterator();
console.log(iterator.next().value); // 1
console.log(iterator.next().value); // 2
console.log(iterator.next().value); // 3
```
在这个示例中，createlterator()前的星号表明它是一个生成器；yield关键字也是ES6的新特性，可以通过它来指定调用迭代器的next()方法时的返回值及返回顺序。生成迭代器后，连续3次调用它的next()方法返回3个不同的值，分别是1、2和3。生成器的调用过程与其他函数一样，最终返回的是创建好的迭代器

　　生成器函数最有趣的部分是，每当执行完一条yield语句后函数就会自动停止执行。举个例子，在上面这段代码中，执行完语句yield 1之后，函数便不再执行其他任何语句，直到再次调用迭代器的next()方法才会继续执行yield 2语句。生成器函数的这种中止函数执行的能力有很多有趣的应用

　　使用yield关键字可以返回任何值或表达式，所以可以通过生成器函数批量地给迭代器添加元素。例如，可以在循环中使用yield关键字。
　　
```javascript
function *createIterator(items) {
    for (let i = 0; i < items.length; i++) {
        yield items[i];
    }
}
let iterator = createIterator([1, 2, 3]);
console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 2, done: false }"
console.log(iterator.next()); // "{ value: 3, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
// 之后的所有调用
console.log(iterator.next()); // "{ value: undefined, done: true }"
```
在此示例中，给生成器函数createlterator()传入一个items数组，而在函数内部，for循环不断从数组中生成新的元素放入迭代器中，每遇到一个yield语句循环都会停止；每次调用迭代器的next()方法，循环会继续运行并执行下一条yield语句


### 类
```javascript
class Xxx{
    constructor(param1,...){
        this.xxx = xxx;
        this.yyy = [];
    }
    
    get zzz(yyy){
        return yyy;
    }
    
    set zzz(yyy){
        this.yyy.push(yyy);
    }
    
    xxx(){
        console.log(x);
    }
}

let xxx1 = new Xxx(xxx);
xxx1.xxx();
```
以上是一个简单的实例

### get & set 用例如上

### static 静态类
静态类不需要实例化类
不需要new
```javascript
class Xxx{
    constructor(param1,...){
        this.xxx = xxx;
        this.yyy = [];
    }
    
    
    static xxx(){
        console.log(x);
    }
}

Xxx.xxx();//不需要new
```


### 继承 extend
```javascript
class Person{
    construcor(name,birthday){
        this.name = name;
        this,birthday = birthday;
    }
    
    intro(){
        return '${this.name} ${this.birthday}';
    }
}

class Xxx extends Person{
    constructor(name,birthday){
    super(name,birthday);//不需要再次写构造函数。
}
```

### Set
```javascript
let xxx = new Set();
xxx.add('x');//添加方法
xxx.add('x');//不能重复
console.log(xxx.size);//输出长度
console.log(xxx.has('y');//判断是否有y
//删除方法
xx.delete('x');
//循环处理
xxx.forEach(xx=>{
    console.log(xx);
});
//清除Set内的内容
xxx.clear();
```

### Map
```javascript
let xxx = new Map();
let yyy = [],zzz = function(){},aaa='abc';
xxx.set(yyy,'a');//往xxx内添加一个yyy的值为a
//同理zzz和aaa
console.log(xxx.size);//输出长度
console.log(xxx.get(yyy));//可以得到yyy；
//删除方法
xx.delete('x');
console.log(xxx.has('y');//判断是否有y
//循环处理
xxx.forEach((value,key)=>{
    console.log('${key}=${value}');
});
//清除Map内的内容
xxx.clear();
```
方法大致和Set相似

### Module

```javascript
export{
    xxx;
}
```

在需要导入的页面：
```javascript
import {xxx} form 'url';
```
或者
```javascript
import * as yyy from 'url';
console.log(yyy.xxx);
```

### 默认导出
```javascript
export default{
    
}
//需要导入的页面
import x(随意) form 'url'//此时的x就是默认导出的东西
```