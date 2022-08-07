# Vue第一天

## 学习目标

能够说出Vue框架的特点

能够写出Vue的插值语法（{{  }}的写法）

能够写出v-bind，v-on基本指令及其简写

能够写出使用Vue代码的基本格式(Vue对象、数据、方法)

能够写出Vue动态控制控制类名的案例

能够写出使用Vue的选项卡案例

能够说出v-if和v-show的区别

能够写出v-for对数组和对象数据进行渲染的基本格式

能够说出什么是双向数据绑定

能够写出v-model表单数据绑定(双向数据绑定)案例

## 一、Vue简介

Vue (读音 /vjuː/，类似于 view)，不要读错。

Vue是一个渐进式的前端框架，什么是渐进式的呢？  VUE全家桶

​		渐进式意味着你可以将Vue作为你应用的一部分嵌入其中，或者如果你希望将更多的业务逻辑使用Vue实现，那么Vue的核心库以及其生态系统。比如Core+Vue-router+Vuex+axios，也可以满足你各种各样的需求。

Vue的特点和Web开发中常见的高级功能：

​		1、解耦视图和数据

​		2、双向数据绑定

​		3、可复用的组件

​		4、前端路由技术

​		5、状态管理

​		6、虚拟DOM

学习Vuejs的前提？

​		从零学习Vue开发，并不需要你具备其他类似于Angular、React，甚至是jQuery的经验，但是你需要具备一定的HTML、CSS、JavaScript基础。

**注意：**

​		**学习Vue框架，必须严格遵循他的语法规则，Vue代码的书写思路和以前的JQuery完全不一样。所以，在项目中使用Vue之前，必须先学习Vue的基本语法规则。**



## 二、Vue 安装使用

项目里引入Vue的方式：（在项目中使用vue）

使用一个框架，我们第一步要先下载安装它

使用Vue的方式有很多：

方式一：直接CDN引入

```html
<!-- 开发环境版本，包含了有帮助的命令行警告 --> 
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
```

方式二：下载和引入

```js
// 开发环境 https://vuejs.org/js/vue.js
// 生产环境 https://vuejs.org/js/vue.min.js
```

方式三：NPM安装（今天先不掌握）

​		后续通过Vue-Cli3(脚手架)方式引入，我们使用该方式



**添加VSCode的模板：**

文件 -> 首选项 -> 用户代码片段，在输入框内输入html.json，用下面的代码覆盖掉原来的即可，下次新建html文件直接输入**hv**，然后按下回车即可

```js
{
	"html:5": {
		"prefix": "hv",
		"body": [
			"<!DOCTYPE html>",
			"<html>",
			"<head>",
				"\t<meta charset=\"UTF-8\">",
				"\t<meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">",
				"\t<meta http-equiv=\"X-UA-Compatible\" content=\"ie=edge\">",
				"\t<title></title>",
				"\t<script src=\"https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js\"></script>",
			"</head>",
			"<body>",
				
			"</body>",
			"</html>",
		],
		"description": "HTML5"
	}
}
```



## 三、体验Vue

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title></title>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
</head>
<body>
    <div id="app">
        {{ str1 }}
    </div>
</body>
<script>
    
    var vm = new Vue({    //这个Vue对象用来控制某一个标签里面的数据
        el:"#app",   //要控制的标签
        data:{
            str1:"hello vue",   //定义一个数据，在id为app的标签内部去使用
        }
    })
</script>
</html>
```

上面的代码做了什么事情？(了解，重点掌握格式的书写！)

1. 先看js代码，会发现创建了一个Vue对象

2. 创建Vue对象的时候，传入了一个对象：{}

   2.1 {}中的el属性：该属性决定了这个Vue对象挂载到哪一个元素上，很明显，我们这里挂载到了id为app的元素上。

   2.2 {}中包含了data属性：该属性中通常会存储一些数据，好像上面例子中的str1就是直接定义出来的数据



## 四、Vue常见的语法格式（重点）

#### 4.1、模板语法的初步认识

```html
	<div id="app">
        <p>{{ str1 }}</p>
        <p>{{ str1.split("").reverse().join("") }}</p>
        <p>{{num+1}}</p>
        <p>num1和numn2的最大值是：{{ num1>num2 ? num1 : num2 }}</p>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                str1:"hello",
                num:20,
                num1:40,
                num2:80
            }
        })
    </script>
```



#### 4.2、v-bind控制标签属性

```html
	<div id="app">
        <a v-bind:href="bd">百度</a>
        <a :href="tb">淘宝</a>
        <a :href="tb">淘宝</a>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                bd:"https://www.baidu.com",
                tb:"https://www.taobao.com"
            }
        })
    </script>
```

#### 4.3、v-on事件格式

```html
	<div id="app">
        <p>{{num}}</p>
        <button v-on:click="num+=1">点我数字增加</button>
        <button v-on:click="add">点我数字加5</button>
        <button @click="add2(10)">点我数字加10</button>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                num: 20
            },
            methods:{
                add:function(){
                    this.num += 5
                },
                add2(){
                    this.num += 10
                }
            }
        })
    </script>
```

#### 4.4、定义Vue对象基本格式总结

```js
	var vm = new Vue({
        el: "要绑定的标签",
        data: {
            变量名1：值1,
            变量名2：值2,
            变量名3：值3,
            ...

        },
        methods: {
            方法名1: function(){

            },
            方法名2: function(){

            },
            方法名3: function(){

            }
        }
    });
```

## 五、vue控制类名和style样式(动态控制类名)（重点）

```html
	<div id="app">
        <!--控制标签的类名 :class= 的值可以是 js对象 {类名：布尔值} -->
        <div class="box" :class="{box1:bool1, box2:bool2}"></div>

        <!--控制标签的类名 :class= 的值可以是 数组 [类名1，类名2] -->
        <div class="box" :class="['box3', 'box4']"></div>
        
        <!--掌握-->
        <div class="box" :class=" bool3 ? 'current':'' "></div><!--通过控制bool3位真还是假，来控制这个盒子有还是没有current这个类-->
        
        
        <div :style="{fontSize:'40px' }">文字</div>
        <div :style="{ fontSize:false?'40px' : '50px'}">文字</div>
        <div :style="[{fontSize:false?'40px' : '50px'},{background:'pink'}]">文字</div>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                bool1:true,
                bool2:false,
                bool3:true
            }
        })
    </script>
```

## 六、选项卡案例

```html
	<div class="tab_con" id="app">
        <div class="tab_btns">
            <input type="button" value="按钮一" :class="num==1? 'active':''" @mouseover="num=1">
            <input type="button" value="按钮二" :class="num==2? 'active':''" @mouseover="num=2">
            <input type="button" value="按钮三" :class="num==3? 'active':''" @mouseover="num=3">
        </div>
        <div class="tab_cons">
            <div :class="num==1? 'current':''">按钮一对应的内容</div>
            <div :class="num==2? 'current':''">按钮二对应的内容</div>
            <div :class="num==3? 'current':''">按钮三对应的内容</div>
        </div>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                num:1
            }
        })
    </script>
```



## 七、v-if和v-show指令（重点）

v-if 和v-show都是来控制标签是否显示，但是也有区别，v-show是对样式层面的控制，v-if是对dom节点的控制。

```html
<div id="app">
        <!-- v-if指令的作用： 控制标签是否展示，不展示则删除-->
        <!--<div v-if="bool1">1111111</div>-->
        <!--<div style="display:none">2222222</div>-->

        <!--bool1的值为true 第一个盒子被保留，删除第二个盒子，
        为false的话，第2个盒子保留，删除第1个盒子-->
        <!--<div v-if="bool1">11111</div>-->
        <!--<div v-else>222222</div>-->

        <!--<div v-if="type=='a'">11111</div>-->
        <!--<div v-else-if="type=='b'">2222</div>-->
        <!--<div v-else-if="type=='c'">3333</div>-->
        <!--<div v-else>4444</div>-->

        <!--不会删除标签，根据bool1是true还是false决定盒子是显示还是隐藏(在控制display属性的值)-->
        <div v-show="bool1">v-show的用法</div>


    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                bool1: false,
                type: "z"
            }
        })
    </script>
```

点击收藏按钮案例：

```html
<!-- <button v-if="!collectStatus" @click="collectStatus=!collectStatus">点击收藏</button>
        <button v-else @click="collectStatus=!collectStatus">取消收藏</button> -->

<button v-show="!collectStatus" @click="collectStatus=!collectStatus">点击收藏</button>
<button v-show="collectStatus" @click="collectStatus=!collectStatus">取消收藏</button>

<script>
    var vm = new Vue({
        el:".tab_con",
        data:{
            num:1,
            collectStatus:false
        }
    })
</script>
```



## 八、列表和对象的渲染(初步使用)（重点）

```html
 <div id="app">
        <ul>
            <!--i是列表中的每一个数据-->
            <li v-for="i in list1">{{ i }}</li>
        </ul>
       <ul>
            <!--i是列表中的每一个数据 j是每一个数据的下标-->
            <li v-for="(i, j) in list1">{{ i }} {{ j }}</li>
        </ul>

       <ul>
           <!--i是my_obj对象中的值-->
           <li v-for="i in my_obj">{{i}}</li>
       </ul>

       <ul>
           <!--i是my_obj对象中的值 j是my_obj对象中的键名-->
           <li v-for="(i, j) in my_obj">{{i}}  {{j}}</li>
       </ul>

   </div>
   <script>
       var vm = new Vue({
           el:"#app",
           data:{
               list1: ["javascript", "html", "css", "vue", "react"],
               my_obj: {
                   name: "javascript",
                   age: 24
               }
           }
       })
   </script>
```



## 九、表单数据绑定(双向数据绑定)（重点）

v-model的值是，vue接收表单元素的值的变量名， 即v1的值就是用户填写的内容
(甚至可以在data中设置v1的值，从而设置表单元素的默认值)

 ```html
<input type="text" v-model="v1"> 
<div>{{v1}}</div>
 ```

具体代码：

```html
	<div id="app">
        <input type="text" v-model="txt1">  <!-- v-model表示了用户输入的这个数据-->
        <p>{{ txt1 }}</p>

        <select v-model="sel1">
            <option value="0">北京</option>
            <option value="1">上海</option>
            <option value="2">广州</option>
        </select>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                //通过改变txt1或者sel1，来使对应的表单元素的v-model的值发生了变化，所以这个表单元素的value就变化了(v-model看成我们之前将的value)
                txt1: '默认值',
                sel1: 0
            }
        })
    </script>
```

## 十、Vue中的MVVM

### 什么是MVVM

> 1. View层：
>
> 视图层，在前端里就是我们常说的DOM层，主要作用是给用户展示各种信息；
>
> 2. Model层：
>
> 数据层，数据可能是我们自定定义的数据，或者是从网络请求下来的数据；
>
> 3. ViewModel层：
>
> 视图模型层，是View层和Model层沟通的桥梁；一方面它实现了数据绑定（Data Binding），将Model的改变实时反应到View中；另一方面它实现了DOM监听，当DOM发生改变可以对应改变数据（Data）

![1568691099973](F:\0001my\Notes\Vue.assets\1568691099973.png)

# Vue第二天

## 学习目标

能够写出reduce方法计算求数组中的和

能够写出Vue中计算属性computed中定义的函数

能够写出Vue中计算属性computed中定义的函数的调用格式

能够举例证明Vue中计算属性computed有缓存作用

能够写出:value和@input代替v-model的案例

能够写出数组常用的方法

能够写出reduce,filter,map的案例

能够写出数组去重案例

## 一、模板语法的插值操作(其他不常用指令)

v-html    往标签内部插入html文本

v-text    往标签内部插入普通文本(解析不了标签)

v-pre    在界面上直接展示胡子语法

v-cloak    隐藏数据渲染到页面之前，胡子语法在界面上的展示

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    [v-cloak] {
      display: none;
    }
  </style>
</head>
<body>
  <div id="app">
    <div v-html="htmlTxt"></div>
    <div v-text="textTxt"></div>
    <div v-pre>{{123}}</div>
    <div v-cloak>hello {{textTxt}}</div>
  </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  let vm = new Vue({
    el: '#app',
    data: {
      htmlTxt: '<p><strong>我是html</strong></p>',
      textTxt: 'Vue'
    }
  })
</script>
</html>
```



## 二、reduce方法的使用

 利用reduce方法遍历数组的每一个元素，reduce()调用结果最后返回一个最终值（最后一次return值）。

```js
	var arr = [
       {name: 'Vuejs入门', price: 99, count: 3},
       {name: 'Vuejs底层', price: 89, count: 1},
       {name: 'Vuejs从入门到放弃', price: 19, count: 5},
    ]

    //数组名.reduce(回调函数，pre的初始值)
    arr.reduce(function(pre, current){
        // reduce这个方法被调用时，会遍历arr这个数组的每一个元素，每遍历一个元素，就执行一次这里的代码
        // current表示当前正在遍历的这个元素
        // pre 是上一次的这个函数return的值
        // ！！！因为第一次遍历没有上一个return值，所以，交给了第二个参数，设置pre的初始值
        console.log(pre, current)
        return 10
    },0)

	//！！！并且reduce方法最终会返回最后一次的return值
```



上面代码的输出结果：

```
0 {name: "Vuejs入门", price: 99, count: 3}
10 {name: "Vuejs底层", price: 89, count: 1}
10 {name: "Vuejs从入门到放弃", price: 19, count: 5}
```



理解了上面的案例之后，就可以提一个需求：计算上面购物车的总价（每一个 price*count 的和），

```js
	//reduce方法最终会返回最后一次的return值
    var a = arr.reduce(function(pre, current){

        console.log(pre, current)

        // var total = 当前这次的 price*count + 上一次的total
        var total = current.price*current.count + pre
        return total
    },0)

    alert(a)   //这个a就是上面购物车的总价
```

备注：上面这个reduce()方法和Vue本身没有关系，纯粹是一个js数组的方法。



## 三、(重点)Vue的计算属性computed 的使用

我们把上一节的案例在Vue中使用（结合Vue对象的computed属性）：

```html
	<div id="app">
        {{total}}
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                arr: [
                    {name: 'Vuejs入门', price: 99, count: 3},
                    {name: 'Vuejs底层', price: 89, count: 1},
                    {name: 'Vuejs从入门到放弃', price: 19, count: 5},
                ]    
            },
            computed:{
                //computed里面的方法必须有返回值！这个return值将来在视图中被{{total}}引用
                total(){
                    var a = this.arr.reduce(function(pre, current){

                        console.log(pre, current)

                        // var total = 当前这次的 price*count + 上一次的total
                        var total = current.price*current.count + pre
                        return total
                    },0)
                    return a
                }
            }

        })
    </script>
```

## 四、(重点)computed内部方法有缓存的作用

以下代码total调用了三遍，却只执行了1遍，这是computed内部方法的缓存起了作用

```html
	<div id="app">
        {{total}}
        {{total}}
        {{total}}
        {{getTotal()}}
        {{getTotal()}}
        {{getTotal()}}
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                arr: [
                    {name: 'Vuejs入门', price: 99, count: 3},
                    {name: 'Vuejs底层', price: 89, count: 1},
                    {name: 'Vuejs从入门到放弃', price: 19, count: 5},
                ]    
            },
            methods:{
                getTotal(){
                    console.log("getTotal")
                    var a = this.arr.reduce(function(pre, current){

                  

                    // var total = 当前这次的 price*count + 上一次的total
                    var total = current.price*current.count + pre
                    return total
                    },0)
                    return a
                }
            },
            computed:{
                //computed里面的方法必须有返回值！这个return值将来在视图中被{{total}}引用
                total(){
                    console.log("total")
                    var a = this.arr.reduce(function(pre, current){

                        // var total = 当前这次的 price*count + 上一次的total
                        var total = current.price*current.count + pre
                        return total
                    },0)
                    return a
                }
            }

        })
    </script>
```

## 五、computed内部方法的另一种写法(知道有get和 set的格式)

```js
		....
		computed:{
                //computed里面的方法必须有返回值！这个return值将来在视图中被{{total}}引用
                total:{
                    get(){
                        console.log("total_get")
                        var a = this.arr.reduce(function(pre, current){

                            // var total = 当前这次的 price*count + 上一次的total
                            var total = current.price*current.count + pre
                                return total
                            },0)
                            return a
                    },
                    set(){
                        console.log("total_set")
                    },
                }
            }
	...
    

vm.total = 3   //触发调用set方法
```

## 六、使用:value和@input代替v-model

`v-model` 本质上包含了两个操作：

1. `v-bind` 绑定input元素的value属性
2. `v-on` 指令绑定input元素的input事件

即：:value="txtVal" 和 @input="handleInput"

```html
	<div id="app">
        <!-- <input type="text" v-model="txtVal"> -->
        <input type="text" :value="txtVal" @input="handleInput">
        <p>{{ txtVal }}</p>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                txtVal:""
            },
            methods:{
                handleInput(e){
                    console.log(e)
                    this.txtVal = e.target.value
                }
            }
        })
    </script>
```

即：

```html
<input type="text" v-model="textVal"/>
<!-- 等同于 -->
<input type="text" v-bind:value="textVal" v-on:input="textVal = $event.target.value"/>
```



## 七、(重点)数组常用的操作(方法)

#### 7.1、常用方法使用

push    pop    unshift    shift    splice    concat

```js
var arr = [1, 2, 3]
// 往数组最后一位添加一个数字
arr.push(4) // [1, 2, 3, 4]
// 删除数组最后一个数字
arr.pop()   // [1, 2, 3]
console.log(arr)
// 往数组第一位添加一个数字
arr.unshift(0)
console.log(arr)
// 删除数组第一个元素
arr.shift()
console.log(arr)
// splice
// 删除第一个元素
arr.splice(1, 2) 
console.log(arr)
arr.splice(1, 2, 2, 4, 5) 
console.log(arr)
// 合并数组
console.log([1, 6].concat([5, 7]))
```

push（返回数组长度）、unshift（返回数组长度）、shift（返回删除的值）、pop（返回删除的值）、splice、concat（返回新数组）

#### 7.2、reduce、filter、map

```js
	var arr = [1, 2, 3]

    // 计算总数
    var ret1 = arr.reduce((pre, current)=>{
        pre += current
        return pre
    }, 0)
    console.log(ret1)  // 6

    // filter (过滤)
    var ret2 = arr.filter(item =>{
        return item > 2
    })
    console.log(ret2)  // [3]
 
    // map 
    var ret3 = arr.map(item =>{
        return {id:item}
    })
    console.log(ret3)   // [{id: 1}, {id: 2}, {id: 3}]
```

#### 7.3、数组去重

```js
	var arr2 = [1, 2, 3, 1, 6, 2, 3]

    //ES6
    consoloe.log([...new Set(arr2)])
    console.log(Array.from(new Set(arr2)))

    var newArray = [];
    for(var i=0; i<arr2.length; i++){
        if(newArray.indexOf(arr2[i])==-1){
            newArray.push(arr2[i])
        }
    }
    console.log(newArray)

    var newArray2 = [];
    var obj = {};
    for(var i=0; i<arr2.length; i++){
        if(!obj[arr2[i]]){ //如果不在obj中，就表示不重复的数据，就在对象中添加键值对

            obj[arr2[i]] = arr2[i]
            newArray2.push(arr2[i])
        }
    }
    console.log(newArray2)
```



## 九、图书购物车例子

![1568800293540](F:\0001my\Notes\Vue.assets\1568800293540.png)

```html
<div id="app">
        <table>
            <thead>
                <tr >
                    <th v-for="(title, tidx) in titles" :key="tidx">{{title}}</th>
                    <!-- <th>书籍名称</th>
                    <th>价格</th>
                    <th>出版日期</th>
                    <th>数量</th>
                    <th>操作</th> -->
                </tr>
            </thead>
            <tbody>
                <tr v-for="(book,bidx) in books" :key="book.name">
                    <td>{{bidx}}</td>
                    <td>{{book.name}}</td>
                    <td>{{book.price}}</td>
                    <td>{{book.date}}</td>
                    <td>
                        <button @click="sub(bidx)">-</button>
                        {{book.num}}
                        <button @click="add(bidx)">+</button>
                    </td>
                    <td>
                        <button @click="remove(bidx)">移除</button>
                    </td>
                </tr>
            </tbody>
        </table>
        <div>总价格:{{total}}</div>
    </div>
    <script>
        new Vue({
            el: '#app',
            data: {
                titles: ['编号', '书籍名称', '出版日期', '价格', '数量', '操作'],
                books: [
                    {
                        name: '算法导论',
                        date: '2006-9',
                        price: 85,
                        num: 1
                    },
                    {
                        name: 'UNIX编程艺术',
                        date: '2006-2',
                        price: 59,
                        num: 1
                    },
                    {
                        name: 'Vue程序设计',
                        date: '2008-10',
                        price: 35,
                        num: 1
                    },
                    {
                        name: '颈椎康复',
                        date: '2006-3',
                        price: 129,
                        num: 1
                    },
                ]
            },
            // 定义方法的地方
            methods: {
                add(idx) {
                    console.log(idx)
                    this.books[idx].num++
                },
                sub(idx) {
                    if (this.books[idx].num) {
                        this.books[idx].num--
                    }
                    
                },
                // 移除方法
                remove(idx) {
                    // 修改 增加 删除(下标, 删除数量, .....增加的元素)
                    this.books.splice(idx, 1)
                }
            },
            // 计算属性
            computed:{
                total() {
                    return this.books.reduce((pre, current) => {
                        return pre + current.price * current.num
                    }, 0)//总价格
                }
            }
        })
    </script>
```





# Vue第三、四天

## 学习目标

能够写出Vue中过滤器和全局过滤器

能够写出localStorage的设置、获取和删除格式

能够写出sessionStorage的设置、获取和删除格式

能够写出使用 Object.defineProperty定义对象属性的格式

能够写出实现双向数据绑定原理的代码

能够写出全局自定义指令和局部自定义指令的格式(了解)

能够写出全局自定义组件和局部自定义组件的格式(重点掌握)

能够写出父级组件向子级组件传值的代码格式



## 一、（掌握）本地存储

#### 1.1、localStorage永久存储

```js
// 添加数据；setItem的value值是字符串类型的数据
localStorage.setItem('name','张三')；
// 获取数据
localStorage.getItem('name'); // 张三
// 清空
localStorage.clear();
```

**注意事项：**

> 1. 除非是主动删除，不然是不会自动删除的
> 2. 一般浏览器存储的大小是5M
>
>  5M = 1024 * 5kb

  前端缓存

#### 1.2、sessionStorage临时会话存储

```js
// 添加数据；setItem的value值是字符串类型的数据
sessionStorage.setItem('name','张三')；
// 获取数据
sessionStorage.getItem('name'); // 张三
// 清空
sessionStorage.clear();
```

**注意事项：**

> 1. 关闭浏览器会自动清空数据
> 2. 一般浏览器存储的大小是5M



#### 3. cookie   状态保持

> 1. cookie:
>
> 网站中，**http请求是无状态**的。也就是第一次登陆成功（发送请求），第二次请求服务器依然不知道是哪一个用户。这时候的cookie就是解决这个问题的，第一次登陆后服务器返回数据（cookie）给浏览器，然后浏览器保存在本地，当该用户发送第二次请求，浏览器自动会把上次请求存储的cookie数据自动带上给服务器，服务器根据客户端的cookie来判断当前是哪一个用户。cookie存储有大小限制，不同浏览器不一样，一般是4kb，所以cookie只能存储小量数据。
>
> 4kb = 4 * 1024 byte (字节) =  4 * 1024 * 8 bit（位）
>
> token: 用户登录凭证，服务端返回给浏览器（前后端分离项目，基本都是发送ajax请求）
>
> 2. session：
>
> session和cookie的作用有点类似，也是存储用户相关信息。不同的是cookie存储在浏览器，而session存储在服务器。



## 二、Vue指令

vue框架特点：双向数据绑定与组件化开发

#### 2.1、(重点) 深入双向数据绑定原理

> Vue 最独特的特性之一，是其非侵入性的响应式系统。数据模型仅仅是普通的 JavaScript 对象。而当你修改它们时，视图会进行更新。Vue里面是怎么做到的的呢？其实就是使用了`Object.defineProperty` 把Vue内的属性全部转成 `getter/setter`。`Object.defineProperty` 是 ES5 中一个无法 shim 的特性，这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。

 `Object.defineProperty` 实现了**对象劫持**这个功能

> <https://github.com/vuejs/vue/blob/1.0/src/observer/index.js>
>
> <https://github.com/vuejs/vue/blob/2.6/src/core/observer/index.js>

> vue双向数据绑定原理：
>
> <font color="red">**借助Object.defineProperty()对数据进行劫持，并结合发布-订阅者模式，来实现双向数据绑定**</font>

**语法：**

> Object.defineProperty(obj, prop, desc)
>
> 1. `obj` 需要定义属性的当前对象
> 2. `prop` 当前需要定义的属性名
> 3. `desc` 属性描述符



**数据属性：**

> 通过Object.defineProperty()为对象定义属性，有两种形式，分别为数据描述符，存取描述符，下面分别描述两者的区别：
>
> 1. `value` 表示它的默认值  
> 2. `writable` 如果为true标识可以被修改，如果为false标识不能被修改（默认值为false）
> 3. `configurable` 描述属性是否配置，以及可否删除，可以认为是总开关 默认值 false（不可删除）
> 4. `enumerable` 描述属性是否出现在for in 或者 Object.keys()的遍历中 默认值false(不能遍历)



```js
let obj = {};
Object.defineProperty(obj, 'name', {
    value: '张三'
})
obj.name = '李四'
console.log(obj.name) // 张三

```



```js
let obj = {};
Object.defineProperty(obj, 'name', {
    value: '张三',
    writable: true
})
obj.name = '李四'
console.log(obj.name)
```



```js
let obj = {};
  Object.defineProperty(obj, 'name', {
    value: '张三',
    writable: true,
    configurable: true,
    enumerable: true
  })
  obj.name = '李四'
  // delete obj.name
  console.log(obj.name) // 李四
  console.log(Object.keys(obj)) // ['name']
```



**存取属性：**

```js
let obj = {};
let temp = null;
Object.defineProperty(obj, 'name', {
    get() {
        return temp
    },
    set(val) {
        temp = val
    }
})
obj.name = '李四'
console.log(obj.name)
```

面试题回答：

> vue的双向数据绑定原理是什么？
>
> vue数据双向绑定是通过数据劫持结合“发布者-订阅者模式”的方式来实现的。
> vue是通过Object.defineProperty()来实现数据劫持，其中会有getter()和setter方法；当读取属性值时，就会触发getter()方法，在view中如果数据发生了变化，就会通过Object.defineProperty()对属性设置一个setter函数，当数据改变了就会来触发这个函数；
>
> 参考：https://segmentfault.com/a/1190000014274840
>
> 参考：https://zhuanlan.zhihu.com/p/51357583

#### 2.2、自定义指令

除了一些内置的制定（v-model和v-show...）,Vue也允许注册自定义指令。

全局自定义指令格式：

```js
// 注册一个全局自定义指令 v-demo
Vue.directive('demo', {
	inserted: function (el, binding) {
		
		console.log(el, binding);
	},
    update(el, binding){}
})
```

局部自定义指令格式：

```js
// 组件中注册局部指令
new Vue({
	el: '#app',
	data: {},
	directives: {
		demo: {
			inserted: function (el, binding) {
				cosnole.log(el, binding);
			}
		}
	}
})
```

自定义指令的使用：

```html
// 在模板中使用自定义指令
<div v-demo>
    
</div>
```

**函数：**

- `inserted` ：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- `update`：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。

**参数：**

- `el`：指令所绑定的元素，可以用来直接操作 DOM 。
- `binding`：一个对象，包含以下属性：
  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-demo="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值
  - `expression`：字符串形式的指令表达式。例如 `v--demo="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-demo.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。



> 实现类似v-show的自定义指令

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
  <div id="app">
    <p v-demo="status">12</p>
    <button @click="status = !status">取反</button>
  </div>
</body>
<script>
const vm = new Vue({
  el: '#app',
  data: {
    status: true
  },
  directives: {
    demo: {
      inserted(el, binding) {
        console.log(el, binding)
        if (binding.value) {
          el.style.display = 'block'
        } else {
          el.style.display = 'none'
        }
      },
      update(el, binding){
        console.log(el, binding)
        if (binding.value) {
          el.style.display = 'block'
        } else {
          el.style.display = 'none'
        }
      }
    }
  }
})
</script>
</html>
```



## 三、(重点)Vue组件化开发



#### 3.1、什么是组件化？

> 面对复杂问题的处理方式，把问题拆解成很多个能处理的小问题，再将其放在整体中，会发现大的问题也会迎刃而解。
>
> 而组件化的思想也类似：
>
> 1. 如果我们实现一个页面结构和逻辑非常复杂的页面时，如果全部一起实现会变得非常复杂，而且也不利于后续的维护和迭代功能。
> 2. 但如果我们这时候把页面分成一个个小的功能块，每个功能块能完成属于自己这部分独立的功能，那么整个页面之后的维护和迭代也会变得非常容易。

* 组件化开发的优势：可维护性高    可复用性高

#### 3.2、Vue组件化思想

> 组件化是Vue重要的思想
>
> 1. 它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用。
> 2. 任何的应用都会被抽象成一颗组件树。

![1568877913978](F:\0001my\Notes\Vue.assets\1568877913978.png)

> 组件化思想的应用开发：
>
> 1. 有了组件化的思想，我们在之后的开发中就要充分的利用它。
> 2. 尽可能的将页面拆分成一个个小的、可复用的组件。
> 3. 这样让我们的代码更加方便组织和管理，并且扩展性也更强。



#### 3.3、全局组件

> 通过`Vue.component('组件名称', {})`，通过这个方法注册的都是全局组件，也就是他们再注册之后可以用在任何新创建的`Vue` 实例挂载的区域内。



```html
<body>
  <div id="app">
    <my-con></my-con>
    <div>
      <my-con></my-con>
    </div>
  </div>
  <my-con></my-con>
</body>
<script>
  Vue.component('my-con', {
    template: '<section><h3>组件标题</h3><p>组件内容</p></section>'
  })
  const vm = new Vue({
    el: '#app'
  })
</script>
```

> 上面案例中，在`<div id="app">...</div>` 外的组件 `my-con` 没有替换成组件真正的页面结构，是因为 `new Vue()` 挂载在 `id=app` 的节点上，不在这个节点上标签，不会受到Vue的影响。



#### 3.4、局部组件

> 通过 `Vue.component` 方式注册的组件，称之为全局组件。任何地方都可以使用。全局注册往往是不够理想的。比如，如果你使用一个像 webpack 这样的构建系统，全局注册所有的组件意味着即便你已经不再使用一个组件了，它仍然会被包含在你最终的构建结果中。这造成了用户下载的 JavaScript 的无谓的增加。



**注册局部组件**

```html
<body>
  <div id="app">
    <my-con></my-con>
    <div>
      <my-con></my-con>
    </div>
  </div>
  <div id="app1">
    <my-con1></my-con1>
  </div>
</body>
<template id="template1">
  <section>
    <h3>组件标题</h3>
    <p>组件内容</p>
  </section>
</template>
<template id="template2">
  <section>
    <h3>组件标题B</h3>
    <p>组件内容B</p>
  </section>
</template>
<script>
  var componentA = {
    template: '#template1'
  }

  var componentB = {
    template: '#template2'
  }
  const vm = new Vue({
    el: '#app',
    components: {
      'my-con': componentA
    }
  })
  const vm1 = new Vue({
    el: '#app1',
    components: {
      'my-con1': componentB
    }
  })
</script>
```



**父组件和子组件**

> 组件和组件之间存在层级关系，而其中一种最重要的关系就是父子组件关系。    



#### 3.5、组件可以访问Vue实例数据吗？

![1568884635108](F:\0001my\Notes\Vue.assets\1568884635108.png)

![1568884656744](F:\0001my\Notes\Vue.assets\1568884656744.png)



> 那组件如果要使用data定义自己属性保存数据要怎么做呢？
>
> 1. 组件对象也有一个data的属性（也有methods等属性，下面我们有用到）
> 2. 只是这个data属性必须是一个函数，而且函数返回一个对象 ，对象保存着数据



```html
<body>
  <div id="app">
    <my-con></my-con>
    <div>
      <my-con></my-con>
    </div>
  </div>
  <div id="app1">
    <my-con1></my-con1>
  </div>
</body>
<template id="template1">
  <section>
    <h3>{{title}}</h3>
    <p>组件内容</p>
  </section>
</template>
<template id="template2">
  <section>
    <h3>{{title}}B</h3>
    <p>组件内容B</p>
    <aa></aa>
  </section>
</template>
<script>
  var componentA = {
    template: '#template1',
    data() {
      return {
        title: 'zujianbiaoti'
      }
    }
  }

  var componentB = {
    template: '#template2',
    data() {
      return {
        title: 'zj'
      }
    },
    components: {
      'aa': {
        template: '<div>aa</div>'
      }
    }
  }
  const vm = new Vue({
    el: '#app',
    data: {title: '组件标题'},
    components: {
      'my-con': componentA
    }
  })
  const vm1 = new Vue({
    el: '#app1',
    components: {
      'my-con1': componentB
    }
  })
</script>
```

> 为什么data在组件中必须是一个函数呢？
>
> 原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响。



#### 3.6、父子组件间的通讯

##### 父级向子级传递

> 在组件中，使用选项props来声明需要从父级接收到的数据。
>
> props的值有两种方式：
>
> 1. 字符串数组，数组中的字符串就是传递时的名称。
> 2. 对象，对象可以设置传递时的类型（String，Number，Boolean，Array， Object，Date，Function，Symbol），也可以设置默认值等。



```html
<body>
  <div id="app1">
    <my-con1></my-con1>
  </div>
</body>

<template id="template2">
  <section>
    <h3>{{title}}B</h3>
    <p>组件内容B</p>
    <!-- my-con1组件内的aa组件 --> 
    <aa v-bind:parent-txt="childtxt"></aa>
  </section>
</template>
<script>
  var componentB = {
    template: '#template2',
    data() {
      return {
        title: 'zj',
        childtxt: 'child text'
      }
    },
    components: {
      'aa': {
        template: '<div>{{parentTxt}}</div>',
        props: ['parentTxt']
      }
    }
  }
  
  const vm1 = new Vue({
    el: '#app1',
    components: {
      'my-con1': componentB
    }
  })
</script>
```



##### 子级向父级传递

> 父组件向子组件传递数据，通过自定义事件

```html
<body>
  <div id="app1">
    <my-con1></my-con1>
  </div>
</body>

<template id="template2">
  <section>
    <h3>{{title}}B</h3>
    <p>组件内容B</p>
    <aa v-bind:parent-txt="childtxt" v-on:changetitle="changeTitle"></aa>
  </section>
</template>
<script>
  var componentB = {
    template: '#template2',
    data() {
      return {
        title: 'zj',
        childtxt: 'child text'
      }
    },
    components: {
      'aa': {
        template: '<div v-on:click="change">{{parentTxt}}</div>',
        props: ['parentTxt'],
        methods: {
          change() {
            this.$emit('changetitle', {
              a: 1
            })
          }
        }
      }
    },
    methods: {
      changeTitle(obj) {
        console.log(obj)
        this.title = obj.a
      }
    }
  }

  const vm1 = new Vue({
    el: '#app1',
    components: {
      'my-con1': componentB
    }
  })
</script>
```

> 案例分析：
>
> 1. 现在的需求是点击子组件`aa` 然后把父组件`my-con1`上的标题给改变；
> 2. 首先，在父组件的具体页面结构找到子组件`aa` ，在子组件`aa` 上使用`v-on:changetitle="changeTitle"` , `changetitle`是子组件的自定义事件名称，`changeTitle`是父组件`my-con1`里的`methods`属性定义的方法；
> 3. 其次，在子组件`aa`里为div绑定点击事件 `v-on:click="change"`, 在子组件`aa`里的methods定义change方法，change方法里使用`this.$emit('changetitle')`，使用$emit方法来触发绑定在子组件上的自定义事件，$emit第一个参数就是上一步定义的自定义事件`changetitle`,第二个参数就是传递到父组件的参数，可以不传。



**弹窗例子:**

![1568945029817](F:\0001my\Notes\Vue.assets\1568945029817.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }
    html,body, #app1{
      width: 100%;
      height: 100%;
    }
    
    .wrapper {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0, 0.3);
    }
    .content {
      width: 220px;
      height: 160px;
      background-color: #fff;
    }
    .title {
      height: 40px;
      line-height: 40px;
      text-align: center;
    }
    .msg {
      display: flex;
      align-items: center;
      justify-content: center;
      box-sizing: border-box;
      padding: 5px 10px;
      border-top: 1px solid #eee;
      border-bottom: 1px solid #eee;
      height: 80px;
      text-align: center;
      color: gray;
      font-size: 14px;
    }
    .bottom {
      display: flex;
      height: 40px;
      line-height: 40px;
      text-align: center;
    }
    .bottom div {
      flex: 1;
      color: green;
    }
    .bottom div:nth-of-type(1) {
      border-right: 1px solid #eee;
      color: red;
    }
  </style>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
  <div id="app1">
    <my-con v-show="showCon" :txt-obj="textObj" @btn-handle="handleBtnClick"></my-con>
  </div>
</body>

<template id="template1">
    <div class="wrapper">
        <div class="content">
          <p class="title">{{txtObj.title}}</p>
          <div class="msg">{{txtObj.msg}}</div>
          <div class="bottom">
            <div @click="cancel">{{txtObj.cancelTxt}}</div>
            <div @click="submit">{{txtObj.submitTxt}}</div>
          </div>
        </div>
      </div>
</template>
<script>
  var componentA = {
    template: '#template1',
    props: {
      txtObj: {
        type: Object,
        default: {}
      }
    },
    methods: {
      cancel() {
        // 自定义事件名称建议全小写
        this.$emit('btn-handle', 'cancel')
      },
      submit() {
        // 自定义事件名称建议全小写
        this.$emit('btn-handle', 'submit')
      },
    }
  }
  const vm1 = new Vue({
    el: '#app1',
    data: {
      textObj: {
        title: 'bug提示',
        msg: '亲，你还有53633个bug，是否要处理?',
        cancelTxt: '忽略，下班',
        submitTxt: '加班处理'
      },
      showCon: true
    },
    components: {
      myCon: componentA
    },
    methods: {
      handleBtnClick(type) {
        console.log(type)
        if (type === 'cancel') {
          this.showCon = false
        }
      }
    }
  })
</script>

</html>
```



#### 3.7、非父子组件通讯

> 实际工作中如果遇到跨组件或者非父组件间的传递数据，那该怎么办？第一个可以使用中央事件总线，也就是一个中介来完成。第二个就是使用 `Vuex` 提供的功能，这里先暂时不讨论这种方案，后续专门学习Vuex。



**案例：**点击按钮1，改变按钮2的背景颜色

![1568942668557](F:\0001my\Notes\Vue.assets\1568942668557.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
  <div id="app1">
    <my-con></my-con>
    <my-con1></my-con1>
  </div>
</body>

<template id="template1">
  <button @click="click1">按钮1</button>
</template>
<template id="template2">
  <button @click="click2" :style="{backgroundColor: fontColor}">按钮2</button>
</template>
<script>
  const bus = new Vue();
  const componentA = {
    template: '#template1',
    methods: {
      click1() {
        // 点击按钮1
        bus.$emit('xxx', this.getRandomColor());
      },
      getRandomColor() {
        return `rgb(${this.getRandomNum()},${this.getRandomNum()},${this.getRandomNum()})`
      },
      getRandomNum() {
        return Math.floor(Math.random() * 256)
      }
    }
  }
  const componentB = {
    template: '#template2',
    data() {
      return {
        fontColor: ''
      }
    },
    methods: {
      click2() {
        // 点击按钮2
      }
    },
    mounted() {
      bus.$on('xxx', (color) => {
        console.log(color)
        this.fontColor = color
      })
    }
  }
  const vm1 = new Vue({
    el: '#app1',
    components: {
      myCon: componentA,
      myCon1: componentB
    }
  })
</script>

</html>
```



# Vue第五天

## 学习目标

能够写出匿名插槽基本格式

能够写出具名插槽基本格式

能够完成插槽的导航案例

能够写出作用域插槽4种写法

能够写出匿名插槽作用域的写法

能够使用webpack对项目进行管理

能够使用vue create 命令创建项目

## 一、插槽

### 1. 为什么使用slot

> slot翻译为插槽，组件的插槽：
>
> 1. 组件的插槽也是为了让我们封装的组件更加具有扩展性。
> 2. 让使用者可以决定组件内容的一些内容到底展示什么。



**京东头部导航栏例子：**

![1568945650561](F:\0001my\Notes\Vue.assets\1568945650561.png)

![1568945654125](F:\0001my\Notes\Vue.assets\1568945654125.png)

![1568945657300](F:\0001my\Notes\Vue.assets\1568945657300.png)

![1568945660433](F:\0001my\Notes\Vue.assets\1568945660433.png)



### 2. 如何在组件中使用slot呢？

> 如何去封装这类的组件呢？
>
> 1. 它们也很多区别，但是也有很多共性。
> 2. 如果，我们每一个单独去封装一个组件，显然不合适：比如每个页面都返回，这部分内容我们就要重复去封装。
> 3. 但是，如果我们封装成一个，好像也不合理：有些左侧是菜单，有些是返回，有些中间是搜索，有些是文字，等等
>
> 如何封装合适呢？**抽取共性，保留不同**
>
> 1. 最好的封装方式就是将共性抽取到组件中，将不同暴露为插槽。
> 2. 一旦我们预留了插槽，就可以让使用者根据自己的需求，决定插槽中插入什么内容。
> 3. 是搜索框，还是文字，还是菜单。由调用者自己来决定。



### 3. slot的基本使用（匿名插槽）

> 了解了为什么用slot，我们再来谈谈如何使用slot？
>
> 1. 在子组件中，使用特殊的元素`<slot>`就可以为子组件开启一个插槽。
> 2. 该插槽插入什么内容取决于父组件如何使用。

![1568946418410](F:\0001my\Notes\Vue.assets\1568946418410.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    
  </style>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
  <div id="app1">
    <my-con></my-con>
    <my-con>
      <h2>我是h2标签的内容</h2>
      <p>我是p标签的内容</p>
    </my-con>
  </div>
</body>

<template id="template1">
    <div>
      <slot>我是插槽中的默认内容！！</slot>
    </div>
</template>
<script>
  var componentA = {
    template: '#template1',
  }
  const vm1 = new Vue({
    el: '#app1',
    data: {
      
    },
    components: {
      myCon: componentA
    }
  })
</script>

</html>
```



### 4. 具名插槽

> 当子组件的功能复杂时，子组件的插槽可能并非是一个。
>
> 1. 比如我们封装一个导航栏的子组件，可能就需要三个插槽，分别代表左边、中间、右边。
> 2. 那么，外面在给插槽插入内容时，如何区分插入的是哪一个呢？
> 3. 这个时候，我们就需要给插槽起一个名字
>
> 如何使用具名插槽呢？
>
> 1. 非常简单，只要给slot元素一个name属性即可
> 2. `<slot name='myslot'></slot>`



```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    
  </style>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
  <div id="app1">
    <my-con>
      <div slot="left">左侧</div>
      <div slot="right">右侧</div>
      <div slot="center">中间</div>
    </my-con>
  </div>
</body>

<template id="template1">
    <div>
      <slot name="left">我是左侧插槽中的默认内容！！</slot>
      <slot name="center">我是中间侧插槽中的默认内容！！</slot>
      <slot name="right">我是右侧插槽中的默认内容！！</slot>
    </div>
</template>
<script>
  var componentA = {
    template: '#template1',
  }
  const vm1 = new Vue({
    el: '#app1',
    data: {
      
    },
    components: {
      myCon: componentA
    }
  })
</script>

</html>
```

### 5、课堂练习

京东导航栏

![1568945654125](F:\0001my\Notes\Vue.assets\1568945654125.png)

![1568945657300](F:\0001my\Notes\Vue.assets\1568945657300.png)

![1568945660433](F:\0001my\Notes\Vue.assets\1568945660433.png)

### 6. 作用域插槽

> 默认情况下，父组件使用子组件，插槽数据默认是拿父组件的数据，而不是子组件拿数据。
>
> **作用域插槽**在父组件使用我们的子组件时， 插槽的数据从子组件中拿到数据，而不是从父组件拿到。

<img src="F:\0001my\Notes\Vue.assets\作用域插槽理解.png" />



### 7. 作用域插槽的多种写法

```jsx
// 1、基本写法
<one-comp>
  <button slot="btn" slot-scope="scope">按钮{{scope.msg}}</button>
</one-comp>

// 2、基本写法之模板写法
<one-comp>
  <template slot="btn" slot-scope="scope">
    <button>按钮{{scope.msg}}</button>
  </template>
</one-comp>

// 3、指令写法
<one-comp v-slot:btn="scope">
  <button>按钮{{scope.msg}}</button>
</one-comp>

// 4、指令写法之模板写法
<one-comp>
  <template v-slot:btn="scope">
    <button>按钮{{scope.msg}}</button>
  </template>
</one-comp>
```



## 二、Webpack（自动化 模块化 前端开发构建工具）

> 从本质上来说，webpack是一个**静态模块打包工具**。
>
> 要想让我们写好的模块化代码在各式各样的浏览器上能做到兼容，就必须借助于其他工具；而webpack的其中一个核心就是让我们可以进行模块化开发，并帮我们处理模块间的依赖关系。不仅仅是Javascript文件，我们的css、图片、json文件等在webpack中都可以当作模块来使用，这就是webpack的模块化概念。



### 1. gulp和webpack

> Gulp侧重于前端开发的 **整个过程** 的控制管理（像是流水线），我们可以通过给gulp配置不同的task（通过Gulp中的gulp.task()方法配置，比如启动server、sass/less预编译、文件的合并压缩等等）来让gulp实现不同的功能，从而构建整个前端开发流程。

**gulpfile.js**

```js
var gulp = require('gulp');
var uglify = require('gulp-uglify'); //压缩代码

// 压缩js
gulp.task('uglify',function(){
    var combined = combiner.obj([
        gulp.src('src/scripts/**/*.js'), //需要压缩的js文件路径
        sourcemaps.init(),
        uglify(), //压缩js
        sourcemaps.write('./'),
        gulp.dest('dest/scripts') //生成的js文件的目录
    ]);
});

//默认任务
gulp.task('default',['uglify']);
```

> Webpack有人也称之为 **模块打包机** ，由此也可以看出Webpack更侧重于模块打包，当然我们可以把开发中的所有资源（图片、js文件、css文件等）都可以看成模块，最初Webpack本身就是为前端JS代码打包而设计的，后来被扩展到其他资源的打包处理。Webpack是通过loader（加载器）和plugins（插件）对资源进行处理的。



### 2. webpack初体验

#### 1. 生成项目依赖文件

```js
// 执行后生成package.json文件
npm init -y
```



#### 2. 安装依赖（node环境在12.10.0下！）

nvm install 12.10.0

nvm use 12.10.0

npm i webpack@4.44.1 webpack-cli@3.3.12 -g

```js
// 最后的参数-D是安装到package.json的开发依赖devDependencies(开发环境)对象里，也可以用 --save-dev代替
npm install webpack@4.44.1 webpack-cli@3.3.12 -D

// 全局安装webpack和webpack-cli
npm i webpack@4.44.1 webpack-cli@3.3.12 -g

// -S是--save的简写，这样安装的话，会安装到dependencies(生产环境)对象里，也可以用 --save代替
npm install jquery -S
```

```js
// package.json
{
  "name": "webpack-demo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^4.40.2",
    "webpack-cli": "^3.3.9"
  },
  "dependencies": {
    "jquery": "^3.4.1"
  }
}

```

> devDependencies与dependencies的区别：
>
> 在发布npm包的时候，本身dependencies下的模块会作为依赖，一起被下载；devDependencies下面的模块就不会自动下载了；但对于项目而言，npm install 会自动下载devDependencies和dependencies下面的模块。

### 3.创建入口文件

`index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
</body>
<script src="./index.js"></script>
</html>
```



`index.js`

```js
import $ from 'jquery'
$('ul li:even').css({background: 'red'})
$('ul li:odd').css({background: 'green'})
```



在浏览器打开

![1568968799462](F:\0001my\Notes\Vue.assets\1568968799462.png)

> 为什么会这样？因为浏览器并不兼容import引入模块这种方式，所以我们要用到webpack打包

### 4. 通过webpack打包

```js
// 执行命令  output输出
webpack index.js -o dist/bundle.js
```

![1568968968751](F:\0001my\Notes\Vue.assets\1568968968751.png)

> 出现这个报错，这是因为命令行执行时候会找全局的webpack，但是我们并没有安装全局的webpack，所以我们可以安装全局webpack，或者是使用脚本方式启动



**package.json**

```js
{
  "name": "webpack-demo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "webpack index.js -o dist/bundle.js"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^4.40.2",
    "webpack-cli": "^3.3.9"
  },
  "dependencies": {
    "jquery": "^3.4.1"
  }
}

```



执行package.json文件中添加的start命令

```js
// 生成 dist文件夹和bundle.js文件
npm run start
```



然后再把index.html原来引入index.js的地方改成是通过webpack生成的bundle.js

```html
<!--index.html文件-->
<!--<script src="./index.js"></script>-->
<script src="./dist/bundle.js"></script>
```



最终浏览器看到的效果：

![1568969333664](F:\0001my\Notes\Vue.assets\1568969333664.png)

**优化**

> webpack index.js -o dist/bundle.js 这一句其实是可以写在一个配置文件里



**webpack.config.js：**

```js
const path = require('path');

module.exports = {
  entry: path.join(__dirname, './index.js'),	// dirname代表索引到文件所在目录
  output: {
    path: path.join(__dirname, './dist'),
    filename: 'bundle.js'
  }
}
```



**package.json：**

```json
"scripts": {
    "start": "webpack --config webpack.config.js"
  }
```



### 5.webpack-dev-server

> 这时候如果修改index.html的背景颜色red改成是gray，会发现浏览器刷新也没有效果，需要再跑一次`npm run start`命令才有用，这时候就需要webpack-dev-server(热重载)



**安装：**

```js
npm install webpack-dev-server@3.11.2 -D
```



**package.json：**

```json
"scripts": {
    "start": "webpack-dev-server --config webpack.config.js --open --port 3002 --hot"
  }
// --open 自动打开浏览器
// --port 服务监听的端口 3002
// --hot  自动更新

```

> 这里注意：
>
> 1、启动webpack-dev-server后， 你在目标文件夹中是看不到编译后的文件的，实时编译后的文件都保存到了内存当中。想看到bundle.js文件，可以运行localhost:3002/bundle.js查看
>
> 
>
> 2、既然bundle.js已经不在dist目录下，因此，如果没有其他的webpack配置项，上面的命令也可以简写为：
>
> ```js
> "scripts": {
> "start": "webpack-dev-server --open --port 3002 --hot"
> }
> ```

**index.html**

```html
<script src="./bundle.js"></script>
```



### 6. html-webpack-plugin

安装：`npm install html-webpack-plugin@4.5.1 -D`

**webpack.config.js**

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: path.join(__dirname, './index.js'),
  output: {
    path: path.join(__dirname, './dist'),
    filename: 'bundle.js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, './index.html'),
      filename: 'index.html'
    })
  ]
}
```



> 删掉index.html文件里面的bundle.js引用，因为html-webpack-plugin会自动把打包出来的bundle自动加到我们的index.html代码里



### 7. css-loader

创建一个index.css

**index.css**

```css
body {
    background: skyblue;
}
```



**index.js**

```js
import $ from 'jquery'
$('ul li:even').css({background: 'gray'})
$('ul li:odd').css({background: 'green'})

import './index.css'
```

![1568972642846](F:\0001my\Notes\Vue.assets\1568972642846.png)

> 为什么报错，因为webpack默认是不识别`.css`文件的，需要我们通过 `loader`  将 `.css` 文件进行解释成正确的模块。



**安装css-loader和style-loader**

```js
npm install css-loader@5.2.4 style-loader@2.0.0 -D 
//index.css -> bundle.js -> style-loader -> <style> index.html
// css-loader的作用是将index.css文件解析为webpack能识别的模块，然后打包进bundle.js里面，但是这样样式并未成功显示在浏览器中。
// style-loader的作用就是将打包到bundle.js中的样式绑定到浏览器上，以style标签的形式显示出来
```



**webpack.config.js**

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: path.join(__dirname, './index.js'),
  output: {
    path: path.join(__dirname, './dist'),
    filename: 'bundle.js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, './index.html'),
      filename: 'index.html'
    })
  ],
  module: {
    rules: [{
      test: /\.css$/,
      use: ['style-loader', 'css-loader']	// 注意：这里的数组是反向读取的（即从右往左）
    }]
  }
}
```



> 补充：引入的文件是less
>
> 安装：npm install less-loader@7.2.1 less@4.1.0 -D
>
> 规则： 
>
> {
>
> ​	test: /\.less$/,
>
> ​	use: ['style-loader', 'css-loader', 'less-loader']
>
> }



### 8. ES6 转 ES5 

> 安装依赖包

```js
npm install babel-core babel-loader@7.1.5 babel-plugin-transform-runtime@6.23.0 babel-preset-env@1.7.0 babel-preset-stage-0@6.24.1 -D
```

```js
const fn = () => {
  console.log(123)
}
```



> 配置loader 

```js
{test:/\.js/,use:['babel-loader'],exclude:/node_modules/} 
```

exclude表示排除掉 node_modules下载的依赖项。这样可以加速网站开发，而且我们也只需要对我们的项目src 

源文件进行编译即可。

 

> 新增.babelrc文件 

```json
{ 
    "presets":["env","stage-0"], 
    "plugins":["transform-runtime"] 
} 
```



新增并在index.js中引入main.js，然后使用es6语法 

```js
const fn = () => {
  console.log(123)
}

fn()
```



执行命令编译 

```js
npm run start 
```



编译后的结果

```js
var fn = function fn() {\n    console.log(123);\n}
```

至此关于webpack的基本配置已经到这里。 



### 9. html热更新

在安装过html-webpack-plugin之后，安装：

```js
npm install --save-dev raw-loader@4.0.2
```

在webpack.config.js中配置raw-loader:

```js
module.exports = {
  ......
  module: {
    rules: [
      {
         test: /\.(htm|html)$/,
         use: [
           'raw-loader'
         ]
      },
      ......
    ]
  }
}
```

在 `index.js` 中引入html：

```js
import './index.html'
```

## 三、Vue CLI使用准备

### Node版本

> Vue CLI 需要Node.js 8.9 或者更高版本（推荐使用 <font color="red">12.11.0</font>）。你可以使用`nvm` 或 `nvm-window`来管理电脑上面的Node版本。



**安装Vue CLI脚手架的包：**

```js
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

安装之后，你就可以在命令行中访问 `vue` 命令。你可以通过简单运行 `vue`，看看是否展示出了一份所有可用命令的帮助信息，来验证它是否安装成功。

你还可以用这个命令来检查其版本是否正确 (4.x)：

```bash
vue --version
vue -V
```



如果安装比较慢，可以把下载源切换成淘宝的源：

npm  对应的淘宝下载源设置：

```shell
//切换taobao镜像源
npm config set registry https://registry.npm.taobao.org/
// 查看下载源
npm config get registry
```

yarn  对应的淘宝下载源设置：

```shell
//切换taobao镜像源
yarn config set registry https://registry.npm.taobao.org/

// 查看下载源
yarn config get registry
```



## 四、创建项目

### 初始化项目

**vue create**

运行以下命令来创建一个新项目：

```js
vue create hello-world
```



你会被提示选取一个 preset。你可以选默认的包含了基本的 Babel + ESLint 设置的 preset，也可以选“手动选
择特性”来选取需要的特性。

![](F:\0001my\Notes\Vue.assets\cli-new-project.png)

这个默认的设置非常适合快速创建一个新项目的原型，而手动设置则提供了更多的选项，它们是面向生产的项目更加需要的。

![CLI é¢è§](F:\0001my\Notes\Vue.assets\cli-select-features.png)

对于每一项的功能，此处做个简单描述：

- TypeScript 													支持使用 TypeScript 书写源码。
- Progressive Web App (PWA) Support     PWA支持
- Router                                                          路由
  Vuex													状态管理
   CSS Pre-processors					 支持 CSS 预处理器。
   Linter / Formatter					 支持代码风格检查和格式化。
   Unit Testing										 支持单元测试。
   E2E Testing									 支持 E2E 测试。

如果你决定手动选择特性，在操作提示的最后你可以选择将已选项保存为一个将来可复用的 preset



> ~/.vuerc
>
> 被保存的 preset 将会存在用户的 home 目录下一个名为 `.vuerc` 的 JSON 文件里。如果你想要修改被保存的 preset / 选项，可以编辑这个文件。
>
> 在项目创建的过程中，你也会被提示选择喜欢的包管理器或使用[淘宝 npm 镜像源](https://npm.taobao.org/)以更快地安装依赖。这些选择也将会存入 `~/.vuerc`。



### 项目结构

**项目目录**

![1569235847530](F:\0001my\Notes\Vue.assets\1569235847530.png)



```js
node_modules
public // 静态资源文件
    |-favicon.ico
    |-index.html
src // 项目源代码，书写代码的地方
    |-assets
    |-App.vue
    |-main.js
.browserslistrc    // 浏览器相关支持情况
.eslintrc.js       // 代码相关支持情况
.gitignore         // Git忽略文件
babel.config.js    // babel配置ES语法 转换
package-lock.json  // npm安装依赖库的具体信息
package.json       // npm依赖库版本信息
postcss.config.js  // css相关转换
README.md          // 项目说明
vue.config.js      // Vue及webpack配置项
```



### vue.config.js

`vue.config.js` 是一个可选的配置文件，如果项目的 (和 `package.json` 同级的) 根目录中存在这个文件，那么它会被 `@vue/cli-service` 自动加载。你也可以使用 `package.json` 中的 `vue` 字段，但是注意这种写法需要你严格遵照 JSON 的格式来写。

这个文件应该导出一个包含了选项的对象：

```js
// vue.config.js
module.exports = {
  // 选项...(例如：)
  lintOnSave: false	// 关闭eslint
}
```



# 基于Vue脚手架之上的开发(第五天)

## 今日学习目标

能够在Chrome浏览器中安装Vue开发者工具Devtools

能够写出v-model语法糖

能够写出Vue中常用的修饰符

能够写出watch属性的基本语法格式

能够写出watch属性深度监听的语法格式

能够说出watch和computed的区别

能够说出Mixins的作用

能够写出KeepAlive的使用格式并完成课上组件缓存的案例

## 一、Devtools与Vscode开发配置（了解）

Vue-Devtools是vue在做项目开发时常用的浏览器插件。

### 1、安装方式

- 升级浏览器至最新版

<img src="F:\0001my\Notes\Vue.assets\01.png" style="border: 2px solid" />

- 点击浏览器右上角的 `三个点` ，在 `更多工具` 中，选择 `扩展程序`
- 打开 `扩展程序` 的 `开发者模式`

![image-20200718142634459](F:\0001my\Notes\Vue.assets\02.png)

- 将 `Vue.js Devtools_5.3.3.crx` 这个插件直接拽入当前界面，即可完成安装

### 2、打开控制台测试devtools

随意写一个点击事件，并查看点击效果

<img src="F:\0001my\Notes\Vue.assets\03.gif" style="zoom:100%;" />

像一些使用Vue完成的项目，右上角的Vue图标会亮起：

1） [https://www.bilibili.com](https://www.bilibili.com/) （bilibili） 
2） [http://m.sohu.com](http://m.sohu.com/) （手机搜狐网） 
3） http://element.eleme.io/#/en-US  

### 3、VsCode用户片段提供

请在VScode中设置如下代码片段，以用于后面每一个案例的创建

```json
{
	"demo": {
	  "prefix": "vue",
	  "body": [
		"<template>",
		"\t<div>",
		"\t\t$0",
		"\t</div>",
		"</template>",
		"",
		"<script>",
		"export default {",
		"\tdata () {",
		"\t\treturn {\n",
		" ",
		"\t\t}",
		"\t}",
		"}",
		"</script>",
		" ",
		"<style lang = \"less\" scoped>",
		"\t",
		"</style>"
	  ],
	  "description": "自定义的一个vue代码段"
	}
  }
```

### 4、“@/”路径提示配置

安装 Path Intellisense插件

打开设置 - 首选项 - 搜索 `Path Intellisense` - 打开 `settings.json` ，添加：

```json
"path-intellisense.mappings": {
     "@": "${workspaceRoot}/src"
 }
```

在项目 `package.json` 所在同级目录下创建文件 `jsconfig.json`：

```json
{
    "compilerOptions": {
        "target": "ES6",
        "module": "commonjs",
        "allowSyntheticDefaultImports": true,
        "baseUrl": "./",
        "paths": {
          "@/*": ["src/*"]
        }
    },
    "exclude": [
        "node_modules"
    ]
}
```

最后**重启打开**即可

## 二、v-model语法糖(了解)

v-model作为语法糖，相当于：v-on搭配v-bind，如下：

```vue
<input v-model="val" />

// 相当于

<input v-on:input="val = $event.target.value" v-bind:value="val" />
```

## 三、常用修饰符

vue中常用的修饰符分三种，分别是事件修饰符、按键修饰符和表单修饰符。

### 1、事件修饰符

- `.stop` 阻止事件冒泡(*)
- `.prevent` 阻止默认事件(*)
- `.prevent.stop` 阻止默认事件的同时阻止冒泡
- `.once` 阻止事件重复触发（once与stop不能一起使用，否则再次触发事件，依然会冒泡）(*)

```vue
<template>
    <div>
        <div class="big" @click="cb">
            <div class="small" @click="cs">
                <a href="#" @click.stop.prevent="ca">a标签</a>
            </div>
        </div>
        <button @click.once="cc">点我</button>
    </div>
</template>

<script>
export default {
    
    methods:{
        cb(){
            console.log("点击大的");
        },
        cs(){
            console.log("点击小的");
        },
        ca(){
            console.log("点击a标签");
        },
        cc(){
            console.log("点击按钮");
        }
    }

}
</script>

<style>
.big{
    width: 300px;
    height: 300px;
    background-color: pink;
}
.small{
    width: 200px;
    height: 200px;
    background-color: skyblue;
}
</style>
```



### 2、按键修饰符

在监听键盘事件时，我们经常需要检查详细的按键。Vue 允许为 `v-on` 在监听键盘事件时添加按键修饰符：

```vue
<input v-on:keyup.enter="submit">
<input v-on:keyup.13="submit">
```

为了在必要的情况下支持旧浏览器，Vue 提供了绝大多数常用的按键码的别名：

- `.enter` (*)
- `.tab`
- `.delete` (捕获“删除”和“退格”键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

### 3、表单修饰符

我们还有其他的修饰符，比如表单上常用的 `trim` 和 `number` ：

- 想去除用户输入的前后空格：

```vue
<input v-model.trim="val" type="text">

data(){
  return {
  	val: "你好，世界"
  }
}
```

- 希望在input的change之后再更新输入框的值

```vue
<input v-model.lazy="val" type="text">
```

> .trim与.lazy可以合并使用：
>
> <input v-model.lazy.trim="val" type="text" />
>
> 二者没有先后顺序

```vue
<template>
<!-- 表单修饰符 -->
    <div>
        <!-- 加了.trim之后，获取到的是去除前后空格的结果 -->
        <input type="text" v-model.trim="iptVal">
        <button @click="handleClcik">按钮</button>
        <br>
        <!-- 加了.number之后, 获取到的用户输入的信息就是number类型了-->
        <input type="number" v-model.number="numVal">
        <button @click="handleClcik2">按钮</button><br><br>
        <!-- 加了.lazy, 用户每一次触发就不会马上更新这个值，等到用户按回车的时候，才更新这个值 -->
        <input type="text" v-model.lazy="ipt2Val">
        <p>{{ipt2Val}}</p>
    </div>
</template>

<script>
export default {
    data () {
        return {
            iptVal:"",
            numVal:"",
            ipt2Val:""
 
        }
    },
    methods:{
        handleClcik(){
            console.log(this.iptVal);
        },
        handleClcik2(){
            console.log(this.numVal, typeof this.numVal);
        }
    }
}
</script>
```



### 4、系统修饰键

可以用如下修饰符来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器。

- `.ctrl` （实测结果：由于mac系统 `ctrl+鼠标左键 = 右键` 这个功能，所以mac上无法实现）
- `.alt`
- `.shift`
- `.meta` （meta在win上代表⊞键，在mac上代表⌘键）

```vue
<!-- Alt + C -->
<input v-on:keyup.alt.67="doSomething">

<!-- Ctrl + Click -->
<div v-on:click.ctrl="doSomething">Do something</div>
```

#### 注意

![image-20200716202014266](F:\0001my\Notes\Vue.assets\04.png)

## 四、Watch

watch的作用可以监控一个值的变换，并调用因为变化需要执行的方法。可以通过watch动态改变关联的状态。

简单点说，就是实时监听某个数据的变化。

### 1、普通监听

```vue
<template>
  <div class="home">
    <input type="text" v-model="msg">
    <h3>{{msg}}</h3>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data(){
    return {
      msg: "你好，世界"
    }
  },
  watch: {
    msg(val, oldVal){
      console.log(val, oldVal)
    }
  }
}
</script>
```

### 2、立即监听

如果我们需要在最初绑定值的时候也执行函数，则就需要用到immediate属性。

```vue
<template>
  <div class="home">
    <input type="text" v-model="num">
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      num: 20
    };
  },
  watch: {
    num: {
      handler(val, oldVal) {
        console.log(val, oldVal);
      },
      // 组件注入页面时就立即监听
      immediate: true
    }
  }
};
</script>
```

> immediate需要搭配handler一起使用，其在最初绑定时，调用的函数也就是这个handler函数。

### 3、深度监听

当需要监听一个对象的改变时，普通的watch方法无法监听到对象内部属性的改变，只有data中的数据才能够监听到变化，此时就需要deep属性对对象进行深度监听。

```vue
<template>
  <div class="home">
    <h3>{{obj.age}}</h3>
    <button @click="btnClick">按钮</button>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data(){
    return {
      obj: {
        name: "Lucy",
        age: 13
      }
    }
  },
  methods: {
    btnClick(){
      this.obj.age = 33;
    }
  },
  watch: {
    obj: {
      handler(val, oldVal){
        console.log(val.age, oldVal.age)		//  33   33
      },
      deep: true
    }
  }
}
</script>
```

> 注意：
>
> 1、如果监听的数据是一个对象，那么 `immediate: true `失效；
>
> 2、一般使用于对引用类型的监听，深度监听，如监听一个Object，只要Object里面的任何一个字段发生变化都会被监听，但是比较消耗性能，根据需求使用，能不用则不用。
>
> 3、因为上面代码obj是引用数据类型，val, oldVal指向一致，导致看到的结果一样。

### 4、deep优化

我们可以通过点语法获取对象中的属性，然后转为字符串，即是对深度监听的优化

```vue
<template>
  <div class="home">
    <h3>{{obj.age}}</h3>
    <button @click="btnClick">按钮</button>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      obj: {
        name: "Lucy",
        age: 13
      }
    };
  },
  methods: {
    btnClick() {
      this.obj.age = 33;
    }
  },
  watch: {
    // 通过点语法获取对象中的属性，然后转为字符串，即是对深度监听的优化
    "obj.age": {
      handler(val, oldVal) {
        console.log(val, oldVal);
      },
      deep: true,
      immediate: true,		// 此时监听的数据不是一个对象，可以使用immediate
    }
  }
};
</script>
```

### 5、Watch与Computed的区别

- watch中的函数是不需要调用的，computed内部的函数调用的时候不需要加()
- watch(属性监听)，监听的是属性的变化，而computed(计算属性)，是通过计算而得来的数据
- watch需要在数据变化时执行异步或开销较大的操作时使用，而对于任何复杂逻辑或一个数据属性，在它所依赖的属性发生变化时，也要发生变化，这种情况下，我们最好使用计算属性computed。 
- computed 属性的结果会被缓存，且computed中的函数必须用return返回最终的结果
- watch 一个对象，键是需要观察的表达式，值是对应回调函数。主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑操作；

### 6、Watch与Computed的使用场景

- computed 　　　
  - 当一个结果受多个属性影响的时候就需要用到computed
  - 最典型的例子： 购物车商品结算的时候

- watch
  - 当一个数据的变化需要有额外操作的时候就需要用watch
  - 搜索数据

- 总结：
  - 一个值的结果受其他值的影响，用computed
  - 一个值的变化将时刻影响其他值，用watch

## 五、Mixins混入

mixins就是定义一部分公共的方法或者计算属性,然后混入到各个组件中使用,方便管理与统一修改。同一个生命周期，混入对象会比组件的先执行。

### 1、导出mixins

在src下创建 `mixins/index.js`，写入：

```js
export const MixinsFn = {
    created() { 
        console.log("这是mixins触发的created")
    }
}
```

### 2、引用mixins

```vue
<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>
<script>
import { MixinsFn } from '@/mixins/index.js'
export default {
  created(){
    console.log("这是about触发的created")
  },
  mixins: [MixinsFn]
}
</script>
```

我们会发现，`mixins中的created` 比 `about中的created` 优先执行。

## 六、ref与$refs

vue中获取页面里的某个元素（标签或组件），可以给它绑定ref属性，有点类似于给它添加id名。

### 1、简单使用

```vue
<template>
 <div class="">
     <h3 ref="title">{{msg}}</h3>
     <button @click="btnclick">按钮</button>
 </div>
</template>
 
<script>
export default {
  data() {
    return {
      msg: "你好"
    };
  },
  methods: {
    btnclick() {
      console.log(this.$refs.title);		// 得到h3标签
    }
  }
};
</script>
 
<style lang = "less" scoped>
</style>
```

### 2、子组件中的数据获取及方法调用

子组件：

```vue
<template>
 <div class="">
     <h4>{{num}}</h4>
 </div>
</template>
 
<script>
export default {
  data() {
    return {
      num: 100
    };
  },
  methods: {
      subFn(){
          console.log('子组件中的方法')
      }
  }
};
</script>
 
<style lang = "less" scoped>
</style>
```

父组件：

```vue
<template>
 <div class="">
     <Sub ref="sub" />
     <button @click="btnclick">按钮</button>
 </div>
</template>
 
<script>
import Sub from '../components/Sub'
export default {
  methods: {
    btnclick() {
      console.log(this.$refs.sub.num);	// 100
      this.$refs.sub.subFn();						// '子组件中的方法'
    }
  },
  components: {
      Sub
  }
};
</script>
 
<style lang = "less" scoped>
</style>
```

## 七、（重点）KeepAlive

`<keep-alive>`是Vue的内置组件，能在组件切换过程中将状态保留在内存中，防止重复渲染DOM。

KeepAlive用于处理组件缓存。有什么用呢？想象一个业务场景：

> 在Login页面填写完手机号，发现未注册，需要跳去Register页面完成注册，再返回Login页面填写密码，进行登录，此时如果在Login页面没有保存好手机号，那么跳回来时，用户又得重新输入手机号。为了解决这样的需求，我们需要借助keep-alive。

这里，我们新创建两个页面， `You.vue` 和 `Me.vue` ，并且都实现累加功能。

### 1、修改App.vue

```vue
// 将原本的：
<router-view/>

// 修改为：
<keep-alive>
  <router-view/>
</keep-alive>
```

这样，我们实现了整个项目中每个页面的缓存，显然我们不想这么做，我们只想针对某些页面，这时，我们修改一下：

```vue
<keep-alive>
	<router-view v-if="$route.meta.keepAlive" />
</keep-alive>
<router-view v-if="!$route.meta.keepAlive" />
```

> 注意：
>
> `<keep-alive>` 是用在其一个直属的子组件被开关的情形。如果你在其中有 `v-for` 则不会工作。

那这里的 `$route.meta.keepAlive` 存在于哪里呢？

### 2、Router中的meta

这是写在路由文件中的字段，我们去 `router/index.js` 中，将我们要缓存的 `Me.vue` 页面加上meta：

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'

Vue.use(VueRouter)

const routes = [
  	...,
    {
      path: '/me',
      name: 'Me',
      component: () => import('../views/Me.vue'),
      meta: {
        keepAlive: true
      }
    },
    {
      path: '/you',
      name: 'You',
      component: () => import('../views/You.vue')
    }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router
```

## 八、今日作业

作业在今日的作业文件夹中，注意：

1、所有同学必须完成作业题1和作业题2.

2、拓展题1作为以上完成作业后的奖励！继续提升学习！

3、拓展题2有点难度，请量力而行！

4、拓展题目为非必须完成。

## 九、预习知识点

今日预习资料文件夹中——Vuex笔记





