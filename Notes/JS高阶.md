js高级8天

1. ES6基本语法----2天(快乐)
2. 面向对象---------3天(难,抽象----js底层)
3. 面试题------------3天(知识点的形式----难----递归,闭包,异步程序)------工作拧螺丝,面试造火箭

# day01(重要)

> 今日要点
>
> 1. 了解什么是ES6
> 2. **掌握使用let和const声明变量和常量**
> 3. **掌握模板字符串的使用**
> 4. **掌握对象、数组、字符串的解构**
> 5. **掌握使用对象简化的方式声明对象**
> 6. **掌握如何给函数设置默认参数以及函数参数的解构**
> 7. **掌握函数中rest 参数的使用**
> 8. **掌握拓展运算符的使用**

## 一、ES6介绍

我们之前学习过，Javscript分为三大部分：ECMAScript + DOM + BOM

而我们说的ES就是指 ECMAScript

![image-20210222150239675](F:\\js高阶\JS高阶.assets\image-20210222150239675.png)

ECMAScript就是一种语法标准，规定了这个语言的语法要如何书写，何种语法有何种作用。我们之前学习的很多东西都是在ES5的标准里面的。5只是ECMAScript的其中一个版本，而6也是其中一个大版本。只是ES6和ES5相差的比较大，并且也相对好用，所以企业的使用面积非常大。

ES6 既是一个历史名词，也是一个泛指，含义是 5.1 版以后的 JavaScript 的下一代标准，涵盖了 ES2015、ES2016、ES2017 等等，而 ES2015 则是正式名称，特指该年发布的正式版本的语言标准。本书中提到 ES6 的地方，一般是指 ES2015 标准，但有时也是泛指“下一代 JavaScript 语言”。

**<span style="color:orange;">也就是说从2015年以后推出的新标准，现在统称为ES6</span>**

> 扩展阅读：[ECMAScript和Javascript](https://es6.ruanyifeng.com/#docs/intro)
>
> ES6中的新语法和新特性，对于低版本的浏览器支持不友好

## 二、ES6变量声明

### 2.1、var的弊端

使用var关键字声明变量的弊端：

1、var声明的变量有预解析，造成 逻辑混乱，可以先使用，后声明

2、var可以重复定义同一个变量，逻辑错误，第二次应该是修改变量，而不是定义

3、var用在for循环条件中，造成for 循环的污染的问题

4、var 声明的变量没有块级作用域（ES5中的作用域：全局和局部）

```js
// 1、var声明的变量有解析，造成 逻辑混乱，可以先使用，后声明
// console.log(a);
// var a = 10;

// 2、var可以重复定义同一个变量，逻辑错误，第二次应该是修改变量，而不是定义
// var a = 10;
// var a = 30;
// console.log(a);

// 3、var用在for循环条件中，造成for 循环的污染的问题
// for(var i=0; i<10; i++){
//     console.log(i);
// }
// console.log("=====================");
// console.log(i);

// 4、var 声明的变量没有块级作用域（ES5中的作用域：全局和局部）
// {
//     var b = 200;
// }
// console.log(b);
```

###  2.2、let关键字

ES6推出了一个新的声明变量的关键字，它的基本使用如下：

```js
let 变量 = 值;
例如：
let age = 15;
```

**let关键字的必要性**

var关键字其实是有不少的问题的，比如var的变量会提升，提升后会造成一定的混乱，你可以在变量声明之前使用这个变量，而此时你对于这个变量是否有值是不确定的，所以var的变量提升后其实是有一定的问题的。

因此es6中为了统一并提高代码的安全性，引入了let关键字来代替var声明变量

* let声明的变量不会提升，必须要在声明后才能使用（let没有预解析）

```js
console.log(data) // Uncaught ReferenceError: Cannot access 'data' before initialization
let data = 10;
```

* let声明的变量不能重复声明

```js
let data = 10;
let data = 20; // Uncaught SyntaxError: Identifier 'data' has already been declared
```

* let声明的变量存在块级作用域

```js
if(false){
  let data = 10;
}
console.log(data) // Uncaught ReferenceError: data is not defined
```

**块级作用域**

块指的是代码块，一对 `{}` 之间就是一个代码块。

变量的有效范围只在这对 大括号 之间，就是`块级作用域`

块级作用域非常有必要：

```js
var btns = document.querySelectorAll('button')
for(var i = 0; i < btns.length; i++){
  btns[i].onclick = function(){
    console.log(i)
  }
}
```

此时我们点击按钮，输出的i不会是每个按钮对应的按钮，而是按钮的个数。就是因为for里面的变量是var声明的，没有形成块级作用域，每次访问i都是访问的全局的i。如果我要在事件里面得到按钮的索引，就需要别的方法来实现。

如果我们换成let

```js
let btns = document.querySelectorAll('button')
for(let i = 0; i < btns.length; i++){
  btns[i].onclick = function(){
    console.log(i)
  }
}
```

此时我们点击按钮，就能输出按钮对应的索引了。这是因为我们使用了let关键字，let会在{}之间形成一个块级作用域，for循环执行多少次，我们就会形成多少个块级作用域，每个i对应1个，当我们在事件里面获取i的时候，i会到事件函数的上级作用域找，刚好就是每个i对应的块级作用域。我们就简单地得到了每个按钮对应的索引。

> **所以，let的特点：**
>
> 1、let声明的变量**==没有预解析==**，不会有变量提升
>
> 2、同一作用域let不可以重复定义同一个变量
>
> 3、let用在for循环条件中，不会造成for 循环的污染的问题
>
> 4、let声明的变量有块级作用域（ES6中的作用域：全局和局部还有块级作用域）

### 2.3、const关键字

ES6中，为了让程序可以执行起来更加高效，推出了const关键字来声明一个只读的常量

常 ———— 恒常的意思 ， 意思就是永久不变。

所谓常量，就是永久不变的量。

常量具备以下特点：

1. 一旦声明就必须赋值
2. 一旦赋值就不能修改
3. 常量的作用域和let声明的变量作用域一样 块级作用域
4. 没有预解析
5. 引用类型的值可以修改

那么我们该怎么使用const关键字呢，其固定语法如下：

```js
const 常量名 = 值;
例如：
const data = 100;
```

如果我们声明了常量不赋值：

```js
const data; // Uncaught SyntaxError: Missing initializer in const declaration
```

如果我们想要修改常量

```js
const data = 100;
data = 200; // Uncaught TypeError: Assignment to constant variable
```

**<span style="color:orange;">所以当我们在一段代码中有一个数据在执行过程中不会改变，就可以使用常量来标识</span>**

const只能保证值类型的数据不能被修改，如果是引用类型则不行：

```js
const Arr = [10, 0, 30];
Arr[1] = 20;
console.log(Arr);   //[ 10, 20, 30 ]
```

> 小结：
>
> 1. 当一个数据不会变化的时候，我们就要使用const来声明
> 2. 常量的恒定不变，只是相对于值类型来说的，引用类型还是能改变其属性
> 3. [(19条消息) JavaScript 变量声明var、let、const详解_火星飞鸟的博客-CSDN博客_javascript条件声明](https://blog.csdn.net/Jack_lzx/article/details/121037556)

## 三、模板字符串

在es5中，当我们需要把多个字符串和多个变量拼接到一起的时候，写法还是比较复杂的

```js
let name = '狗蛋',age = 12,gender = '男'
let str = "大家好，我叫" + name + "，今年" + age + "岁了，我是一个" + gender + "孩子"
```

所以在es6中为了解决这个问题，提供了一种模板字符串

固定用法：

```js
`固定字符${变量或者表达式}`
```

* 在模板字符串中，可以解析 `${}` 之间的变量或者表达式
* 在整个字符串中允许换行

所以当我们在es6中拼接字符串

```js
let name = '狗蛋',age = 12,gender = '男'
let str = `大家好，我叫${name}，今年${age}岁了，我是一个${gender}孩子`
```

## 四、解构语法

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构。

目的：简化代码。

#### 4.1、对象解构

```js
let obj = {
    name: "luowowo",
    age:11,
    email:"luowowo@163.com"
};

// 取出所有属性并赋值：
// let name  = obj.name;
// let age  = obj.age;
// let email  = obj.email;

// 现在只需要(等效于上面的写法):
// 等号左边的变量要和对象里面的属性同名，否则没法解构出来
// let {name, email, age} = obj;  //{ }中的变量名和obj的属性名一致   完全解构

// 部分解构
// let {name} = obj;     // 部分解构

//解构之后重命名   
let {name:itsName} = obj;     解构之后重命名为itsName

//将现有对象的方法，赋值到某个变量
let {random}=Math;
console.log(random)//[Function: random]
```

笔记：

```js
	<script>
        var obj = {
            name: 'laji',
            age: 99,
            gender: '男'
        }

        // 取出所有的值 赋值给变量
        // 传统
        /* var name = obj.name;
        var age = obj.age;
        var gender = obj.gender;
        console.log(name, age, gender); */

        // ES6语法：解构语法
        // 对象解构：将对象中的值，全部提取出来 赋值给变量
        /*
            let {变量,变量,变量...} = 对象
            实现将对象的key的value赋值给 与key同名的变量
            就是 等号左边的变量要和对象里面的属性同名
            key和变量要同名才可以解构
        */
        // let { name, age, gender } = obj;
        // console.log(name, age, gender);
        // 1.这种将全部值取出来赋值给变量是  完全解构

        // 2.部分值赋值给变量  部分解构
        // window全局有name属性
        // console.log(name);  // 输出空的
        // 结构之后重命名：let{对象key:重命名的变量名}=obj
        // let { name: myName } = obj;
        // console.log(myName);

        // 3.解构内置对象的方法
        // let {变量} = Math内置对象   {random:fn}
        let { random } = Math;
        // console.log(random); // 输出函数体
        console.log(random()); // 调用输出随机数
    </script>
```



#### 4.2、数组解构

```js
let arr1 = [10, 20, 30];

let [a, b, c , d] = arr1;

// 完全解构
console.log(a);  //10
console.log(b);  //20
console.log(c);  //30
// 若解构不成功，变量的值就等于 undefined
console.log(d);  //undefined

// 部分解构
let [e] = arr1;
console.log(e);  //10

let [ , ,f] = arr1;
console.log(f);  //30


// 复合解构
let arr2 = [1, 2, [10, 20, 30]];
let [ j, k, [x, y, z]] = arr2;
console.log(j);  //1
console.log(k);  //2
console.log(x);  //10
console.log(y);  //20
console.log(z);  //30
```

笔记：

```js
	<script>
        // 数组解构：数组中的值赋值给变量
        // 语法：let [变量,变量,变量...] = arr;

        arr = [1, 2, 3];
        // 1.完全解构
        /* 
        let [a, b, c] = arr;
        console.log(a, b, c); */

        // 2.部分解构
        // let [c] = arr;
        // console.log(c);  // 1  这样只能取到第一位
        // 可以在前面加逗号 来控制拿到的第几个 补全 占位
        // let [, b] = arr;
        // console.log(b);  // 2
        // let [a, b, c, d] = arr;
        // console.log(a, b, c, d); // 1 2 3 undefined

        // 3.复合解构
        let arr2 = [1, 2, 3, [4, 5, 6]];
        let [a, b, c, [x, y, z]] = arr2;
        console.log(a, b, c, x, y, z); // 1 2 3 4 5 6
    </script>
```





#### 4.3、字符串解构

```js
let string1 = "xyz";

let [a,b,c] = string1;
console.log(a);  //x
console.log(b);  //y
console.log(c);  //z


string1[1] = "Y";
console.log(string1);  // xyz    无法修改
console.log(string1[1]);  // y

笔记：
// 解构字符串
let str = '我是大魔王';
console.log(str[1]);  // 是
console.log(str.length);  // 5
// 字符串有索引和长度 但是不能使用数组方法 本质上是伪数组
// 所以解构语法跟数组解构差不多
str[1] = '不是';  // 不能修改
console.log(str[1]);  // 是
```

#### 4.4、应用场景

交换两个变量的值

```js
let a = 10;
let b = 20;
[b,a] = [a,b]
console.log(a,b) // a=20,b=10
```

## 五、对象的简化写法

当我们在以前定义对象字面量的时候，如果有如下代码

```js
let name = '狗蛋',age = 12,gender = '男'
let obj = {
  name : name,
  age : age,
  gender : gender
}
```

此时我们发现obj的属性名和变量是同样的，可以在es6中简化为：

```js
let obj = {name,age,gender}
```

也就是说，**如果一个对象的属性名和外面的一个变量名同名，可以直接将变量名作为属性名，并会自动地把变量的值作为属性的值**

方法上面也可以进行简化：

```js
let name = 'andy';
let age = 12;

function fn() {
    console.log(`my name is ${this.name}`);
}

// es6 写法
 let userInfo = {
     name,
     age,
     fn
 };
console.log(userInfo);
userInfo.fn();
```

## 六、函数参数默认值和参数解构

### 6.1、函数形参的默认值

es5里面如果我们想要实现参数可以省略，我们有一个办法是这样做

```js
function add(a,b,c,d){
  a = a || 0;
  b = b || 0;
  c = c || 0;
  d = d || 0;
  return a + b + c + d;
}
```

此时我们可以把给了默认值的参数省略

```js
add(10,20) // 30
add(10,20,30) // 60
```

但是这样的做法比较麻烦，es6中提供了一种更加方便的方式，专门实现参数默认值。参数有了默认值之后就可以在调用的时候省略。

```js
funciton 函数名(参数=默认值){ // 注意当 参数 为 undefined 时 参数 赋值为 默认值
  
}
```

上面的例子就可以必成：

```js
function add(a=0,b=0,c=0,d=0){
  return a + b + c + d;
}
```

### 6.2、函数参数的解构赋值

函数参数解构

```js
 // 参数是一组有次序的值
function f([x, y, z]) { 
    console.log(x, y, z);
}
f([1, 2, 3]);
// 参数是一组无次序的值
function fn({x, y, z}) { // {x, y, z} = obj 解构
    console.log(x, y, z);
}
fn({z: 4, x: 5, y: 6});
```

### 6.3、解构赋值指定参数的默认值

```js
function func2({name, age} = {}){   //防止不传实参时候的报错
    console.log(name, age);
}
func2();   //undefined undefined
// func2(); //相当于传了一个null   {name, age}=null 就会报错
// func2({});  //不会报错，输出：undefined undefined
```

```js
function func2({name="luowowo", age=11} = {}){    //指定默认值
    console.log(name, age);
}
func2();  //luowowo 11
```

## 七、rest 参数和拓展运算符

### 7.1、rest 参数/剩余参数

arguments 对象：

```js
function fn(){
    console.log(arguments);// 伪数组
}

fn(10, 20, 30, 50, 60);
```

ES6提供了新的方法：使用rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。

注意，rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。

```js
function func( a, b ,...rest){  // 把剩余的参数都交给rest
    console.log(rest);
}

func(10, 20, 30, 50, 60);

function func2(...rest){   //rest 接收所有参数作为一个数组
    rest.forEach(function (item) {
        console.log(item);
    });
}
func2(60, 70, 80, 90);

// 报错
function f(a, ...b, c) {
  // ...
}
```

### 7.2、拓展运算符

ES6中的扩展运算符是一个非常有用的运算符号，可以用来快速展开数组，对象...

它的作用就是可以将数组或者对象展开，拆开成为一个一个单独的数据。

```js
// 快速将一个数组拆开成一个一个的元素
let arr = [1, 2, 3, 4]
console.log(...arr)
// 快速将一个对象里面的数据复制一份到一个新的对象里面
let obj = { name: '狗蛋', age: 12, gender: '男' }
console.log({id:1,birthday:'2020-02-02', ...obj})
// 将一个字符串拆开成为多个单独的字符
let str = 'abc'
console.log(...str)
```

使用场景：

```js
// 1、数组中的值作为函数参数使用
let arr1 = [10, 20, 30];

function func(a, b, c){
    console.log(a,b,c)
}

func(...arr1);  //等效于：func(10,20,30);     输出结果10 20 30

// 2、合并数组
let arr2 = [40, 50, 60];
let newArr = [...arr1,...arr2];  // 等效于 [ 10, 20, 30, 40, 50, 60 ]
console.log(newArr);    //[ 10, 20, 30, 40, 50, 60 ]

// 3、合并对象
let obj1 = {
    name:"luowowo",
    age:"11",
};
let obj2 = {
    email:"luowowo@163.com",
};
let newObj = {...obj1,...obj2}; // 等效于{ name: 'luowowo', age: '11', email: 'luowowo@163.com' }
console.log(newObj);    //{ name: 'luowowo', age: '11', email: 'luowowo@163.com' }

// 4、es6中另一个合并对象的方法
let newObj2 = Object.assign({},obj1,obj2);  // 把第二个及第二个以上的参数都合并到第1个上面去。
console.log(newObj2);   //{ name: 'luowowo', age: '11', email: 'luowowo@163.com' }
```

### 7.3、...在解构赋值中的使用

针对数组解构

```js
let [a, b, c, ...arr] = [1, 2, 3, 4, 5, 6, 7];
console.log(a, b, c, arr); // a = 1, b = 2, c = 3, arr = [4,5,6,7]
```

按照顺序把数组里面的元素解构到等号左边的变量里面，当左边的变量不够，会把剩下的数据放到arr这个数据里面，此时arr是就一个新的数组。

解构字符串

```js
let str = "abcde";
let [a, b, c, ...strArr] = str;
console.log(a, b, c, strArr); // a = 'a',b='b',c='c',strArr=['d','e']
```

## 八、作业

1. 【黄金】——必须完成
   1. ES6课堂代码写三遍(包含课堂写的)+**总结**
   2. bootstrap项目写两遍
   3. 页面嵌套案例写三遍
   4. jQuery阶段总结
2. 【铂金】使用ES6语法改造之前学过的案例（基础和进阶）
3. 【钻石】预习后面的内容



# day02-ES6

> 今日要点
>
> 1. 掌握**箭头函数**的语法
> 2. 能说出Promise出现的目的
> 3. 掌握**Promise的基本语法**
> 4. 掌握如何在then方法和catch方法里面得到参数
> 5. 掌握then的链式调用
> 6. 掌握Promise的all方法和race方法的使用
> 7. **掌握async/await的用法**

## 一、箭头函数

### 1.1、基本语法

ES6 允许使用 “箭头”（=>）简化函数的定义。

箭头函数本质也是函数，它出现的目的是为了让我们在使用回调函数的时候更简单

固定语法：

```js
(参数) => { 函数体 }
```

例如：

```js
// function func(){
//     console.log("hello");
// }

// 以上代码使用箭头函数书写为：
var func = () => {
    console.log("hello");
};

func();
```

**注意点：**

1. 形参个数如果为1个，可以省略小括号不写;
2. 如果函数体里面只有一个语句，可以省略大括号不写, 并且他会默认返回 => 符号后面的数据。
3. 如果函数体有多个语句，则不能省略大括号。
4. 如果函数体只有一个语句，且返回一个对象，建议是，不要写简写的方式。
5. 箭头函数不可以使用 arguments 获取参数列表，可以使用 rest 参数代替。

代码示例：

```js
// 无参数无返回
let func11 = () => console.log('func11');
func11();

// 无参数有返回

let func22 = () => 'func22';
console.log(func22());

// 有参数无返回
let func33 = x => console.log('func33', x);
func33(2);

// 有参数有返回
let func44 = (x, y) => {
    let sum = x + y; 
    return sum + 'func44';
};
console.log(func44(1, 2));
```

注意：

```js
// 如果return的是单一个对象，则需要加上大括号和return，例如：

// let func55 = (x, y) => {a:,x b:y};    //报错
let func66 = (x, y) => {
    return { a: x, b: y };
};
console.log(func66(5, 8));
```

```js
// 箭头函数不可以使用 arguments 获取参数列表，可以使用 rest 参数代替。
let func=(a,b)=>{
    console.log(a,b);
    console.log(arguments);
}
func(1,2)// 这种方式获取不到实参列表
let fun=(...value)=>console.log(value);
fun(1,2)//[ 1, 2 ]
```

使用场景（回调函数）：

```js
// 定时器中的回调函数
setInterval(() => {
    console.log("我用了箭头函数");
}, 1000);

// forEach中的回调函数
var arr = [22, 32, 11, 3, 5, 7, 88];
arr.forEach(item => console.log(item));
```

### 1.2、箭头函数中的this

this指向总结：

1. 全局使用（函数全局调用）指向window
2. 对象调用指向该对象（事件中的事件源）
3. 箭头函数没有自己的作用域，即箭头函数 this 指向其外层作用域

```js
var name = "windowName";
var obj = {
    name: "奶茶",
    fn: function () {
        console.log(this.name);
    },
};
obj.fn();

var obj2 = {
    name: "绿茶",
    fn2: () => {
        console.log(this.name);
    },
};
obj2.fn2();

//所以创建字面量对象，不适合书写箭头函数
```

在dom操作中使用箭头函数

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .box{
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>
<body>
    <div id="odiv" class="box"></div>
    <script>
      var obj = document.getElementById("odiv");
      obj.onclick = function () {
        // setTimeout(function () {
        //   console.log(this);
        //   this.style.width = "300px"; //修改不了
        // }, 1000);

        setTimeout(() => {
          console.log(this);
          this.style.width = "300px"; //修改成功
        }, 1000);
      };
    </script>
</body>
</html>
```

## 二、Promise对象

### 2.1、Promise简介

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了`Promise`对象。

**功能：避免了回调地狱，把异步代码改成调用起来像同步代码。**

所谓`Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

**一个 Promise 对象 有以下几种状态：**

- pending: 初始状态，既不是成功，也不是失败状态。
- fulfilled: 意味着操作成功完成。
- rejected: 意味着操作失败。

**`Promise`对象有以下两个特点：**

（1）对象的状态不受外界影响。`Promise`对象代表一个异步操作，有三种状态：`pending`（进行中）、`fulfilled`（已成功）和`rejected`（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是`Promise`这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。

（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。`Promise`对象的状态改变，只有两种可能：从`pending`变为`fulfilled`和从`pending`变为`rejected`。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。如果改变已经发生了，你再对`Promise`对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

> 小结：
>
> 1. Promise是一个构造函数，new出来实例对象可以帮我们解决异步操作的一些问题
> 2. 当我们遇到异步操作的时候，都可以使用Promise来加工，便于后期的代码书写

### 2.2、Promise产生背景

我们如果在进行ajax请求的时候，一个效果需要有多个请求按照一定的顺序完成，如果不使用Promise实现，做起来就容易形成回调地狱

如：

```js
$.ajax({
    url:'url1',
    success(res){
        if(res.code == 200){
            $.ajax({
                url:'url2',
                success(res){
                    if(res.code === 200){
                        $.ajax({
                            url:'url3',
                            success(res){
                                if(res.code === 200){
                                    // TODO
                                }
                            }
                        })
                    }
                }
            })
        }
    }
})
```

这样的代码是非常恶心的，将来想要维护的时候，难度非常高，所以我们不推荐这样的写法。

> 小结：Promise的出现是用来解决异步回调的多层嵌套问题的(地狱回调)

### 2.3、Promise的基本使用

Promise的执行流程

<img src="F:\\js高阶\JS高阶.assets\image-20210222180638299.jpg" alt="image-20210222180638299" style="zoom:50%;" />

Promise的基本语法：

```js
// 默认pending: 初始状态
var p=new Promise(function (resolve,reject) {
    if("操作成功"){
        resolve();//pending-->fulfilled  异步操作成功的回调函数
    }else{
        reject(); //pending-->reject     异步操作失败的回调函数
    }
})
p.then(data => {//在外面调用then处理成功的逻辑
    console.log("处理成功的逻辑");//fulfilled  
}).catch(err=>{//在外面调用catch处理失败的逻辑
    console.log("失败的逻辑");//reject
})
// then方法会在异步成功后调用，catch方法会在异步失败后调用
```

例如：

```js
let flag = false;
let p = new Promise((resolve, reject) => {
    if (flag) {
        resolve("做一件大事");
    } else {
        reject("说句对不起");
    }
});
p.then((data) => {
    console.log("我要" + data); //fulfilled
}).catch((err) => {
    console.log("我要" + err); //reject
});
```

### 2.4、使用Promise解决回调地狱

**Promise的then链式调用的特点：**
1、第一个then执行完会执行第二个then
2、then里面的函数的返回值，会被下一个then的形参接收
3、如果返回的是一个promise对象，下一个then的形参接收到的不是这个promise对象，而是这个promise对象内部调用resolve时候的实际参数

#### 2.4.1、如何解决多重请求（回调地狱）

```js
let p1 = new Promise((resolve,reject)=>{
  $.ajax({
    url:'url1',
    success(res){
      resolve(res)
    },
    error(err){
      reject(err)
    }
  })
})
let p2 = new Promise((resolve,reject)=>{
  $.ajax({
    url:'url2',
    success(res){
      resolve(res)
    },
    error(err){
      reject(err)
    }
  })
})
let p3 = new Promise((resolve,reject)=>{
  $.ajax({
    url:'url3',
    success(res){
      resolve(res)
    },
    error(err){
      reject(err)
    }
  })
})

p1.then(res1=>{
  console.log('第一个请求完成')
  return p2;
}).then(res2=>{
  console.log('第二个请求完成')
  return p3
}).then(res3=>{
  console.log('第三个请求完成')
})
```

这样我们就使用了Promise解决了回调函数里面嵌套回调函数的问题。

> 小结： 我们可以通过多个promise调用then方法来把地狱回调转化为链式编程，便于后期的维护

#### 2.4.2、简化多重请求的promise写法

```js
function PromiseAjax(url){
  return new Promise((resolve,reject)=>{
    $.ajax({
      url,
      success(res){
        resolve(res)
      },
      error(err){
        reject(err)
      }
    })
  })
}

let p1 = PromiseAjax('url1')
let p2 = PromiseAjax('url2')
let p2 = PromiseAjax('url2')

// TODO ...
```

### 2.5、Promise的方法使用

**all方法：** 

1. 只有`p1`、`p2`、`p3`的状态都变成`fulfilled`，`p`的状态才会变成`fulfilled`，此时`p1`、`p2`、`p3`的返回值组成一个数组，传递给`p`的回调函数。
2. 只要`p1`、`p2`、`p3`之中有一个被`rejected`，`p`的状态就变成`rejected`，此时第一个被`reject`的实例的返回值，会传递给`p`的回调函数。

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject("失败");
    }, 3000);
});
const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("成功2");
    }, 2000);
});
const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("成功3");
    }, 1000);
});

// 全部成功返回成功，有一个失败返回失败
let p = Promise.all([p1, p2, p3]).then((res) => console.log(res)).catch(err=>console.log(err));
```

**race方法：**只要`p1`、`p2`、`p3`之中有一个实例率先改变状态，`p`的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给`p`的回调函数。

```js
let p = Promise.race([p1, p2, p3])
.then((res) => {
    console.log(res);
})
.catch((err) => {
    console.log("网络状态不佳");
    console.log(err);
});
```

### 2.6、异步代码同步化

**async函数和await关键字**一般成对出现，当函数执行的时候，一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(1);
    }, 3000);
});
const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("成功2");
    }, 2000);
});
const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("成功3");
    }, 1000);
});

// 比如下面执行的接口要等到上面的接口请求的返回值，这时候可以让代码同步化
async function fn() {
    const res  = p1;
    console.log(res + 1);
}


async function getVal(){
    await p1.then(res=>console.log(res))
    await p2.then(res=>console.log(res))
    await p3.then(res=>console.log(res))
}
getVal()
```

## 三、作业

1. 【黄金】课堂代码写三遍(包含课堂写的)+**总结**--------**必须完成**;
2. 【铂金】使用箭头函数改造之前的案例
   - 比如进阶或者基础的案例
   - 比如骡窝窝项目中的回调函数
   - 过程中体会：什么时候可以用，什么时候不能用，尤其掌握其中的this指向
3. 【钻石】自学原生ajax的写法（后面还会讲）
4. 【王者】使用Promise封装原生ajax（模拟$.ajax方法）



总的难度10

骡窝窝--------5

小程序项目--------6.5

vue项目------------7.5

react项目----------8

vue3.0+typescript---------9.5

js高级---------------9



js高级正式开始

面向对象*3---------深挖底层-------工作中暂时用不到,面试可能会问--------写框架

当然不仅仅为了面试-------底层挖的越深,写业务会想的越多-------凡事都会想我怎么实现这个方法

# day03-面向对象

> 今日要点
>
> 1. 复习加深之前对象的学习的印象
> 2. 了解面向对象和面向过程两种思想的不同
> 3. 掌握创建对象的几种方法（必须掌握自定义构造函数）
> 4. 必须掌握**构造函数**的使用以及相关属性
> 5. **必须掌握this指向问题**
> 6. 掌握**原型对象**的使用和获取
> 7. 能说出面向对象中的名词概念
> 8. 能说出构造函数实例化对象的真实过程

## 一、对象的复习

### 1.1、万物皆对象

对象：花括号包裹的一组键值对。

生活中的每一个具体的事物都成为对象。

window对象，document对象……

JavaScript——"万物皆对象"语言。

### 1.2、对象的成员

书写对象的语法：

```javascript
{
	key1:value1，
	key2:value2
}
```

完成一个需求，对某人这个对象用代码表示：

```javascript
var person = {
    name : "阳仔",
    age : 10,
    gender : 1,
    eat : function () {
        console.log("吃饭");
    },
    sleep : function () {
        console.log("睡觉");
    }
};
console.log(person.name);//访问对象的属性
person.eat();//访问对象的方法
```

- **对象内有两种成员**：
  - name / age / sex等对象特征描述称之为对象的**属性**，就是我们之前学习的变量
  - eat / sleep 等对象拥有的行为称之为对象的**方法**，也就是我们之前说的函数

### 1.3、对象的操作

- 访问
  - person.name      `person["age"]`
  - person.eat()        `person["sleep"]()`
- 增加、修改
  - person.name="xxx"
  - 已存在则修改，不存在则新增
- 删除
  - delete person.name

### 1.4、数据安全

```js
// 将 全局变量 全局作用域的函数 封装进对象里，这样就只有一个全局变量了，就是我们创建的对象obj
// 创建一个对象，更多的是一种解决方案，一种编程思想
var obj = {
	myName:"阿伟",
    num:1,
    loginStatus:true
}
```

## 二、面向过程和面向对象编程概述（了解）

> 一般来说把面向对象和面向过程放在一起对比讲解
>
> 这是两种编程思想---或者设计思维-------自己去封装一个库或者框架（架构师）

- **面向过程**编程就是分析出解决问题的步骤，然后使用函数把这些步骤一步步实现，**重心放在完成的每个过程上**。
- **面向对象**则是以封装的思想，**重点放在解决问题需要的对象身上**，然后通过对对象的操作来完成相应的功能。

.![img](F:\\js高阶\JS高阶.assets\0A167BE7.gif)**比如盖房子**

![img](F:\\js高阶\JS高阶.assets\面向对象和面向过程.png)

- 两者比较
  - 面向过程性能比面向对象高，适合跟硬件联系很紧密的东西，但是不易维护、不易复用、不易扩展。
  - 面向对象**易维护、易复用、易扩展**，但是更耗资源，性能比面向过程低。
  - 至于以后使用哪一种，这就需要看我们的具体需求，根据不同的需求做不同的选择。

## 三、创建对象

1. 字面量方式创建对象
2. 内置构造函数创建对象
3. 简单工厂创建对象
4. 自定义构造函数创建对象

### 3.1、用字面量方式创建对象（掌握）

直接使用字面量方式创建对象比较方便，以键值对的格式来定义数据

需求：创建一本书的对象

```javascript
var book1 = {
    name:"JavaScript权威指南",
    price:100,
    author:"作者",
    showInfo:function () {
        console.log("描述信息");
    }
}
console.log(book1);
```

优点：方便直观，可以直接访问里面的属性方法；
缺点：创建大量相或相似对象时，会出现代码重复，只适合创建单个对象

### 3.2、内置构造函数创建对象

使用new关键字+内置的构造函数创建对象

```javascript
var book = new Object();
book2.name="JS";
book2.price=10;
book2.author="作者";
book2.showInfo=function () {
    console.log("描述信息");
}
book2.showInfo();
```

如果需求升级，需要创建三本不同的书的对象：

```js
创建书1:三国演义
var book1 = new Object();
book2.name="三国演义";
book2.price=85;
book2.author="作者";
book2.showInfo=function () {
    console.log("描述信息");
}
创建书2:西游记
var book2 = new Object();
book2.name="西游记";
book2.price=46;
book2.author="作者";
book2.showInfo=function () {
    console.log("描述信息");
}
创建书3:红楼梦
var book3 = new Object();
book2.name="红楼梦";
book2.price=26;
book2.author="作者";
book2.showInfo=function () {
    console.log("描述信息");
}
```

如果要创建100本书，或者创建整个图书馆所有书籍对象，怎么办？

缺点：和字面量创建存在一样问题：代码重复

### 3.3、简单工厂创建对象

利用我们学过的函数封装的思想，我们应该可以想到，当有重复代码的时候，我们可以将这些重复代码抽取到函数中来解决。

把上面的代码直接拿下来，封装进我们的函数内：

``` js
function createBook() {
	var book = new Object();
	book2.name="JS";
	book2.price=10;
	book2.author="作者";
	book2.showInfo=function () {
    	console.log("描述信息");
	}
}

```

这个时候应该想的到，抽取公共部分作为参数，可以传不同值进来；

我们需要得到这个封装好的对象后，需要返回这个对象。

就是：

```javascript
function createBook(name, price, author) {
    var book = new Object();
    book.name=name;
    book.price=price;
    book.author=author;
    book.showInfo=function () {
        console.log(this.name,this.price,this.author);
    }
    return book;
}
var book3 = createBook("bookName1",10,"author1");
var book4 = createBook("bookName2",10,"author2");
console.log(book3);
console.log(book4);
```

我们将创建book对象的代码封装到createBook函数中，当需要创建一个book对象的时候，直接调用该函数，将函数需要的参数传递过去即可。

那么，相同的思想，如果我们需要创建其他的对象，一样可以使用封装函数的方法来解决，这是没问题的。

```javascript
function createPerson(name, age) {
    var p = new Object();
    p.name = name;
    p.age = age;
    return p;
}
console.log(createPerson("Neld", 10))
```

优点：值是活的，可以批量操作，减少重复代码
缺点：无法判断对象类型

### 3.4、自定义构造函数创建对象（必须掌握）

工厂函数无法判断对象的类型，那么我们需要抽象出一个类，就是我们的构造函数

**构造函数本质上和普通函数没有区别**

目的：创建对象！

语法：

```javascript
function 函数名（参数列表）{
	this.key1=参数1,
	this.key2=参数2,
}
var obj = new 函数()
```

怎么用自定义构造函数创建对象

```javascript
function CreatePerson(name, age, sex) {
    this.name=name;
    this.age=age;
    this.sex=sex;
}
var p = new createPerson("Neld", 10, 1);
var p2 = new createPerson("Song", 12, 0);
console.log(p);
console.log(p2);
```

#### 3.4.1、自定义构造函数和工厂函数的区别

1. 构造函数名的**首字母要求大写**
2. 在函数中，不需要手动创建对象进行数据封装，**会自动创建对象并封装数据**
3. 在函数最后，不需要手动返回创建好的对象，**会自动返回**
4. 构造函数一样可以直接调用，此时内部的this执行window，这种方式不太安全，有可能会在函数内部修改当前的全局变量，不建议使用，而且这样做也不能创建对象，**必须要搭配new关键字一起使用才能创建对象**

#### 3.4.2、自定义构造函数到底是如何创建对象的？

也就是new 这个关键字做了什么事情（实例化）：

1. 在函数内部默认会创建一个空对象——var obj = new Object();
2. 默认把创建好的对象赋值给this——this = obj;
3. 通过this添加属性和方法——this.xx=xx……
4. 默认会把内部创建的对象返回——return this;

## 四、构造器属性（必须掌握）

还记不记得，工厂函数没办法区分类型的问题，而我们是构造函数可以区分类型，那，我们在构造函数里，怎么判断该对象的类型呢？

### 4.1、抽象

- **构造器(类)**：
  - **泛指一类事物**
  - 把多个对象相同的部分抽象出来，成为一个类，就是一个函数，构造函数，和new一起来创建对象，
- **对象**：
  - **特质某一个具体事物**
  - 使用构造函数创造出来的对象的类型就是构造函数这种类型

### 4.2、怎么分类

需求：定义Person和Dog类，并各自创建出一个对象，再判断对象是否是Person或Dog类型.

1. **constructor属性**

   定义：使用constructor属性可以获取到创建对象使用的构造器函数（类）。

   语法：对象.constructor——————获取到就是该对象的类

   ```javascript
   function Person(name) {
       this.name = name;
   }
   function Dog(name) {
       this.name = name;
   }
   var p = new Person("p");
   var d = new Dog("d");
   console.log(p.constructor);//打印得到Person函数对象
   console.log(d.constructor);//打印得到Dog函数对象
   if(p.constructor === Person){
       console.log("p是Person对象");
   }
   if(d.constructor === Dog){
       console.log("d是Dog对象");
   }
   ```

2. **instanceof关键字**

   定义：instanceof关键字用来判断对象的类型是否是某个类，如果是返回true，反之返回false。

   语法：var ret = 对象名  instanceof 类名;————————获取到的是一个布尔值

   ```javascript
   function Person(name) {
       this.name = name;
   }
   function Dog(name) {
       this.name = name;
   }
   var p = new Person("p");
   var d = new Dog("d");
   console.log(p instanceof Person);//true
   console.log(d instanceof Person);//false
   
   ```

## 五、this指针（必须掌握）

在JS编程的过程中发现，我们大量使用到this关键字，用好了this，能让我们的代码更加优雅。

this总是指向一个对象（引用类型），但是具体指向谁，需要根据我们在哪里使用this有关。这里主要分为下面几种情况：

1. 全局使用

   函数外部使用，作用域即使是全局作用域（window），所以，在全局作用域中使用的this指向window

   this在函数内部，全局调用这个函数，也是在全局使用，此时函数内的this也指向window

2. 对象方法的调用 例如：obj.fn()

   函数内部的作用域是局部的，属于调用当前函数的对象，所以this执向调用当前函数的对象

   包括事件绑定，也是一种对象.方法()的使用

3. 箭头函数中使用

   箭头函数没有作用域，箭头函数中的this指向外层作用域

4. 构造函数内部

   在构造函数中，this直接执行当前创建出来的新对象

## 六、原型对象

### 6.1、自定义构造函数存在的问题（了解）

问题：P对象和P2对象的say方法是同一个内存地址吗？

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.say = function(){
        console.log("say hello");
    }
}
var p = new Person("zs", 10);
var p2 = new Person("ls", 15);
console.log(p.say===p2.say);
```

上面创建的p对象的内存结构图：

![img](F:\\js高阶\JS高阶.assets\1551926860730.png)

p2对象的内存结构图：

![img](F:\\js高阶\JS高阶.assets\1551927240640.png)

**结论：从内存资源分配考虑，我们无需为每个对象创建并分配一份新的函数对象（完全相同），这种函数大家最好共享同一份。**

解决办法：那么我们可以把函数单独拿出来，定义全局，函数名做方法对象：

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.say = say
}
function say(){
	console.log("say hello");
}
var p = new Person("zs", 10);
var p2 = new Person("ls", 15);
console.log(p.say===p2.say);
```

**结论：解决方法共享的目的是达到了，但是又产生了新的问题，我们面向对象编程的目的是为了减少全局变量，而这种写法又增加了全局变量，与我们编程思想产生了冲突。**

完美的解决办法：这个时候，我们需要在构造函数上想办法，在构造函数身上开辟一个区域，来存放我们的公共方法——原型对象

### 6.2、原型对象释义（必须掌握）

定义：每一个构造函数都有一个与之相关联的对象，该对象称之为原型对象。

功能：每个实例对象都能共享其原型对象上的属性和方法，减少内存分配。

语法：

1. `构造函数.prototype` 获取原型对象
2. `构造函数.prototype.成员名 = 成员值 ` 在原型对象上添加成员的方法

所以，在上一节中，我们想在每个Person对象中共享同一个say方法，可以这样来实现：

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}
//在原型对象上添加say函数，实例对象共享该函数
Person.prototype.say = function(){
    console.log("say hello");
};
var p = new Person("zs", 10);
p.say();
var p2 = new Person("zs", 10);
p2.say();
```

### 6.3、面向对象中的核心概念（理解）

**构造函数**：Person，和new关键字一起创建对象，用来实例化对象的

**原型对象**：Person.prototype，每个构造函数与生俱来的

**实例对象**：由构造器创建出来的对象称之为实例对象

**实例化：**由构造器创建实例对象的过程称之为实例化

对象的成员：属性+方法

**实例成员：**实例对象上的属性和方法，name,age，只能**当前实例对象**才能访问

**原型成员：**原型对象上的属性和方法，say()，使用该原型对象对应构造器创建出来的所有实例对象都能访问

**静态成员：**直接添加在构造函数上的属性和方法，只能使用构造函数才能访问

### 6.4、获取原型对象的方法

#### 6.4.1、 __ proto __属性（必须掌握）

定义：在每个实例对象上都有一个__ proto __的属性，也是用来获取该对象的原型对象（该属性是在ES6之后才纳入规范，在这之前，只有部分浏览器实现。）。

语法： `实例对象.__ proto __;`

```javascript
实例对象.__ proto __ === 构造器.prototype；
```

我们之前说过：每个实例对象都能共享其原型对象上的属性和方法

那么之前我们用 对象.constructor来获取到就是该对象的类 是什么原理？

![img](F:\\js高阶\JS高阶.assets\154548446454.jpg)

结论：实例对象没有constructor属性，其实是共享了其原型对象上的属性（Person.prototype身上才有constructor属性）

`__ proto __`属性，可以当做一个象形文字来看，这个下划线不是无意义的，它相当于一条锁链，把我实例对象身上没有的属性方法，通过这条锁链暴力拉下来，供我使用。



这样，我们就可以通过一个图来表示构造函数、原型对象和实例对象三者的关系：

![img](F:\\js高阶\JS高阶.assets\1551935332196.jpg)



#### 6.4.2、 getPrototypeOf方法（了解）

定义：Object构造器上的静态成员方法。

语法：`Object.getPrototypeOf(实例对象)` 获取指定实例对象的原型对象

以上提到的三种获取原型对象的方法所得到的结果是一样的。即：

```javascript
Object.getPrototypeOf(p) == Person.prototype == p.__ proto __
//代码不能这么写，要分开比较
```

### 6.4、构造函数创建实例对象补充（必须掌握）

在对原型相关的知识有了一定的认识之后，我们再回过头来看看构造函数创建实例对象中的细节问题。

```javascript
function Person(name) {
    //默认创建一个Object对象 var obj = new Object();
    //将obj对象赋值给this   this = obj;
    this.name = name;//通过this添加属性和方法
    //返回封装好的this对象，return this;
}
```

这是我们前面分析出来的步骤，现在再来看问题就很明显了。

在函数中，默认为我们创建的是一个Object类型的对象，该对象和当前的Person构造器没有任何关系。

那么想让最终创建出来的对象拥有具体的类型的话，应该还有下面一个步骤：

```javascript
//设置obj的__proto__属性指向Person构造函数的原型对象
//obj.__proto__ = Person.prototype;
```

**构造函数创建实例对象的完整过程：**

1. 在函数内部默认会创建一个空对象——var obj = new Object();
2. 设置`obj.__proto__` 属性指向构造器.prototype——`obj.__proto__ = Person.prototype`;
3. 默认把创建好的对象赋值给this——this = obj;
4. 通过this添加属性和方法——this.xx=xx……
5. 默认会把内部创建的对象返回——return this;

## 七、作业

1. 【黄金】课堂代码写三遍(包含课堂写的,包含图，课堂没写完的写完)+**总结**--------**必须完成**;
2. 【铂金】思考：（需要预习明天原型链的内容）
   - 为什么字符串（基本类型）可以使用属性方法
   - 为什么创建一个新数组可以使用Array方法
3. 【王者】使用构造函数和原型对象尝试封装tab栏案例



# day04-面向对象

> 今日要点
>
> 1. **掌握原型链的访问规则**
> 2. **掌握原型相关属性学习**
> 3. 了解面向对象三大特性（封装、多态、继承）
> 4. 了解两种继承方式（混入、原型式）
> 5. **掌握原型链继承**
> 6. **掌握call方法和apply的使用**
> 7. 掌握组合继承
> 8. 能够画出完整的原型链结构图

## 一、原型对象的设置和访问（掌握）

### 1.1、设置原型遇到的问题

我们设置单个公共方法的时候可以使用`构造器.prototype.方法名 = 方法函数 ` 这种方法

```javascript
//构造函数
function Person(name, age) {
    this.name = name;
    this.age = age;
}
//在原型对象中添加方法
Person.prototype.study = function () {
    console.log(this.name,this.age);
}
//创建实例对象
var p = new Person("zs",10);
var p2 = new Person("ls",12);
p.study();
p2.study();
```

如果需要在原型对象上添加多个成员的时候怎么办？一个一个添加？是不是首先想到把它们封装进一个对象里，就是下面这种方式：

```javascript
Person.prototype = {
    study:function () {
        console.log(this.name,this.age);
    },
    say:function () {
        console.log(this.name," say hello");
    }
}
```

相对于之前的方式，这种方式能够更统一、更方便的在Person原型对象上添加成员。

那么，问题来了！

**上面这段代码必须写在创建实例对象之前，否则添加的成员不可用。**

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}
var p = new Person("zs",10);
Person.prototype = {
    study:function () {
        console.log(this.name,this.age);
    }
}
p.study();//p.study is not a function
```

为什么会有这样的问题？

其实也不难理解，在创建p对象的时候，Person及Person的原型对象中都没有study函数，所以创建出来的p对象中自然也不会有该函数，所以出现这个问题是必然的。下面画图分析一下：

![1560217055549](F:\\js高阶\JS高阶.assets\设置原型遇到的问题.png)

接着，更可怕的问题又来了！

**对象已经创建好，并且也能使用到原型对象中的方法，此时p对象的constructor属性指向变的不认识了**

```
console.log(p.constructor) ------------>  ƒ Object() { [native code] }
```

为什么会有这样的问题？

我们需要拓展一下之前画过的构造器、原型对象和实例对象的图例

### 1.2、原型对象的访问规则

证明p.constructor是什么：

```javascript
p.constructor === Object  //实例对象的constructor属性指向了Object构造函数
字面量对象.constructor===Object  //说明新的原型对象的constructor属性也指向了Object构造函数
字面量对象.__proto__===Object.prototype  //说明新的原型对象的构造函数和与之相对应的原型对象实例化了该对象
```

之前有讲过：实例对象没有constructor属性，其实是通过`__proto__`共享了其原型对象上的属性

原型对象上没有，怎么办？

**顺着`__proto__` 这个链条，一直往上找，直到找到这个属性为止……**

最终，找到了新的原型对象的构造函数是Object，说明Object.prototype有constructor属性，所以p.constructor属性最终返回的是Object的构造函数。导致的结果是无法判断类型了。

![1560217110614](F:\\js高阶\JS高阶.assets\1551945373857.jpg)

如何解决问题：

在新的原型对象上添加一个constructor属性指向Person构造器，从而改变p.constructor的指向，最终得到其真实类型。

```javascript
Person.prototype = {
    //通过该属性修改constructor属性的指向,达到用他来判断对象类型的目的
    constructor:Person,
    study:function () {
        console.log(this.name,this.age);
    },
    say:function () {
        console.log(this.name," say hello");
    }
}
```

画图表示：

![1560217166912](F:\\js高阶\JS高阶.assets\1551946077524.jpg)



## 二、原型相关属性学习（掌握）

### 2.1、in关键字

定义：用来检查对象中是否存在某个指定的属性(不区分实例属性和原型属性)，

语法：`"属性名" in 实例对象 `

用法：无论判断的成员是属于当前实例对象还是属于其原型对象的，都返回true，如果都不存在，则返回false。

### 2.2、hasOwnProperty方法

定义：Object的原型成员，所有实例对象都能访问的方法，

语法：`实例对象.hasOwnProperty("属性名")`

用法：只判断当前实例对象中是否存在实例的属性，存在返回true，反之返回false。

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}
Person.prototype = {
    constructor:Person,
    study:function () {
        console.log(this.name,this.age);
    },
    say:function () {
        console.log(this.name," say hello");
    }
}
var p = new Person("zs",10);
console.log("name" in p);//true
console.log("study" in p);//true
console.log("name222" in p);//false
console.log(p.hasOwnProperty("name"));//true
console.log(p.hasOwnProperty("study"));//false
console.log(p.hasOwnProperty("name222"));//false
```

有了上面的说明，完成下面两个需求应该就比较简单了。

需求1：检查对象中是否存在某个指定的属性（该属性只存在实例对象上）

​	`hasOwnProperty`

需求2：检查对象中是否存在某个指定的属性（该属性只存在原型对象上）

​	`key in obj && !obj.hasOwnProperty(key)`

### 2.3、isPrototypeOf方法

定义：Object的原型成员，判断某个对象是否是指定对象的原型对象

语法：`原型对象.isPrototypeOf(实例对象)`

用法：A.isPrototypeOf(B) 判断的是A对象是否存在于B对象的原型链之中

### 2.4、instanceof关键字

定义：字面意思理解为判断当前对象是否是指定的类型，更深层次理解应该是，指定类型是否在当前实例对象的原型链上，如果是返回true，反之返回false。

语法：`实例对象 instanceof 构造函数`

用法：A instanceof B 判断的是B.prototype是否存在与A的原型链之中

```javascript
    function Person(name,age) {
        this.name=name;
        this.age=age;
    }
    Person.prototype.say=function () {
        console.log(this.name," say hello");
    }
    var p=new Person('lily',13)
    console.log(p instanceof Person);//true
    console.log(p instanceof Object);//true
    console.log(Object.prototype.isPrototypeOf(p));//true
```

## 三、面向对象三大特性（了解）

### 3.1、封装

定义：使用对象封装一些变量和函数

作用：复用和信息隐藏

详解：封装，也就是把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。

### 3.2、继承

定义：一个类获取另外一个类属性和方法的一种方式
作用：代码复用
详解：继承，就是可以使用已创建好的类的所有功能，并在无需重新编写原来的类的情况下对这些功能进行扩展。

- 通过继承创建的新类称为“**子类**”或“派生类”。
- 被继承的类称为“基类”、“**父类**”或“超类”。
- 继承的过程，就是从一般到特殊的过程。

### 3.3、多态

定义：同一个操作，作用于不用的对象，会有不同的行为
作用：具有可拓展性
详解：多态首先是建立在继承的基础上的，先有继承才能有多态。多态是指不同的子类在继承父类后分别都重写覆盖了父类的方法，即父类同一个方法，在继承的子类中表现出不同的形式。js天生就具备多态的特性(弱类型语言)

## 四、继承

ES5是没有继承语法的，只能通过方法模拟继承语法，所以有多种方式达到继承效果。
继承目的：通过相应的代码将父类中的成员复制到子类对象中

- [x] 混入式继承
- [x] 原型式继承
- [x] 原型链继承
- [ ] 借用构造函数继承
- [ ] 组合继承

### 4.1、混入式继承（了解）

实现原理：**将父类成员拷贝到子对象中（浅拷贝）。**

实现方法：`for…in…循环遍历父类，子类[key]=父类[key]`

缺点：共享数据安全问题，修改子类，会影响父类，引用数据类型浅拷贝，会修改引用地址

```js
//混入式继承（拷贝继承）
//obj2继承到obj1中的成员，可以直接将obj1中的成员拷贝到obj2中即可
var obj1 = {name:"zs",age:10};
var obj2 = {};
// 将obj1中的成员拷贝到obj2中
for (var key in obj1) {
    obj2[key] = obj1[key];
}
console.log(obj1);
console.log(obj2);
```

共享数据安全的问题：

```js
var obj1 = {name:"zs",age:10,car:{name:"mini"}};
var obj2 = {};
// 将obj1中的成员拷贝到obj2中
for (var key in obj1) {
    obj2[key] = obj1[key];
}
//修改obj1对象中的car属性
obj1.car.name = "bus";

console.log(obj1);//{name:"zs",age:10,car:{name:"bus"}}
console.log(obj2);//{name:"zs",age:10,car:{name:"bus"}}
```

当我们需要修改其中某一个对象中的引用类型属性时，会造成其他相关的对象也被修改，原因在于大家引用的是同一个内存区域中的数据。

### 4.2、原型式继承（了解）

实现原理：**将父类中的原型成员添加到子类的原型链中。**

实现方式：`子类.prototype = 父类.prototype`

缺点：数据共享安全，只能继承父类原型对象中成员，不能继父类实例对象成员

```js
function Animal() {
}
Animal.prototype.name="animal";

function Person() {
}
//修改Person的原型对象
Person.prototype= Animal.prototype;

Person.prototype.useTool = function () {
    console.log("use fire");
}
var p = new Person();
console.log(p);
var ani = new Animal();
console.log(ani);
```

画图分析：

1. 最初，Animal和Person的两个对象没有任何关系，所以各自只能访问各自的成员


2. 现在，Person对象如果想要继承Animal对象，只需要将Person的原型对象修改为Animal的原型对象即可

3. 这种方式实现的继承称之为原型式继承，实现也是比较方便的，但是和混入式继承一样，存在数据共享安全的问题。

   ![1560238770648](F:\\js高阶\JS高阶.assets\1552015375952.jpg)

### 4.3、原型链继承（掌握）

实现原理：**将子类的原型对象指向父类的实例对象。**

实现方法：`子类.prototype = new 父类()`

```javascript
function Person(name,age) {
    this.name = name;
    this.age = age;
}
Person.prototype.getInfo = function () {
    console.log("name:",this.name,"age:",this.age);
}
function Student(score) {
    this.score = score;
}
Student.prototype = new Person("小明",10);//继承父构造函数并设置name和age的值
Student.prototype.getScore = function () {
    console.log("分数:"+this.score);
}
var p1 = new Student(100);
p1.name="xxx"//只能这样一个个修改，无法向父类传参
var p2 = new Student(12);
console.log(p1);
console.log(p2);
```

存在问题：存在数据共享问题，无法给父类构造函数传递参数

![1560238770648](F:\\js高阶\JS高阶.assets\fdsfsfsdf.png)

### 4.4、借用构造函数继承（掌握）

#### 4.4.1、call方法和apply方法的基本使用（十分重要）

定义：将方法**借给**某个对象的方法。call和apply作用相同，写法不同。

使用call方法的语法：

```javascript
被借用对象.方法.call(借用对象)
```

使用apply方法的语法：

```javascript
被借用对象.方法.apply(借用对象)
```

 **特点：可以设置方法中this的指向——方法中的this指向借给的对象**

```js
var obj1 = {
    name:"Neld",
    age:10,
    showInfo:function () {
        console.log("name:"+this.name,"age:"+this.age);
    }
}
var obj2 = {
    name:"Lily",
    age:12
}
obj1.showInfo();//name:Neld age:10
obj2.showInfo();//obj2.showInfo is not a function

obj1.showInfo.call(obj2);//name:Lily age:12
// obj1.showInfo.apply(obj2);//name:Lily age:12
```

**call和apply的区别（传参方式不同）**： 

```javascript
// call传参，跟在借用对象后面，用逗号隔开
被借用对象.方法.call(借用对象,参数1,参数2……)
// apply传参，不能直接写在后面，要将参数封装在数组中跟在借用对象后面，用逗号隔开
被借用对象.方法.apply(借用对象,[ 参数1,参数2…… ])
```

需求：给obj1添加add方法，需要传入两个参数，完成加法运算。然后将这个方法借给obj2对象，通过obj2传入参数，完成加法运算

```js
var obj1 = {
    name:"Neld",
    age:10,
    add : function (a, b) {
        return a + b;
    }
}
var obj2 = {
    name:"Lily",
    age:12
}
//使用cal方法
obj1.add.call(obj2, 100, 200);
//使用apply方法
//console.log(obj1.add.apply(obj2, 1, 2));//CreateListFromArrayLike called on non-object
obj1.add.apply(obj2, [100, 200]);
```

#### 4.4.2、借用构造函数继承说明

实现原理：在子构造函数中调用父构造函数，达到继承并向父构造函数传参的目的。

实现方法：

1. 将父对象的构造函数设置为子对象的成员
2. 调用这个方法，类似于将父构造函数中的代码复制到子构造函数中来执行
3. 用完之后删掉

```js
function Person(name,age) {
    this.name = name;
    this.age = age;
}
Person.prototype.getInfo = function () {
    console.log("name:",this.name,"age:",this.age);
}
function Student(name,age,score) {
  	this.newMethod = Person;//1.将父对象的构造函数设置为子对象的成员
    this.newMethod(name, age);//2.调用这个方法，类似于将父构造函数中的代码复制到子构造函数中来执行
    this.score = score;
  	delete this.newMethod;//3.用完之后删掉
}
Student.prototype.getScore = function () {
    console.log("分数:"+this.score);
}

var p1 = new Student("Neld", 10 ,100);
var p2 = new Student("Lily", 12 ,80);
console.log(p1);
console.log(p2);
```

**高级实现方法：凡是要借用方法，首先想到使用call或apply**

```js
function Student(name,age,score) {
    //Person.call(this,name,age);
    Person.apply(this,[name,age]);
    this.score = score;
}
```

这种继承方式都存在下面两个问题：

1. 如果父子构造函数存在相同的成员，那么子构造函数会覆盖父构造函数中的成员
2. 不能继承原型链中的成员

### 4.5、组合继承（必须掌握）

实现原理：基原型链继承+借用构造函数继承

```js
function Student(name,age,score) {
   //Person.call(this,name,age);
   Person.apply(this,[name,age]);//继承构造函数中的成员
   this.score = score;
}

Student.prototype = new Person();//继承原型链上的成员
Student.prototype.constructor = Student
```

缺点：子类的原型对象上有无用属性

### 4.6、寄生组合继承（拓展）

实现原理：组合继承的基础上，改造原本的原型链继承。子类和父类中间创建一个空类，过滤掉无用的父类实例属性。

```js
// 寄生式组合继承，在父子类中间再加一层，去掉子类原型对象上的无用属性
(function () {// 4.创造一个独立的作用域，用完失效
    // 1.创建一个没有实例成员的Super类
    var Super = function () { };
    // 2.将Super类的原型对象指向父类的原型对象
    Super.prototype = Person.prototype;
    // 3.将Super类的实例作为子类的原型
    Student.prototype = new Super();
	Student.prototype.constructor = Student;
})();
```

总结：  ES5实现继承的方式不止一种。这是因为ES5 中的继承机制并不是明确规定的，而是通过模仿实现的。这意味着所有的继承细节并非完全由解释程序处理。作为开发者，你有权决定最适用的继承方式。

## 五、绘制完整的原型链结构图（掌握）

这一节重点探讨函数对象的原型链结构。完整的结构图如下：

![img](F:\\js高阶\JS高阶.assets\15464464848.png)

总结：

1. 所有的函数对象都是Function类型，由Function构造函数创建
2. Function的原型对象是一个匿名空函数，绑定了函数中的通用方法
3. 空函数对象的类型是Object
4. Function函数对象由自身的构造函数创建

## 六、作业

1. 【黄金】课堂代码（包含画图）写三遍(包含课堂写的，课堂没写完的写完)+**总结**--------**必须完成**;

2. 【铂金】说出下列执行结果，并解释原因

   ```js
   console.log(Function instanceof Object);  // true
   console.log(Object instanceof Function);  // false
   console.log(Function.prototype instanceof Object); // true
   console.log(Object.prototype instanceof Function);  // false
   ```

3. 【王者】实现下列继承

   - Animal（父类）---->Person（子类）
   - Person（父类）---->Student（子类）
   - 使用Student创建实例对象，并且调用Animal类的原型方法



# day05-面向对象

> 今日目标
>
> 1. **掌握组合继承和完整的原型链结构图**
> 2. 理解三大**基本包装类型**（String，Number，Boolean）
> 3. 能说出什么是对象的私有成员和特权方法
> 4. 了解Object成员（原型成员+静态成员）
> 5. **使用 Object.prototype.toString.call(...) 判断类型**
> 6. **必须掌握ES6的类class使用**

## 一、基本包装类型的使用（理解）

### 1.1、基本包装类型的创建

定义：方便对string，number，boolean三种基本类型数据操作，ECMAScript提供了三个特殊引用类型——基本包装类型（String，Number，Boolean）

**创建方式：**

```javascript
// 方式一：
var str1 = new String("string1");
var num1 = new Number(123);
var bool1 = new Boolean(true);
console.log(str1);
console.log(num1);
console.log(bool1);
// 方式二
var str2 = new Object("string2");
var num2 = new Object(456);
var bool2 = new Object(false);
console.log(str2);
console.log(num2);
console.log(bool2);
```

### 1.2、基本包装类型使用的注意点

先看下面的代码，观察存在的问题：

```js
var str = "test";
console.log(str.length);//4
console.log(str.substr(0, 2));//te
```

上面代码看似很简单，但是存在一个很基本的疑问点：

str是基本类型，不存在属性和方法一说，但是下面两行代码中却是在访问属性和方法，而且代码还能正确的执行，这是如何实现的呢？

其实，为了让我们实现这种直观的操作，后台已经自动完成了以下操作：

- 创建 String 类型的一个实例；
- 在实例上调用指定的方法；
- 销毁这个实例；

```js
var str = "test";
var obj = new String(str);
console.log(obj.length);
console.log(obj.substr(0, 2));
obj = null;//使用完之后销毁obj
```

经过此番处理，基本的字符串值就变得跟对象一样了。而且，上面这三个步骤也分别适用于 Boolean和 Number 类型对应的布尔值和数字值

## 二、私有成员和特权方法（了解）

这一节我们来解释几个在JS使用过程中经常使用到的概念，清楚这些概念有助于大家对后面知识点的学习。

```js
function Person(name, age) {
    var className = "H5";
    this.name = name;
    this.age = age;
    this.showName = function () {
        console.log(this.name);
    }
    function getClassName() {
        return className;
    }
    this.showClass = function () {
        console.log("姓名：",this.name,"班级：",getClassName());
    }
}
Person.prototype.des = "H5-JS面向对象";
Person.info = "H5 Information";
```

成员：对象的属性和方法

实例成员：实例对象的属性和方法  name\age | showName\showClass

静态成员：构造函数自己的属性和方法  info

原型成员：构造函数对应的原型对象的属性和方法  des

**私有成员**：在构造函数中声明的变量和函数，因为我们只能在函数内部访问，所以是私有的  className  getClassName

**特权方法**：在函数内部使用了私有成员的实例方法被称为是特权方法（闭包）  showClass

## 三、Object成员（了解）

### 3.1、原型成员

![img](F:\\js高阶\JS高阶.assets\465464564.jpg)

- **constructor**：获取当前对象的构造函数

- **hasOwnProperty**：判断当前实例对象中是否存在指定的属性

- **isPrototypeOf**：判断当前对象是否在指定对象的原型链中

- **propertyIsEnumerable**：实例成员是否可以枚举（循环遍历）返回布尔值

- **valueOf**：返回当前对象对应的值。

  - 三大包装类型（还有Date）都有原型成员valueOf，所以基本类型使用valueOf是使用自己包装类型的valueOf原型方法
  - Object.prototype.valueOf.call(...);才能真正使用Object的valueOf原型方法
  - 特点：基本类型会得到包装类型的返回值

  ```javascript
  var strObj = new String("demo");
  console.log(strObj.valueOf());//demo 基本包装类型：返回对应的值 
  var obj = {name:'ls',age:18};
  console.log(obj.valueOf());//{name:'ls',age:18} 返回对象本身
  var date = new Date();
  console.log(date.valueOf());//1559489503989 返回时间戳
  
  Object.prototype.valueOf.call(1);
  Object.prototype.valueOf.call("");
  Object.prototype.valueOf.call(true);
  ```

- **toString**：返回数据特定的格式的字符串  [object  构造函数]。

  - 几乎所有的构造函数都有原型成员toString，所以字符串，数字，布尔，数组等类型使用toString是使用自己构造函数的toString原型方法
  - Object.prototype.toString.call(...);才能真正使用Object的toString原型方法
  - **作用：可以获取所有数据的真实类型**

  ```javascript
  // 其实调用的是包装类型的toString方法
  console.log("abc".toString());//"abc"
  console.log((123).toString());//"123" 
  console.log((100).toString(2));//1100100 
  console.log((100).toString(16));//64 
  console.log(true.toString());//"true"
  
  // 对象使用的才是Object的toString原型方法
  function Person(name) {
  	this.name = name; 
  } 
  var p = new Person("Neld"); 
  // 第一个object为对象的类型，第二个Object为对象对应的构造函数
  console.log(p.toString());//"[object Object]"
  
  // 数组会调用Array的toString方法
  var arr = [1,2,"A",false]; 
  console.log(arr.toString());//"1,2,A,false"
  ```


### 3.2、静态成员

![img](F:\\js高阶\JS高阶.assets\46456464dsd.jpg)

- **assign**：将多个对象合并到一个对象中并返回

  ```javascript
  var obj = {name:"Neld", age:10};
  console.log(Object.assign(obj, {info: "xxx"}, {name: "zs"}));
  // 返回结果为：{name:"zs", age:10, info:"xxx"}，如果多个对象想存在相同的属性，后面会将前面属性值覆盖。
  ```

- **create**：创建对象，并设置原型对象

  ```javascript
  // 该方法可以接收的参数有一下两种
  // 1. null 创建一个空对象，这个空对象中连最基本的原型对象都没有的 
  	Object.create(null)//创建一个空对象
  // 2. 对象 创建传递进来的对象，并设置该对象的原型对象为当前的参数
  	Object.create({……})//创建出的对象，给原型对象添加……成员
  ```


- **is**：判断两个参数是否相等，等同于===，注意下面两种特殊的判断即可

  ```javascript
  console.log(0 === -0); //true
  console.log(Object.is(-0, 0)); //false
  console.log(NaN === NaN); //false
  console.log(Object.is(NaN, NaN)); //true
  ```


- **values**：获取当前对象所有属性的值，合并成一个数组并返回

  ```javascript
  var obj={name:"小明",age:10,gender:1};
  Object.values(obj) //["小明", 10, 1]
  ```


## 四、ES6类的实现——class（必须掌握）

### 4.1、class的基本结构

定义及用法：calss关键字定义类，创建构造函数，类名首字母大写

语法结构：

```javascript
class 类名{
  constructor(参数1,参数2){
    // 构造函数体，添加实例对象成员
  }
  方法名(){
    // 添加原型对象成员
  }
  static 方法名{
    // 添加静态成员，只能用类调用
  }
}
var d=new 类名
```

ES5中，使用function定义一个类，并使用它来创建对象。

```js
function Person(name, age){
    //实例成员
    this.name = name;
    this.age = age;
}
Person.prototype.doWork = function(){
    console.log("ES5中在原型对象上添加方法")；
}
var p = new Person("Neld", 10);
```

在ES6中，使用class关键字定义同样的类。

```javascript
class Person{
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
    doWork(){
        console.log("ES6中在原型对象上添加方法");
    }
}
var p = new Person("Neld",10);
console.log(p);
```

ES6中使用class定义类只是一种语法糖（语法糖能够增加程序的可读性，从而减少程序代码出错的机会的一种语法），底层最终还是转换成ES5中使用的function类定义类，以及其中的实例成员和原型成员。

![1552221266698](F:\\js高阶\JS高阶.assets\11616161561.jpg)

**class使用的细节：**

1.  constructor方法是创建对象的构造方法，通常在这里为实例对象定义属性（方法也是可以的），new 之后会自动调用。

2.  constructor方法外面的方法是对象的原型方法。

3.  在之前外面还为构造方法添加过成员（静态成员），前面要加static。

```javascript
class Person{
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
    static doWork(){
        console.log("ES6中在原型对象上添加方法");
    }
}
Person.doWork()
```

### 4.2、class的继承结构

ES6中class用extends 和 super实现继承。

语法结构：

```javascript
class 子类 extends 父类{
  constructor(参数1,参数2){
    //调用父类构造函数，将数据封装到对应属性中
    super(参数1,参数2);
  }
}
```

需求：用class定义Animal类，然后定义Person类并继承Animal类。

```js
class Animal {
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
    eat(){
        console.log("吃饭");
    }
    sleep(){
        console.log("睡觉");
    }
}
class Person extends Animal{//extends关键字实现类继承
    constructor(name,age){
        super(name,age);//调用父类中的构造方法
    }
    play(){
        console.log("打豆豆");
    }
}
console.log(new Person("Neld", 10));
```

**class实现继承的细节：**

1. Animal中定义了动物都应该有的属性和方法
2. 使用extends关键字实现Person类继承Animal类的功能，此时他们两就属于继承关系了。

3. 在Person的构造方法中，使用super关键字调用父类中的构造方法。


## 五、异常捕获（了解）

JS引擎执行JS代码时，会发生各种错误，比如：

1. 语法相关问题（程序报错）
2. 业务逻辑相关问题（即使出错了，也会继续执行后面的代码）

```javascript
try{
 	 // 可能出错的代码
 	 throw // 手动抛出自定义异常
}catch(e){
 	 // 处理try代码块中抛出的异常
 	 // e 错误信息
}finally{
 	 // 无论什么情况都会执行代码块
}：
```

需求：判断函数参数是不是数字，不是则抛出异常。

```javascript
function fun(num) {
    if (typeof num !== "number") {
      throw "数据类型错误";
    }
    console.log(num);
}

try {
 	 fun("1");
} catch (e) {
    if(e==="数据类型错误"){
      	console.log('本程序猿知道了，马上就改')
    };
}
```

## 六、严格模式（了解）

为什么使用严格模式：

- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;

- 消除代码运行的一些不安全之处，保证代码运行的安全；
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript做好铺垫。

"严格模式"体现了Javascript更合理、更安全、更严谨的发展方向，包括IE 10在内的主流浏览器，都已经支持它，许多大项目已经开始全面拥抱它。

另一方面，同样的代码，在"严格模式"中，可能会有不一样的运行结果；一些在"正常模式"下可以运行的语句，在"严格模式"下将不能运行。掌握这些内容，有助于更细致深入地理解Javascript，让你变成一个更好的程序员。

**严格模式的限制：**

进入严格模式的方法很简单，只需要在脚本或者函数的开头输入**"use strict"**即可，值得一提的是，在无法执行严格模式的旧版浏览器中（IE10之前），该条指令会自动被忽略。

限制1：不允许使用未声明的变量

```js
"use strict";
x = 1;          // Uncaught ReferenceError: x is not defined
```

限制2：严格模式定义在脚本开头，会对整个脚本执行严格模式

```js
"use strict";
function fn () {
  x = 1;            // Uncaught ReferenceError: x is not defined
}
fn();
```

限制3：如果严格模式定义在函数头部，那么只在当前函数中使用严格模式，对函数外部的代码没有影响。

```js
x = 1;//不报错
function fn () {
  "use strict"
  y = 2；            // Uncaught ReferenceError: y is not defined
}
fn();
```

限制4：在严格模式下，不能对对象的只读属性赋值

```js
"use strict";

// 给不可写属性赋值
var obj1 = {};
Object.defineProperty(obj1, "x", { value: 42, writable: false });
obj1.x = 9; // 抛出TypeError错误


// 给不可扩展对象的新属性赋值
var fixed = {};
Object.preventExtensions(fixed);
fixed.newProp = "ohai"; // 抛出TypeError错误
```

限制5：在严格模式下，试图删除不可删除的属性时，会抛出异常

```js
"use strict";
delete Object.prototype; // 抛出TypeError错误
```

限制6：在严格模式下，不允许重名属性

```js
"use strict";
var o = { p: 1, p: 2 }; // 语法错误
```

限制7：严格模式要求函数参数名唯一

```js
function sum(a, a, c){ // 语法错误
  "use strict";
  return a + a + c; // 代码运行到这里会出错
}
```

限制8：禁止八进制数字语法

```js
"use strict";
//0开头8进制  0x开头16进制  0b开头2进制
var sum = 015 + // 语法错误
          197 +
          142;
```

限制9：禁止设置原始类型（primitive）值的属性

```js
(function() {
  "use strict";
  false.true = "";              //TypeError
  (14).sailing = "home";        //TypeError
  "with".you = "far away";      //TypeError
})();
```

限制10：禁用`with`

```js
var a = {
    name:"zs",
    b:{
        age:10,
        c:{
            color:"red",
            des:"description"
        }
    }
}
console.log(a.b.c.color);
console.log(a.b.c.des);

// with语句可以在不造成性能损失的情况下，减少变量的长度，同时简化我们的代码。
with(a.b.c){
    console.log(color);
    console.log(des);
}
```

限制11：严格模式下，`eval()`创建变量不能被调用

```js
"use strict";
eval ("var x = 2");
alert (x);                      // Uncaught ReferenceError: x is not defined
```

限制12：严格模式禁止删除声明变量

```js
"use strict";

var x;
delete x; // 语法错误
```

限制13：不能使用`eval` 和 `arguments`作为标识

```js
"use strict";
var arguments = 1;// Uncaught SyntaxError: Unexpected eval or arguments in strict mode
var eval = 2;     // Uncaught SyntaxError: Unexpected eval or arguments in strict mode
```

限制14：严格模式下，函数的 arguments 对象会保存函数被调用时的原始参数。arguments[i] 的值不会随与之相应的参数的值的改变而变化，同名参数的值也不会随与之相应的 arguments[i] 的值的改变而变化。

```js
"use strict";
function f(a,b) {
    a=10;
    console.log(arguments[0]);//1
    arguments[0] = 20;
    console.log(a);//10
}
f(1,2);
```

限制15：不再支持`arguments.callee`

```js
"use strict";
var f = function() { return arguments.callee; };
f();                // TypeError
```

限制16：保留部分关键字，这些字符包括implements, interface, let, package, private, protected, public, static和yield。在严格模式下，你不能再用这些名字作为变量名或形参名。

限制17：禁止this指向全局对象，当this指向全局对象时，自动转为undefined

**总结**

当你想要提升原生JS代码的健壮性和可读性，回避JS一些被人诟病的语法，严格模式是你不二的选择。

## 七、作业

1. 【黄金】课堂代码写三遍(包含课堂写的，课堂没写完的写完)+**总结**--------**必须完成**;
2. 【铂金】使用class实现下列继承
   - Animal（父类）---->Person（子类）
   - Person（父类）---->Student（子类）
   - 使用Student创建实例对象，并且调用Animal类的原型方法
3. 【王者】使用class实现Tab栏面向对象封装
