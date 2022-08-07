3天------知识点形式-----火箭

面试题生生世世背不完---概率性-----背面试题为了提高概率

学习最怕:

1. 我全都要-----没必要钻那么深
2. 他行我也行----跟自己比,超过昨天的自己

# day06-面试题粗讲

> 今日要点
>
> 1. 能说出立即执行函数的特点
> 2. 能说出闭包的概念和特点
> 3. 掌握递归的基本写法
> 4. 掌握深拷贝的实现
> 5. 掌握冒泡排序法的实现
> 6. 理解快速排序算法的实现

## 一、立即执行函数（掌握）

定义：声明一个函数,并马上调用这个匿名函数就叫做**立即执行函数**或者即时函数（匿名函数自执行）Immediately-Invoked Function Expression (*IIFE*)

特点：

1. 首先是个匿名函数，无需函数命名。
2. 主要作用是：防止全局变量污染，便于多人协作开发。
3. 函数需要立即执行，且只需要执行一次，执行一次之后不再调用，通常用于需要初始化的变量。

语法结构：

```js
// 掌握这一种
(function (形参) {
    console.log("方式一");
})(实参);

// 了解下面的
(function () {
    console.log("方式二");
}());
!function () {
    console.log("方式三");
}();
+function () {
    console.log("方式四");
}();
-function () {
    console.log("方式五");
}();
~function () {
    console.log("方式六");
}();
```

立即执行函数的作用：

- 避免了污染全局变量
- 封装变量
- 立即执行函数内部形成了一个单独的作用域，可以封装一些外部无法读取的**私有**变量

需求：给三个li标签绑定事件，点击之后打印对应索引

```html
<ul id=”test”>
    <li>这是第一条</li>
    <li>这是第二条</li>
    <li>这是第三条</li>
 </ul>
 
<script>
    var liList=document.getElementsByTagName('li');
    for(var i=0;i<liList.length;i++){
         liList[i].onclick=function(){
             console.log(i);
        }
    };
</script>
```

问题：for循环会在一瞬间完成，当你触发点击事件的时候，i已经成为了3

**用之前学过的方法解决**

先把索引存起来，变成自己的私有属性

```javascript
  var liList = document.getElementsByTagName("li");
  for (var i = 0; i < liList.length; i++) {
    liList[i].index = i;
  	liList[i].onclick = function () {
  		console.log(this.index);
  	};
  }
```

**用立即执行函数解决**

给每个 li 创造一个独立作用域，立即执行函数执行的时候，i 的值被赋值给 ii，此后 ii 的值一直不变，实现了**全局变量私有化**。

```javascript
  var liList=document.getElementsByTagName('li');
  for(var i=0;i<liList.length;i++){
    (function(ii) {
      liList[ii].onclick=function(){
          console.log(ii);
      }
    })(i)
  };
```

## 二、闭包（理解）

### 2.1、函数外部如何访问局部变量

JS中每个函数都有自己的作用域，在当前函数中定义的变量，只能在该函数或该函数的嵌套函数中访问。如：

```js
function fun(){
    var a = 123;
    console.log(a);//123
}
console.log(a);//报错：a没有定义
```

在开发中，如果需要在当前函数作用域外访问函数的局部变量能实现吗？看下面的代码：

```js
function fun() {
    var a = 123;
    function fun2() {
        return a;
    }
    return fun2;
}
var fun3 = fun();
console.log(fun3());//123
```

在函数fun中定义了另一个函数fun2,fun2中访问函数外部的局部变量a，最后将fun2返回。

调用fun得到返回值（fun2函数），因为该返回值是一个函数，所以我们调用得到函数中返回的a的值。

**定义：像这种函数中返回另一个函数的结构称为闭包。**

特点：

1. **打破作用域的限制，让外部访问函数内部变量成为可能，延长变量的生命周期；**
2. 可以避免使用全局变量，防止全局变量污染；
3. 保护私有变量不会被随意修改；
4. 局部变量会常驻在内存中，会造成内存泄漏（有一块内存空间被长期占用，而不被释放）

### 2.2、定时器时间和闭包的执行

**需求：使用setTimeout开启10个定时器，分别输出 0,1,2,3,4,5,6,7,8,9。**

这么简单是需求，直接用for循环：

```js
for (var i = 0; i <10; i++) {
    setTimeout(function(){
        console.log(i);
    }, 1000);
}
```

for循环会一瞬间完成，定时器是异步，此时已经全部是10。

不好意思，结果输出了10个10，而不是我们需要的连续的数字。

方法一：立即执行函数

那么结果方案其实已经出来了，因为定时器中的函数没能立即执行才造成这个问题，那我们让它立即执行不就OK了吗！

```js
for (var i = 0; i <10; i++) {
    setTimeout(
        (function(){
        	console.log(i);
    	})(), //立即执行函数
    1000);
}
```

setTimeout第一个参数需要一个函数，此时传递的确是一个undefined。

方法二：闭包

```js
for (var i = 0; i < 10; i++) {
    function fun() {
        return function (j) {
            console.log(j);
        };
    }
    //如果setTimeout内函数需要参数
    //实参是在setTimeout的第二个参数（时间）之后。
    setTimeout(fun(), 1000 *i, i);
}
```

### 2.3、DOM事件和闭包的执行

延长事件返回值的生命周期

```html
<ul id=”test”>
    <li>这是第一条</li>
    <li>这是第二条</li>
    <li>这是第三条</li>
 </ul>
 
<script>
    var liList=document.getElementsByTagName('li');
  	//立即执行函数
    for (var i = 0; i < liList.length; i++) {
        (function fun(j) {
            liList[j].onclick=function () {
              	console.log('第'+ (j+1) +'个li');
            }
        })(i)
    }
  
  	// 闭包
    for (var i = 0; i < div.length; i++) {
      div[i].onclick=(function (j) {
        return function(){
          console.log('第'+ (j+1) +'个div');
        }
      })(i)
    }
</script>
```

## 三、递归

### 3.1、递归的基本结构（掌握）

定义：函数中用调用函数自己的结构称作递归

```javascript
function f1() {
	console.log("从前有座山，山里有个庙，庙里有个老和尚给小和尚讲故事：");
	f1();
};
f1();//浏览器崩溃，因为没有结束条件——死循环
```

**递归两个要素**

1.递归的边界——找到出口，在什么情况下跳出递归

2.递归的逻辑——找到入口，什么情况下重复调用自己，调用自己做什么

```javascript
var i=0;
function f1() {
	i++;
	if (i<5){// <5的时候就是入口
		f1();
	}        // =5的时候就是出口
	console.log("从前有座山，山里有个庙，庙里有个老和尚给小和尚讲故事：");
};
f1();
```

需求：封装一个方法，计算正整数num的阶乘（递归阶乘）

什么是阶乘（factorial）：所有小于及等于该数的正整数的积

```javascript
// 递归阶乘
function factorial(num) {
  if(num <= 1) { return 1 };
  return num * factorial(num - 1);
}
```

### 3.21、拷贝（掌握）

#### 3.2.1、浅拷贝实现

需求：就是将p1对象中的属性或者是方法拷贝到p2对象中。

我们首先想到是的for…in循环，将p1的属性拷贝一份到p2中：

```js
var p1 = {
    name:"zs",
    age:10,
    favs:["H5","Java","C"],
    wife:{
        name:"lily",
        age:8
    }
}
var p2 = {};
for(var key in p1){
    p2[key] = p1[key];
}
console.log(p2);
```

缺点：对象内属性是引用数据类型的话，拷贝过来的就是引用地址，并没有实现真正的拷贝，依然同一份数据。

#### 3.2.2、深拷贝实现

所以要实现深拷贝，当我们发现属性对应的值是一个对象或数组的时候，应该将该对象或数组再拷贝一份，然后赋值给当前属性。

思路：

1. 浅拷贝拷贝基本数据类型
2. 判断是否引用数据类型
3. 递归调用，完成所有层次拷贝
4. 判断value是数组还是对象

```js
var p={
  name:'小明',
  age:13,
  favs:['H5','Java','C'],
  wife:{
    name:'小丽',
    age:15,
    favs:['H5','Java','C']
  }
};
var p2={};
function deepCopy(source,target) {
  for (var Key in source) {
    //只拷贝当前对象的属性
    if(source.hasOwnProperty(Key)) {
      //选择引用数据类型
      if (typeof source[Key] == 'object') {
        //判断value是数组还是对象
        target[Key] = Array.isArray(source[Key]) ? [] : {};
        //递归，深层次拷贝
        deepCopy(source[Key], target[Key])
        //arguments.callee(source[Key],target[Key])
      }else{
        target[Key] = source[Key]
      }
    }
  }
}

deepCopy(p,p2)
console.log(p2);
```

通过上面的深度拷贝得到的p2对象是和p1完全不同的两份数据，此时不再存在数据共享的问题。

### 3.3、排序（至少掌握一种）

#### 3.3.1、冒泡排序法（Bubble Sort）

> 一种计算机科学领域的较简单的排序算法。
>
> 基本思路是：重复地走访过要排序的元素列，依次比较两个相邻的元素，如果顺序（如从大到小、首字母从Z到A）错误就把他们交换过来

![1552393446652](F:\\js高阶\JS面试题.assets\冒泡排序.png)

需求：将数组[5,3,9,4,6]按从大到小的顺序重新排序

```javascript
var arr = [5,3,9,4,6];
// 将数组中的数两两比对，调换顺序
// 轮数
for(var i = 0;i<arr.length-1;i++){
  // 次数
  for(var j = i+1;j<arr.length;j++){
    // var temp;
    if(arr[i]<arr[j]){
      /*temp = arr[i];
      arr[i]=arr[j];
      arr[j]=temp;*/
      [arr[i],arr[j]]=[arr[j],arr[i]];
    }
  }
}
console.log(arr)
```

#### 3.3.2、快速排序法（Quick Sort）

> 快速排序是对冒泡排序的一种改进。
>
> 基本思想是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

![1552393446652](F:\\js高阶\JS面试题.assets\快速排序法.png)

需求：随机获取10到999之间的100个整数，并且要从大到小排序，要求使用快速排序算法。

```javascript
//获取到min到max-1的total个随机数
function getRandomNum(total,min,max){
    let arr=[];
    for(let i = 0;i<total;i++){
        arr.push(Math.floor(Math.random()*(max-min)+min))
    }
    return arr
}


//快速排序算法
function arrSort(arr) {
    if (arr.length <= 1) { return arr; }
    var index = Math.floor(arr.length / 2);
    var middle = arr.splice(index, 1)[0];
    var left = [];
    var right = [];
    for (var i = 0; i < arr.length; i++) {
        if (arr[i] < middle) {
            right.push(arr[i])
        } else {
            left.push(arr[i])
        }
    }
    return arrSort(left).concat(middle, arrSort(right))
}
console.log(arrSort(getRandomNum(100,10,1000)))
```

## 四、作业

1. 【黄金】课堂代码写三遍(包含课堂写的，课堂没写完的写完)+**总结**--------**必须完成**;
2. 【铂金】预习后面的课程（设计模式、正则、执行栈……）
3. 【王者】[面试题](http://kumanxuan1.f3322.net:8360/static/interview/html/)，打开这个炫酷的网站，开始背面试题……



# day07-面试题精讲

> 今日要点：
>
> 1. 理解快速排序算法(难,听懂)
> 2. **两种数组去重的方法**
> 3. 能**说出三种设计模式实现原理**
> 4. 能**说出原生AJAX的执行流程**
> 5. 能理解原生AJAX发送请求的语法
> 6. **必须掌握JSON格式的概念和写法**(项目)
> 7. 了解eval函数如何转换JSON数据
> 8. 必须掌握**JSON对象的两个方法使用**

## 一、设计模式简单介绍（了解）

### 1.1、单例模式

定义：保证一个类仅有一个实例，并提供一个访问它的全局访问点。

核心：确保只有一个实例，并提供全局访问。

实现：假设要设置一个管理员，多次调用也仅设置一次，我们可以缓存一个内部变量来实现这个单例。

```js
var _instance;
function Person() {
   if(_instance){
            console.log('之前已经创建过,直接返回之前创建的对象');
            return _instance;
   }
   _instance = this;
   console.log("创建了对象");//第一次new会打印这句话
}
var p1 = new Person();
var p2 = new Person();
console.log(p1 === p2); // true，他俩是同一个对象
```

### 1.2、观察者模式（Observer pattern）

定义：定义了对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都将得到通知。

举例：

1. 售楼部的客服小姐姐---有新的房源---被观察者Subject
2. 直接通知给不同的潜在客户---观察者Observer
3. 不同客户做出不同的反应

画图说明：

![img](F:\\js高阶\JS面试题.assets\535435435435.png)

```javascript

```

### 1.3、发布-订阅模式（Publish–subscribe pattern）

定义：类似观察者模式，只有中间多了一个调度中心。

举例：

1. 售楼部的客服小姐姐---有新的房源---发布者（Publish）
2. 小姐姐将新的房源信息发布到一个公众号平台（调度中心）
3. 需要买房的用户（订阅者subscribe）看到公众号信息
4. 不同的客户做出不同的反应

画图说明：

![img](F:\\js高阶\JS面试题.assets\452355435435.png)

[易混淆点](https://zhuanlan.zhihu.com/p/51357583) ：很多资料都会将观察者模式和发布订阅模式混为一谈，因为都是存在两个角色实现一对多关系（被观察者-观察者，发布者-订阅者），确实容易混淆，他们忽略了发布订阅模式里的经纪人角色或者叫调度中心。

## 二、原生AJAX(xhr)

### 2.1、兼容处理

JS的Ajax对象：**XMLHttpRequest 对象用于在后台与服务器交换数据。**

创建ajax对象会有浏览器兼容性问题：

```js
function createAjax() {
  	var request;
    if(Windows.XMLHttpRequest){
        request=new XMLHttpRequest();
    }else{
      	request=new ActiveXObject("Microsoft.XMLHTTP"); //IE 5,IE6
    }
}
```

### 2.2、响应处理和响应流程（掌握）

响应处理，即对服务响应回浏览器的数据根据状态码和 AJAX 对象的状态信息进行不同的处理，在绑定状态改变的处理函数中写对应的逻辑代码即可。

AJAX 对象中有 4 个属性：

- readyState 总共有 5 个状态值，分别为 0 ~ 4，每个值代表了不同的含义：
  - 0：初始化，AJAX 对象还没有完成初始化
  - 1：载入，AJAX 对象开始发送请求
  - 2：载入完成，AJAX 对象的请求发送完成
  - 3：解析，AJAX 对象开始读取服务器的响应
  - 4：完成，AJAX 对象读取服务器响应结束
- status 表示响应的 HTTP 状态码，常见状态码如下：
  - **200 OK：请求成功**
  - **302 Found：重定向**，新的 URL 会在 response 中的 Location 中返回，浏览器将会使用新的 URL 发出新的 Request
  - **304 Not Modified：已缓存**，文档已经被缓存，直接从缓存调用
  - 400 Bad Request：客户端请求有语法错误，不能被服务器所理解
  - **403 Forbidden：服务器收到但拒绝服务**，引用外部资源触发防盗链
  - **404 Not Found：找不到资源**，请求资源不存在
  - **500 Internal Server Error：服务端错误**，服务器发生了不可预期的错误
  - 503 Server Unavailable：服务器当前不能处理客户端的请求，一段时间后可能恢复正常
- responseText 获得字符串形式的响应数据。
- responseXML  获得 XML 形式的响应数据。

综合以上，在状态改变的处理函数一般针对 readyState == 4 且 status == 200 的情况才处理，再根据后台返回的数据类型决定从 responseText 或者 responseXML 获取服务器响应回去来的数据。

![AJAX请求流程图](F:\\js高阶\JS面试题.assets\AJAX请求流程图.png)

### 2.3、使用ajax发送get请求

步骤：

```js
// 1、创建 AJAX 对象；new XMLHttpRequest()
// 2、设置请求路径，请求方式等；ajax.open(请求方式，路径)
// 3、绑定监听状态改变的处理函数，在处理函数可获取响应数据；ajax.onreadystatechange
// 4、发送请求。ajax.send
```

代码：

```html
<body>
    <button id="btn">发送get请求</button>
  
<script>
    btn.onclick = function(){
        // 1、创建 AJAX 对象；
        var ajax = new XMLHttpRequest();
        // 2、设置请求路径，请求方式等；ajax.open(请求方式，路径)
        ajax.open('get', 'http://kumanxuan1.f3322.net:8809/travels/query');
        // 3、绑定监听状态改变的处理函数，在处理函数可获取响应数据；
        ajax.onreadystatechange = function(){
            // console.log(ajax.readyState);
            if(ajax.readyState==4 && ajax.status==200){
                // 此时获取服务器发过来的数据
                console.log(ajax.responseText)	// 得到的是字符串对象，需要用JSON.parse(txt)转对象
            }
        }
        // 4、发送请求。
        ajax.send();
    }
</script>
</body>
```

### 2.4、使用ajax发送post请求

post请求需要传递参数给后台，

**常见的Content-Type**：

- application/x-www-form-urlencoded  浏览器默认
- application/json --------- JSON 字符串
- multipart/form-data ------- 文件类型

代码：

```html
<body>
	用户名：<input id="user" type="text"><br>
    密码：<input id="pwd" type="password"><br>
    <button id="btn">登录</button>

<script>
    // 后台要求携带参数：
    // 用户名 - username
    // 密码 - password
    btn.onclick = function () {
        // 1、创建 AJAX 对象
        var ajax = new XMLHttpRequest();
        // 2、设置请求路径，请求方式等
        ajax.open("post", "http://kumanxuan1.f3322.net:8809/users/login");
        // 3、设置请求头，不然无法传递参数到后台
        ajax.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
        // 4、绑定监听状态改变的处理函数
        ajax.onreadystatechange = function () {
            if (ajax.readyState == 4 && ajax.status == 200) {
                console.log(ajax.responseText);
            }
        }
        // 5、发送请求并携带参数
        ajax.send(`username=${user.value}&password=${pwd.value}`)
    }
</script>
</body>
```

## 三、JSON数据处理（掌握）

### 3.1、eval函数的基本使用

作用：将字符串类型的参数转换成JS代码。

eval函数Function的区别：

1. Function:需要调用函数，才会执行代码

2. eval：转换之后立即执行


在开发中的应用场景：

​	当获取到一个字符串类型的数据，但是想将其转换成JS代码执行的时候使用该函数可以实现

```js
var jsonStr = "({name:'Neld',age:10})";
console.log(eval(jsonStr));//转换成JS的对象
```

在实际开发中不建议使用eval函数，原因：

1. 存在安全隐患
2. 影响程序的执行性能
3. 事实上，目前只有后端在用eval这种方式，前端开发有更好的方式：JSON方法。

### 3.2、JSON数据格式

定义：JSON 格式（JavaScript Object Notation 的缩写）是一种用于数据交换的文本格式-----前后端数据交互的常见格式(尤其是后台数据,基本上都是json)。

JSON 对值的类型和格式有严格的规定：

1. 复杂数据类型的值只能是数组或对象，不能是函数、正则表达式对象、日期对象。
2. 原始类型的值只有四种：字符串、数值（必须以十进制表示）、布尔值和`null`（不能使用`NaN`, `Infinity`, `-Infinity`和`undefined`）。
3. 字符串必须使用双引号表示，不能使用单引号。
4. 对象的键名必须放在双引号里面。
5. 数组或对象最后一个成员的后面，不能加逗号。
6. 不能写注释

```javascript
// 以下都是合法的 JSON：

["one", "two", "three"]

{ "one": 1, "two": 2, "three": 3 }

{"names": ["张三", "李四"] }

[ { "name": "张三"}, {"name": "李四"} ]


// 以下都是不合法的 JSON：

{ name: "张三", 'age': 32 }  // 属性名必须使用双引号

[32, 64, 128, 0xFFF] // 不能使用十六进制值

{ "name": "张三", "age": undefined } // 不能使用 undefined

{ "name": "张三",
  "birthday": new Date('Fri, 26 Aug 2011 07:13:10 GMT'),
  "getName": function () {
      return this.name;
  }
} // 属性值不能使用函数和日期对象
```

**JSON对象**是 JavaScript 的原生对象，用来处理 JSON 格式数据。它有两个静态方法：

```javascript
JSON.stringify(JS对象);//序列化：JS对象转JSON字符串
JSON.parse('JSON字符串');//反序列化：JSON字符串转成相应的数据格式(JS对象)
```

需求：使用JSON方法实现深拷贝。

```javascript
var data = [
  { name: "小龙", age: 40 },
  { name: "老陈", age: 35 }
];
var jsonData=JSON.stringify(data);//JS对象转JSON字符串
console.log(jsonData);
var newData=JSON.parse(jsonData);//JSON字符串转成相应的数据格式(JS对象)
// 此时已经实现了深拷贝，它虽然很香，但是面试题不会考你用这种方式实现深拷贝
console.log(newData);
console.log('---------------------------------');
newData[0].age=50;
console.log(data);
console.log(newData);
```

## 四 、作业

1. 【黄金】课堂代码写三遍(包含课堂写的，课堂没写完的写完)+**总结**--------**必须完成**;
2. 【铂金】尽量每个人都尝试写一下第八天的编程题
3. 【王者】[面试题](http://kumanxuan1.f3322.net:8360/static/interview/html/)，打开这个炫酷的网站，开始背面试题……



1. ES6(必考)
   1. Promise基本语法 
   2. 箭头函数---------**this指向*5**------**它的特点*6**
   3. **声明变量和常量**
   4. 模板字符串
   5. **解构语法**
   6. **对象的简化写法**
   7. **函数参数默认值设置已经解构**
   8. **rest参数**---函数中使用
   9. **拓展运算符**
2. 面向对象(思想--造轮子)
   1. 构造函数
   2. 原型对象(共享成员给实例使用)
   3. 原型链--------通过`__proto__`往上去查找,直到找到为止,------就近原则
   4. 继承*6
      - **call apply-----借用方法**
   5. 基本包装类型
   6. 完整的原型链结构图
   7. **ES6 class**
3. 面试题(面试--造火箭)
   1. 异常捕获+严格模式
   2. 闭包
   3. 递归(入口,出口)
   4. 设计模式
   5. 原生ajax-----**json(语法还是方法)**
   6. 正则-----了解-----看懂,会简单修改
   7. 异步任务-------执行栈(先入后出)-----任务列队(先入先出)------宏任务微任务(先同步再异步,先微任务再宏任务)
   8. 编程题-----面试笔试,机试-----加强大家的处理数据的能力(建议深挖)

# day08-JS编程题

> 今日要点
>
> 1. 能看懂简单的正则表达式
> 2. 能根据规则简单修改正则表达式
> 3. 理解什么是执行栈及执行规则
> 4. 理解异步任务的执行顺序
> 5. 理解js编程题的思路
> 6. 重点是学会去套用思路解决问题

## 一、正则表达式（理解）

在开发中，尤其在表单里面，我们经常需要对字符串进行一定条件的限制。比如我们在注册的时候经常要用到手机号，那么怎么才能确定用户输入的是一个手机号？

像这种需求，我们一般使用正则来判断 ———— 也就说，正则的作用就是：**判断字符串是否满足一定的规则**

### 1.1、正则的创建

在js里面，已经封装好了一种对象：正则对象，所以我们每次使用，只需要创建出来就可以直接使用。创建正则对象的方式分种：

```js
// 构造函数
let reg = new RegExp('规则','匹配模式')
// 字面量
let reg = /pattern/flags;

/*
    pattern:正则表达式  
    flags:标识(修饰符)
      标识主要包括：
        1. i 忽略大小写匹配
        2. m 多行匹配，即在到达一行文本末尾时还会继续寻常下一行中是否与正则匹配的项
        3. g 全局匹配 模式应用于所有字符串，而非在找到第一个匹配项时停止
*/
```

其中修饰符是可以省略的，所以我们先大概给大家演示用法：

```js
// 匹配字符串里面有没有a
let reg = new RegExp('a')
// 或者
let reg = /a/
// 调用 test 方法对字符串进行验证
reg.test('123') // false
reg.test('abc') // true
```

### 1.2、正则表达式的规则

正则的基本使用还是比较简单的，难在我们要表达出我们想要的规则，而在正则中，使用不同的元字符来实现不同的规则。

[测试地址](https://regex101.com/)

**特定规则**

> \d 匹配数字   \D  和\d相反
>
> \w 匹配数字+字母+_    \W  和\w相反
>
> \s 匹配空白字符		\S  和\s相反

**数量限定**

> `*`     匹配特定规则出现任意次
>
> `+` 	匹配特定规则出现至少1次
>
> ?       匹配特定规则现出1或者0次（前面的字符可有可无）
>
> {n}	 匹配特定规则出现n次
>
> {n,}	  匹配特定规则出现至少n次
>
> {n,m}	 匹配特定规则出现n到m次

```js
ab+ * ？c
ab{1,3}c

ac
abc
abbbc
abbbbbbc
adc
adddddddc
```

**开关结尾限定**

> ^      	匹配特定规则开关
>
> $		  匹配特定规则结尾

例如：

```js
// 匹配手机号
// 1.手机号以1开关  2.共11位数字
/^1\d{10}$/
```

**范围限定**

范围限定使用的`[]`用法比较特殊，大概分为这么三种

> 1.连续范围
>
> [0-9]  匹配数字   [a-z]   匹配小写字母   [3-8]  匹配3到8之间的数字
>
> 2.范围集合
>
> [0-9a-zA-Z]   匹配数字+字母
>
> 3.无规律集合
>
> [259a-f*]    匹配2/5/9+a到f和`*`中的任意字符
>
> 4.取反
>
> [^0-9]		匹配非数字

**其它**

> .    匹配任意单个字符
>
> \     反斜杠 转义
>
> ()     分组
>
> |       或者

```js
// 手机号匹配
/^1[3|4|5|7|8][0-9]{9}$/.test(phone)
// 颜色值匹配
/^#[a-fA-F0-9]{6}$/.test("#FBB2h0")
```

## 二、异步任务（理解）

### 2.1、执行栈

想要想明白异步编程的执行顺序，首先要知道js代码是如何执行的。此时有一个概念一定要先知道：执行栈

执行栈，也称“调用栈”，是一种拥有 **后进先出** 的数据结构，被用来存储代码运行时创建的所有执行上顺序。

当 JavaScript 引擎第一次遇到你的脚本时，它会创建一个全局的执行环境并且压入当前执行栈。每当引擎遇到一个函数调用，它会为该函数创建一个新的执行环境并压入栈的顶部。

引擎会执行处于栈顶的执行环境的函数。当该函数执行结束时，执行环境从栈中弹出，控制流程到达当前栈中的下一个执行环境。

让我们通过下面的代码示例来理解：

```js
 console.log('全局环境开始');
let a = 10;

function first() {
  console.log('函数1');
  second();
  console.log('两次回到函数1');
}

function second() {
  console.log('函数2');
}

first();
console.log('全局环境结束');
```

上面的代码可以用这样的过程来理解

![](F:\\js高阶\JS面试题.assets\image-20210331151641670.png)

1.首先是全局的执行环境入栈

2.在全局环境下调用了first函数,再把first函数的环境压入栈中

3.在first函数里面调用了second函数，再把second函数的环境压入栈中

4.second执行完毕，于是把second的执行环境从栈中移除(先进后出，后入先出)

5.回到first的执行环境，再把fist的代码执行完成，从执行栈中再移除

6.最后把全局的执行环境也出栈，整个程序执行完成

### 2.2、EventLoop

`Event Loop`即事件循环，是指浏览器或`Node`的一种解决`javaScript`单线程运行时不会阻塞的一种机制，也就是我们经常使用**异步**的原理。

#### 2.2.1、javascript是单线程的

JavaScript语言的一大特点就是单线程，也就是说，**同一个时间只能做一件事**。那么，为什么JavaScript不能有多个线程呢？这样能提高效率啊。

JavaScript的单线程，与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？

所以，为了避免复杂性，从一诞生，JavaScript就是单线程，这已经成了这门语言的核心特征，将来也不会改变。

```js
// 异步任务---定时器
setTimeout(()=>{
    console.log("定时器1");
},2000)
setTimeout(()=>{
    console.log("定时器2");
},1000)
console.log("全局");
for(let i=0;i<10000;i++){
    console.log("靓仔");
}
```

#### 2.2.2、EventLoop和任务队列

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。如果前一个任务耗时很长，后一个任务就不得不一直等着。

如果排队是因为计算量大，CPU忙不过来，倒也算了，但是很多时候CPU是闲着的，因为IO设备（输入输出设备）很慢（比如Ajax操作从网络读取数据），不得不等着结果出来，再往下执行。

JavaScript语言的设计者意识到，这时主线程完全可以不管IO设备，挂起处于等待中的任务，先运行排在后面的任务。等到IO设备返回了结果，再回过头，把挂起的任务继续执行下去。

于是，所有任务可以分成两种，一种是**同步任务**（synchronous），另一种是**异步任务**（asynchronous）。同步任务指的是，在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；异步任务指的是，不进入主线程、而进入"任务队列"（task queue）的任务，只有"任务队列"通知主线程，某个异步任务可以执行了，该任务才会进入主线程执行。

具体来说，异步执行的运行机制如下。

```js
1.所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。
2.主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
3.一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。
4.主线程不断重复上面的第三步。
```

于是就会形成下面这样一个执行模型

<img src="F:\\js高阶\JS面试题.assets\image-20210331154715816.png" alt="image-20210331154715816" style="zoom:50%;" />



### 2.3 Task（宏任务）和 MicroTask（微任务）

而在代码的执行过程中，我们还把所有的分为两个大类，**宏任务**和**微任务**

| 宏任务                                       | 微任务                  |
| -------------------------------------------- | ----------------------- |
| script环境                                   | Promise的then/catch回调 |
| setInterval/setTimeout 定时器                | Object.observe(先忽略)  |
| requestAnimationFrame 浏览器的帧循环(先忽略) | Proxy(先忽略)           |
| UI Rendering 浏览器的UI渲染(先忽略)          |                         |

`Event Loop`中，每一次循环称为`tick`，每一次`tick`的任务如下：

执行栈在执行完同步任务后，查看执行栈是否为空，如果执行栈为空，就会去执行`Task`（宏任务），每次宏任务执行完毕后，检查微任务(`microTask`)队列是否为空，如果不为空的话，会先执行完微任务(`microTask`)后，设置微任务(`microTask`)队列为`null`，然后再执行宏任务，如此循环



以下面的代码为例：

```js
console.log('1');
setTimeout(function() {
    console.log('2');
    new Promise(function(resolve) {
        console.log('3');
        resolve();
    }).then(function() {
        console.log('4')
    })
})
new Promise(function(resolve) {
    console.log('5');
    resolve();
}).then(function() {
    console.log('6')
})
console.log('7')
```

执行过程如下

1. 全局打印1
2. 创建定时器，宏任务未执行
3. 创建Promise对象是同步，先执行打印5
4. 再次全局打印7
5. 执行微任务.then打印6
6. 执行宏任务定时器
7. 进入主线程，打印2
8. 同步代码创建Promise对象，打印3
9. 执行微任务.then打印4

所以最终的结果为： 1,5,7,6,2,3,4

## 三、编程题（掌握）

1. 两个数组，最终输出：['员工张三，29岁，工作于百度', '员工李四，26岁，工作于阿里巴巴'，...]

   ```javascript
   var employees = [
       {
           name: "张三", // 员工名字
           empId: 0, // 员工id
           age: 29, // 员工年龄
           compId: 1, // 所属公司id
       },
       {
           name: "李四",
           empId: 1,
           age: 26,
           compId: 2,
       },
       {
           name: "王五",
           empId: 2,
           age: 28,
           compId: 1,
       },
       {
           name: "小明",
           empId: 3,
           age: 32,
           compId: 3,
       },
   ];
   
   var companies = [
       {
           name: "百度", // 公司名称
           id: 1, // 公司id
       },
       {
           name: "阿里巴巴",
           id: 2,
       },
       {
           name: "腾讯",
           id: 3,
       },
   ];
   ```

2. 请把下列的数组变成是: [['苹果','胡萝卜', '花生'], ['梨', '西芹', '坚果']....]

   ```javascript
   var basket = [
       { fruit: "苹果", veg: "胡萝卜", nut: "花生" },
       { fruit: "梨", veg: "西芹", nut: "坚果" },
       { fruit: "香蕉", veg: "土豆", nut: "杏仁" },
       { fruit: "西瓜", veg: "豆芽", nut: "核桃" },
   ];
   ```


3. 程序实现对数据统计其出现的次数并按出现次数进行排序，[1, 4, 2, 1, 3, 2, 1, 4] 作为参数（参数可变）传入js方法中，控制台输出如下结果

   ```javascript
   1 出现了 3 次
   2 出现了 2 次
   4 出现了 2 次
   3 出现了 1 次
   ```

4. 实现二维数组行转列

   ```javascript
   var arr = [
       ["前端", "3人", "8-15k", "本科"],
       ["后端", "5人", "10-25k", "研究生"],
       ["UI", "2人", "9-11k", "大专"],
       ["ETL工程师", "10人", "6-12k", "大专"],
   ];
   
   转换 =>
   
   var newArr = [
       ["前端", "后端", "UI", "ETL工程师"],
       ["3人", "5人", "2人", "10人"],
       ["8-15k", "10-25k", "9-11k", "6-12k"],
       ["本科", "研究生", "大专", "大专"],
   ];
   ```

5. 对以下数据 取出每人(name)最大的销售量(sales)数据 ( 对sales排序对name去重)

   ```javascript
   var arr = [
       { name: "小明", year: 2019, sales: 53 },
       { name: "小明", year: 2020, sales: 234 },
       { name: "小明", year: 2018, sales: 24 },
       { name: "小强", year: 2019, sales: 31 },
       { name: "小强", year: 2020, sales: 567 },
       { name: "小强", year: 2018, sales: 678 },
       { name: "小红", year: 2019, sales: 465 },
       { name: "小红", year: 2020, sales: 82 },
       { name: "小红", year: 2018, sales: 576 },
       { name: "小马", year: 2019, sales: 4567 },
       { name: "小马", year: 2020, sales: 832 },
       { name: "小马", year: 2018, sales: 674 },
   ];
   [
       {name: '小明', year: 2020, sales: 234},
       {name: '小强', year: 2018, sales: 678},
       {name: '小红', year: 2018, sales: 576},
       {name: '小马', year: 2019, sales: 4567}
   ]
   ```

## 四、作业

1. 【黄金】课堂代码写三遍(包含课堂写的，课堂没写完的写完)--------**必须完成**;
2. 【铂金】回顾一下今天用到的数组对象方法，总结整理一下。**完成阶段总结**。
3. 【王者】[面试题](http://kumanxuan1.f3322.net:8360/static/interview/html/)，打开这个炫酷的网站，开始背面试题……

4. 【...】拓展编程题

1. ```js
   // 需求：请自定义一个函数，实现字符串的反转
   //'abcdefg' => 'gfedcba' 
   ```

2. ```js
   // 统计零食店所有零食的库存总数量
   var shopsLists = [
       {
           id: 1,
           name: "你好零食店-天河分店",
           areaid: 33,
           provice: 12,
           address: "广州市天河区",
           status: 0,
           storage: [
               // 库存
               { id: 23, name: "饼干", num: 106 },
               { id: 26, name: "牛奶", num: 290 },
               { id: 44, name: "可乐", num: 157 },
               { id: 80, name: "辣条", num: 457 },
           ],
       },
       {
           id: 2,
           name: "你好零食店-黄埔分店",
           areaid: 40,
           provice: 12,
           address: "广州市黄埔区",
           status: 0,
           storage: [
               { id: 23, name: "饼干", num: 30 },
               { id: 55, name: "瓜子", num: 99 },
               { id: 45, name: "棒棒糖", num: 75 },
               { id: 90, name: "面包", num: 75 },
           ],
       },
       {
           id: 3,
           name: "你好零食店-海珠分店",
           areaid: 60,
           provice: 12,
           address: "广州市海珠区",
           status: 0,
           storage: [
               { id: 44, name: "可乐", num: 155 },
               { id: 26, name: "牛奶", num: 70 },
               { id: 45, name: "棒棒糖", num: 41 },
               { id: 90, name: "面包", num: 317 },
           ],
       },
   ];
   // 转换 =>
   // [{id: 44, name: '可乐', count: 312}, {id: 90, name: '面包', count: 392}.........]
   
   ```

3. ```js
   //剔除不及格的学生,得到一个新的学生数组
   
   let arr1 = [
       {
           id: 1,
           groupname: "小组1",
           students: [
               { id: 1, name: "张小娴", score: 90 },
               { id: 2, name: "李小宏", score: 70 },
               { id: 3, name: "吴小说", score: 40 },
               { id: 4, name: "五小加", score: 99 },
           ],
       },
       {
           id: 1,
           groupname: "小组2",
           students: [
               { id: 5, name: "问小世", score: 60 },
               { id: 6, name: "萨小斯", score: 50 },
               { id: 7, name: "权小韦", score: 80 },
               { id: 8, name: "离小天", score: 55 },
           ],
       },
       {
           id: 1,
           groupname: "小组3",
           students: [
               { id: 9, name: "世小想", score: 70 },
               { id: 10, name: "邓小睿", score: 78 },
               { id: 11, name: "沃小考", score: 90 },
               { id: 12, name: "沙小酱", score: 59 },
           ],
       },
   ];
   // 转换 =>
   /* let newArr = [
                 {
                   id: 1,
                   groupname: "小组1",
                   students: [
                     { id: 1, name: "张小娴", score: 90 },
                     { id: 2, name: "李小宏", score: 70 },
                     { id: 4, name: "五小加", score: 99 },
                   ],
                 },
                 {
                   id: 1,
                   groupname: "小组2",
                   students: [
                     { id: 5, name: "问小世", score: 60 },
                     { id: 7, name: "权小韦", score: 80 },
                   ],
                 },
                 {
                   id: 1,
                   groupname: "小组3",
                   students: [
                     { id: 9, name: "世小想", score: 70 },
                     { id: 10, name: "邓小睿", score: 78 },
                     { id: 11, name: "沃小考", score: 90 },
                   ],
                 },
               ]; */
   
   ```

4. ```js
   // 根据数组挑选出每个小组留下来的学生信息
   
   let arr2 = [
       {
           id: 1,
           groupname: "小组1",
           students: [
               { id: 1, name: "张小四", score: 90 },
               { id: 2, name: "李小宏", score: 70 },
               { id: 3, name: "吴小说", score: 40 },
               { id: 4, name: "五小加", score: 99 },
           ],
       },
       {
           id: 2,
           groupname: "小组2",
           students: [
               { id: 5, name: "问小世", score: 60 },
               { id: 6, name: "萨小斯", score: 50 },
               { id: 7, name: "权小韦", score: 80 },
               { id: 8, name: "离小天", score: 55 },
           ],
       },
       {
           id: 3,
           groupname: "小组3",
           students: [
               { id: 9, name: "世小想", score: 70 },
               { id: 10, name: "邓小睿", score: 78 },
               { id: 11, name: "沃小考", score: 90 },
               { id: 12, name: "沙小酱", score: 59 },
           ],
       },
   ];
   let arr1 = [1, 6, 5, 3, 11, 4];
   // 转换 =>
   /* let newArr = [
           {
             id: 1,
             groupname: "小组1",
             students: [
               { id: 1, name: "张小四", score: 90 },
               { id: 3, name: "吴小说", score: 40 },
               { id: 4, name: "五小加", score: 99 },
             ],
           },
           {
             id: 2,
             groupname: "小组2",
             students: [
               { id: 5, name: "问小世", score: 60 },
               { id: 6, name: "萨小斯", score: 50 },
             ],
           },
           {
             id: 3,
             groupname: "小组3",
             students: [{ id: 11, name: "沃小考", score: 90 }],
           },
         ]; */
   ```

5. ```js
   // 需求：假设有如下字符串“A12”，其中“A”表示数据类型（A-Z），“12”表示数据序号（0-9）。
   // 现在需要对一组数据 先按照数据序号 再按照数据类型(字母)进行排序。
   // 例如：["B3","D2","F1","A9","D12","A2","C1","Z0","B1"]=>		["Z0","B1","C1","F1","A2","D2","B3","A9","D12"]
   
   
   // 思路：先对首字母排序，再对数字排序
   ```
