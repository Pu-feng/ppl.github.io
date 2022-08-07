# NodeJS课程讲义-NodeJSAPI

## Node环境使用

### repl运行环境(知道就行)

node给我们提供了一个"REPL"运行环境 

【r = read】  读取用户输入的文字

【e = eval】  执行用户输入了内容

【p = print】 输出执行结果

【l = loop】  循环执行上面的流程

我们只需要在cmd或者运行里面输入 "node",就可以进入repl运行环境，可以在这个环境下写代码。

![image-20210315151105489](F:\0001my\Notes\NodeJS.assets\image-20210315151105489.png)

### 在js文件中写代码

毫无疑问，repl的方式肯定不方便，不是我们最常用的方式，所以我们正常都是在编辑器里把代码写好，然后再执行。

我们直接在vscode里面写一个文件

![image-20210315151944850](F:\0001my\Notes\NodeJS.assets\image-20210315151944850.png)

执行这个文件的方式有很多，但是归根到底都是一样的，就是要通过命令窗口(cmd/powershell)调用node环境执行它。

#### 方式1 - cmd执行

1,打开文件所在目录

![image-20210315152118788](F:\0001my\Notes\NodeJS.assets\image-20210315152118788.png)

2，在地址栏上点击并输入cmd回车

![image-20210315152154149](F:\0001my\Notes\NodeJS.assets\image-20210315152154149.png)

3,在弹出来的cmd窗口里面输入 <span style="color:yellowgreen;">node 指定文件</span>

![image-20210315152450272](F:\0001my\Notes\NodeJS.assets\image-20210315152450272.png)

4,回车之后就能看到结果

![image-20210315152604438](F:\0001my\Notes\NodeJS.assets\image-20210315152604438.png)

#### 方式2 - 在编辑器的终端执行

在vscode里面通过 “终端” -> "新终端"  ，或者使用快捷键 `ctrl + ~` 打开vscode的命令行窗口

![image-20210315152841445](F:\0001my\Notes\NodeJS.assets\image-20210315152841445.png)

![image-20210315152907165](F:\0001my\Notes\NodeJS.assets\image-20210315152907165.png)

在终端里面也是使用node命令执行文件

![image-20210315153134879](F:\0001my\Notes\NodeJS.assets\image-20210315153134879.png)

> 小结：
>
> 1. 重点掌握使用node命令执行js文件
> 2. 无论是在cmd还是在vscode的终端里面执行，本质都就在使用命令调用node环境进行解析执行

## NodeAPI学习

### NodeJS和浏览器的js的区别

NodeJS是一个和浏览器完全不同的环境，NodeJS当初设计出来，目的就是为了写服务器的代码的，所以里面有很多功能浏览器是不具备的，同样，服务器环境下不需要的功能，Node环境下也不会有。

![image-20210315154458072](F:\0001my\Notes\NodeJS.assets\image-20210315154458072.png)

* NodeJS组成
  * ECMAScript         语法，功能
  * Node标准库          Node官方自带的功能API
  * Node第三方库        开发者在开发过程中封装的常用代码

* 浏览器JS组成
  * ECMAScript         语法，功能
  * DOM                操作页面元素的API
  * BOM                操作浏览器功能的API

> 在服务器里面是没有页面的，没有浏览器功能的，所以NodeJS里面没有必要有DOM和BOM，这点要记住。

### NodeJS标准库

在NodeJS中提供了很多的标准库，也就是自带的功能API，我们可以先大概学习一部分和后面课程相关的。

#### fs模块

fs模块，是Node标准库中用于操作计算机上的文件的模块，提供了很多的方法，比如现在我们想从电脑上读取一个HTML文件，把内容返回给浏览器，就需要用到这个模块

##### fs读取模块

![image-20210315155408780](F:\0001my\Notes\NodeJS.assets\image-20210315155408780.png)

我们打算读取一下index.html

![image-20210315155523903](F:\0001my\Notes\NodeJS.assets\image-20210315155523903.png)

用法如下：

```js
// 1. 引入fs模块 ， node里面几乎所有的标准库都要先引入才能使用
const fs = require('fs')
// 2. 调用readFile方法
fs.readFile('./page/index.html',(error,data)=>{
  console.log(data)
})
```

如果我们没有指定options里面的编码，那么默认读取出来的是 `<Buffer>` ，是一些二进制数据，我们需要指定对应的编码，才能看到结果

```js
// 1. 引入fs模块 ， node里面几乎所有的标准库都要先引入才能使用
const fs = require('fs')
// 2. 调用readFile方法 , 并指定编码
fs.readFile('./page/index.html','utf-8',(error,data)=>{
  console.log(data)
})
```

> 注：读取文件是一个异步的过程，因为我们不知道要读取的文件有多大，越大越耗时，所以我们不等待这个动作完成，而是采用异步的方式，给一个回调函数，当它读取完成的时候再执行逻辑。

### node命令注意点

我们在上一步学习读取文件的时候，使用的是相对路径，但是相对路径在node环境里面是存在隐患的。因为在nodejs里面，所有的相对路径的开始位置是你的node命令执行的位置。如下：js文件在一个node文件夹里面

![image-20210315160926418](F:\0001my\Notes\NodeJS.assets\image-20210315160926418.png)

如果你此时在code目录下运行fs.js,就没有问题

![image-20210315161058900](F:\0001my\Notes\NodeJS.assets\image-20210315161058900.png)

因为相对路径的开始目录是从node命令所有的目录开始的，也就是code文件夹，通过 './page/index.html'是能找到指定文件的，所以执行正常

但是如果我们切换到了node目录下再执行，就会有问题。

![image-20210315161352848](F:\0001my\Notes\NodeJS.assets\image-20210315161352848.png)

因为我们的node命令在node文件夹下执行，fs.js里面的路径'./page/index.html'以node文件平开始查找，肯定找不到html文件，所以报错了。

### path模块

所以既然在NodeJS里面使用相对路径有一定的风险，有没有好的方式可以解决呢？答案是肯定的。

我们依然在node目录下写我们的js代码，使用下面的两个方案来解决。

<img src="F:\0001my\Notes\NodeJS.assets\image-20210315162929485.png" alt="image-20210315162929485" style="zoom:50%;" />

#### path.join

第一种方案可以使用path.join方法配合__dirname常量来实现

```js
const path = require('path')
const dir = path.join(__dirname,'../page/index.html')
```

其中join的作用是把多个路径片段拼接到一起，并解决不同平台的字符兼容问题。__dirname是得到当前js文件所在目录的API

#### path.resolve

而第二种方案就简单得多，我们只需要给一个相对路径，就能得到一个绝对路径

```js
const path = require('path')
const dir = path.resolve('../page/index.html')
```

此时我们再使用fs进行读取就不会出现路径错误了。

> 小结：
>
> 1. NodeJS里面提供了非常多的标准库(内置模块)，要学会从文档中学习
> 2. 相对路径是基于node命令执行的目录的，所以大家在执行node代码的时候要注意
> 3. 建议在用到路径的地方使用path来得到绝对路径再使用

## NodeJS服务器开发

### 服务器概念

**服务器**是一(多)台电脑，在这台电脑上面安装了一个**服务器软件**，让这台电脑可以为我们提供特定的服务。<span style="color:yellowgreen;">对于我们而言，服务器主要提供静态资源和动态数据</span>。只不过这台电脑一般放在运营商的机房里面，我们看不见。

![image-20210315171313335](F:\0001my\Notes\NodeJS.assets\image-20210315171313335.png)

> 注：通常我们不会把服务器电脑和服务器软件分开来说，一般说到服务器就是指两者的结合

当我们在请求服务器的时候，会发生下面的过程：

![image-20210315174139590](F:\0001my\Notes\NodeJS.assets\image-20210315174139590.png)

**IP** ：一台计算机在一个网络中的唯一地址

**端口**：一个软件在一台计算机上的唯一编号

> 小结：
>
> 1. 服务器可以是指服务器电脑，也可以是指服务器软件
> 2. web服务器主要提供静态资源和动态数据
> 3. 请求通过ip识别服务器主机，通过端口识别服务器软件
> 4. 服务器软件通过url识别请求的目的
> 5. 上述内容都是由http协议规定的

### 服务器代码

由上述的内容我们知道，服务器要能让浏览器访问，至少要告诉别人两个重要的东西：ip+端口，所以我们如果要使用nodejs写一个服务器，肯定要有这些要素。

#### NodeJS实现一个服务器的代码

```js
// 1. 引入http协议，node里面已经帮我们封装好了关于这部分的API
const http = require('http')
// 2. 创建一个服务器对象
const server = http.createServer()
// 3. 绑定ip和端口
server.listen(8080,'127.0.0.1')
// 4. 服务器对象监听浏览器的请求
server.on('request',(request,response)=>{
	// 5. 响应数据回浏览器
  response.end('<h1>hello world!!!</h1>')
})
```

通过上面的5行代码，我们就使用nodejs编写了一个服务器软件，只要开启起来，就能让浏览器请求，并得到返回的数据了。

#### 中文乱码问题

同学们在自己练习的过程中，可能会写一些中文返回给浏览器，于是发现了中文会在浏览器中乱码。我们可以定位到肯定是编码格式不对的问题，所以我们需要通过一些特殊的方式告诉浏览器编码格式。http协议中规定，我们可以在响应头中返回数据解析方式和数据的编码格式。

```js
response.setHeader('Content-Type','text/html;charset=utf-8')
response.end('<h1>你好，世界！！！</h1>')
```

#### 返回静态数据

目前为止，我们已经可以实现服务器和浏览器的通信了，但是我们发现，返回的内存太过于简单了，也不像是我们平时开发的静态资源，所以我们需要用到fs模块来把我们写好的静态资源读取出来，并返回给浏览器。

```js
const http = require('http')
// 引入fs模块
const fs = require('fs')
const server = http.createServer()
server.listen(8080,'127.0.0.1')
server.on('request',(request,response)=>{
  // 读取出来指定的文件
  fs.readFile('./views/index.html',(err,data)=>{
   // 调用 响应回浏览器的方法把页面内容返回浏览器 
    response.end(data)
  })
})
```

#### 根据请求url返回不同的静态资源

 如果要根据不同的url来返回不同的静态资源，那么就要在最开始的时候约定好，浏览器发什么url回服务器，服务器就返回对应的数据

我们暂时约定： 如果请求 <span style="color:hotpink;">'/views/index.html'</span> 我们就从服务器返回 index页面的内容

如果请求 <span style="color:hotpink;">'/css/index.css'</span> 我们就从服务器返回 index.css 的内容

如果请求 <span style="color:hotpink;">'/views/list.html'</span>  我们就从服务器返回 list页面的内容

首先我们需要在服务器端把请求的url获取到：

```js
server.on('request',(request,response)=>{
  // 得到浏览器请求的url
  console.log(request.url)
})
```

所以我们只需要在request事件里面判断请求的url，并读取不同的资源返回即可

```js
server.on('request',(request,response)=>{
  // 返回index.html
	if(request.url === '/views/index.html'){
    // fs读取index.html , response.end() 返回
  }
  else if (request.url === '/views/list.html'){
    // fs读取list.html , response.end() 返回     
  }
  else if (request.url === '/css/index.css'){
    // fs读取index.css , response.end() 返回           
  }
})
```

#### 统一返回静态资源

到此为止我们发现了一定的规则，我们fs读取的路径，事实上和我们约定的请求url是一样的，所以我们可以直接修改为

```js
server.on('request',(request,response)=>{
  fs.readFile(__dirname+request.url,(err,data)=>{
    response.end(data)
  })
})
```

但是这样有一个问题，我们能访问到这个网站下的所有资源，这样不安全，所以我们约定，只有几个固定的，用来放静态资源的文件夹才能被访问

```js
server.on('request',(request,response)=>{
  // 请求的url要以 /views 开关，才是静态请求
      if(/^\/views/.test(request.url)){
  	fs.readFile(__dirname+request.url,(err,data)=>{
      response.end(data)
    })   
  }
})
```

### 处理动态数据

相比于静态资源来说，动态数据的请求会有很多，而且每个的功能和处理的逻辑都不尽相同，所以每个处理动态数据的接口就只能单独写了。原理也是和之前一样，通过判断不同的URL来判断浏览器要服务器做什么。我们管这种处理动态请求的方式称呼为 ： **接口**

约定好：如果浏览器请求的是 <span style="color:yellowgreen;">'/getArticles'</span> , 就是要获取文章的列表，我们就返回一个数组给浏览器。那么我们的代码要这么写：

```js
server.on('request',(request,response)=>{
  // 判断url
  if(reqeust.url === '/getArticles'){
    // 返回一个数组给浏览器 - 但是不能直接返回一个数组，要先把数组转换为字符串，否则会报错
    let json = JSON.stringify([
      {id:1,title:'标题1',content:'内容1'},
      {id:2,title:'标题2',content:'内容2'},
      {id:3,title:'标题3',content:'内容3'}
    ])
    response.send(json)
  }
})
```

此时我们只要在页面中写ajax请求，请求这个接口，就能得到一个数组。

```html
<ul id="parent">
  
</ul>
<script>
  $.ajax({
    url:'http://127.0.0.1:8080/getArticles',
    success(res){
      // 服务器给我们的是一个字符串，先把字符串转换为数组
      let arr = JSON.parse(res)
      let str = ''
      arr.forEach(e=>{
        str += `<li>${e.title}</li>`
      })
      $('#parent').append(str)
    }
  })
</script>
```

### network开发者工具

我们已经可以得到从服务器响应给我们的动态数据了，但是请求响应有时候并不总是一帆风顺，所以我们需要借助一些工具对我们的请求和响应进行观察，让我们对这个过程中的细节更加了如指掌。

network开发工具就是这样一个工具。下面我们给大家反这个工具的使用讲解一下。

每当浏览器发生一次请求和响应，我们都可以在里面监视到。首先打开F12，找到 `network` 工具选项

![](F:\0001my\Notes\NodeJS.assets\networktools.png)



# NodeJS课程讲义-模块化

## 模块化

### 模块化的必要性

通过之前的学习，我们知道在处理动态请求的时候，我们需要判断不同的url来处理不同的请求，这个时候会有一个问题：一个网站的接口肯定是很多的，如果都写在一个js文件里面，代码多了会很不好扩展和维护。不仅仅是我们写接口的时候，但凡是代码，肯定会越写越多，如果全放在一个js文件里面，无疑是不合适的。

所以我们把代码分到多个js文件里面，势在必行。但是有一个问题，我们怎么对这些代码进行分割呢？这个时候有一个思想： **模块化**

### 模块化的概念及作用

代码的模块化，要求我们以功能为界限，把代码分割到不同的js文件里面，以达到随意组合，随意拆分，易于理解，易于扩展，易于维护，易于复用等目的。

其实我们之前使用的fs和path等，已经使用了模块化的思想。当我们需要操作文件时，我们找到fs模块，当我们需要处理目录时，我们找来了path模块，当我们需要和浏览器通信时，找来了http模块......我们可以做到随意组合，当我们在别的地方要用，也可能重复使用这些或者别的模块，每个模块中的功能单一了，代码自然就相对简洁了，也就提升了代码的可读性和可以性......

打个比方，一个程序好比是一个自行车，我们把我们的代码模块化成为每个轮子，铃铛，坐鞍，把手.....，如果要给这台自行车添加电动功能，只需要在原来的基础上添加电池的马达(易于扩展),如果它的铃铛坏了，我们就换个新的(易于维护)，如果我们想把它的轮子用于另一台车上，也是可行的(易于复用).....

所以模块化这个思想，是非常好用的，我们要掌握好。



### 模块化的实现

在js发展的历程中，模块化的标准出现过4个

* AMD
* CMD
* CommonJS
* ES Module

其中AMD和CMD历史久远，在此我们就不进行讲解了，有兴趣的同学自行百度。

[参考:AMD、CMD、CommonJs、ES6的对比]()

我们重点学习CommonJS和ES Module，CommonJS是Node环境原生支持的，有时候我们在开发中还会用到，而ES Module是JS官方推出的方式，目前在项目中已经广泛使用。

#### CommonJS模块化

模块化的语法分为导出和导入两部分，下面都是固定语法，大家熟记并使用熟练就好了。

##### 导出

```js
module.exports = { 导出的数据 }
或者
module.exports.键 = 导出的数据
或者
exports.键 = 导出的数据
```

其中 `module.exports` 和 `exports` 在最开始是同一个对象，并且js模块最终是以module.exports指向的对象为准，所以在使用CommonJS模块化的写法的时候，要注意：

1. exports 不能重新赋值，无效
2. module.exports 重新赋值后，导出的对象就变成了这个对象

##### 导入

```js
const 模块名称 = require('指定模块路径或者模块名称')
```

如：a.js

```js
module.exports = {add}
function add (a,b){ return a + b}
module.exports.reduce = reduce
function reduce (a,b) { return a - b }
```

b.js

```js
const a = require('./a.js')
console.log(a) // { add,reduce }
```

我们就可以把之前的代码变成模块化的写法，拆分出来

router.js

```js
// 把动态请求的功能放在这个router.js里面
module.exports = function(req,res){
    if(req.url === '/getArticle'){
        res.end(文章数据)
    }else if(req.url==='/login'){
        res.end(登录结果)
    }
    // TODO
}
```

server.js

```js
const http = require('http')
const fs = require('fs')
const path = require('path')
// 导入router.js里面导入的函数
const router = ruquire('./router.js')
const server = http.createServer()
server.listen(8080,'127.0.0.1')
server.on('request',(req,res)=>{
    if(/^\/views/.test(req.url)){
        fs.readFile(path.join(__dirname,req.url),(err,data)=>[
            res.end(data)
        ])
    }else{
      	// 调用函数处理动态数据
        router(req,res)
    }
})
```





#### ES Module(俗称es6模块化)

##### 导出：

```js
// 默认导出
export default 要导出的对象

// 按需导出
export { 要导出的数据 }
```

> 注意： 
>
> 1. 默认导出只能写1次
> 2. 多次按需导出会最终导出一个对象，是js文件里面所有按需导出的数据的集合

##### 导入

```js
// 默认导入
import 模块名 from '模块或者路径'

// 按需导入
import {数据 , 数据 ...} from '模块或者路径'

// 混合导入
import 模块名,{数据 , 数据 ...} from '模块或者路径'
```

> 注意：
>
> 1. 默认导入的名称不用和导出的那你一样
> 2. 按需导入的数据名称要和按需导出的数据名称要一样
> 3. 按需导入可以部分导入

如：

a.js

```js
// 默认导出
export default add
function add(a,b) { return a + b }
// 按需导出
export { add , reduce }
function reduce(a,b) { return a - b }
```

b.js

```js
// 默认导入
import fn from './a.js'
// 按需导入
import {add} from 'a.js'
// 混合导入
import fn,{add,reduce} from './a.js'
```

> 注意：
>
> 1. 后期我们使用ES Module的写法非常多，所以一定要掌握好
>
> 2. node环境下默认不支持ES Module的语法，需要：
>
>    a. 保证node版本在13及以上
>
>    b. 要使用.mjs结尾才能正常使用

相比于CommonJS而言，ES Module在浏览器中也可以直接使用

a.js

```js
export default function add(a,b){return a + b}
```

b.js

```js
import add from 'a.js'
```

html代码

```html
<body>
<script src="b.js" type="module"></script>
</body>
```

在浏览器里面使用ES Module的时候，注意一定要加上type="module"属性，以及需要以服务器环境打开页面，比如在vscode里面使用live server插件打开，不然无法执行。

> 了解一下就行，正常开发中我们不会使用这种用法的。



## 包管理工具

经过了之前的学习，我们已经掌握了如何实现浏览器和服务器的通信，不过相信大家已经有一个疑问了，我们自己又写前端，又写后端的情况下，如果什么都自己来完成，肯定会效率非常低，我们之前已经有过在前端代码里面使用插件实现效果的经验，那么我们在node里面有没有这种类似的做法呢？

有！Node除了本身自己的功能强大之外，周边衍生出来的生态圈同样强大 ———— NodeJS拥有数量非常庞大的插件，只不过我们把它们称为**"第三方模块"**

并且在Node当中，使用这些第三方模块也十分简单，因为Node中集成了管理这些第三方模块的工具，我们称为“**包管理工具**”

### npm

node中自带的包管理工具叫 NPM(Node Package Manager)，其实说白了无非也是一个软件，只是我们在安装Node的时候就已经"捆绑"安装了。只需要在cmd中输入 `npm -v` 就能看到当前的npm的版本号。

#### 作用

1. 下载并管理项目中使用到的第三方式模块(包)
2. 发布自己的模块到npmjs平台

### 使用

步骤1：初始化项目

在一个项目中初次使用npm，需要先交项目初始化。在自己项目的根目录，打开终端，输入

```shell
npm init -y
```

会得到一个package.json文件，文件描述了我们整个node项目的基本信息。

步骤2：下载需要使用的第三方模块

```shell
npm install 模块名称
例如：
npm install colors
```

下载完成我们会发现在根目录下多了一个node_modules文件，里面就是我们下载下来的模块。

步骤3：在https://npmjs.com 查找对应的文档学习如何使用下载下来的模块。

这部分内容由老师上课演示并带领大家学习。

### npm安装模式

npm安装第三方模块有三种方式：

1. 全局依赖方式 - 一次安装，在任何项目都能用，一般是方便项目构建的工具
2. 生产依赖方式 - 上线需要依赖的模块
3. 开发依赖方式 - 只是在开发的时候使用的模块，上线不需要使用

#### 各方式安装命令

```shell
# 全局安装
npm install -g 模块    或者   npm install --global 模块
# 生产依赖安装
npm install --save-dev 模块 或者  npm install -S 模块
# 开发依赖安装
npm install --dev 模块 或者 npm install -D 模块
```

#### nodemon

我们之前每次修改了node代码，都需要重新执行，这样还是比较麻烦的。所以我们推荐大家一个工具 ———— nodemon,它可以在我们保存代码的时候就自动重启代码

安装：

```shell
npm install -g nodemon
```

使用

```shell
nodemon 01.js
```

> 全局安装了nodemon后，只需要把node命令换成nodemon即可

#### npm镜像

如果有同学下载模块很慢，一般就是网络问题。npn默认也是到国外下载包的，所以我们可以手动修改其下载的源

```shell
# 配置到淘宝服务器
npm config set registry https://registry.npm.taobao.org
# 查看 registry 是否配置正确
npm config get registry
```

### yarn

`Yarn` 是于 2016 年 10 月 由 Facebook、Google、Exponent 和 Tilde 联合推出了一个新的 JS 包管理工具，旨在取代 npm 这种包管理工具。

官网：
https://yarnpkg.com/en/docs

中文参考链接：
https://yarn.bootcss.com/



**特点**：

- 速度超快

> yarn 缓存了每个下载过的包，所以再次使用时无需重复下载。 同时利用并行下载以最大化资源利用率，因此安装速度更快。

- 超级安全

> 在执行代码之前，yarn 会通过算法校验每个安装包的完整性。

- 超级可靠

> 使用详细、简洁的锁文件格式和明确的安装算法，yarn 能够保证在不同系统上无差异的工作。

**安装**:

管理员模式运行cmd   ：**npm install -g yarn**



**常用命令**：

| npm                          | yarn                    |
| ---------------------------- | ----------------------- |
| npm init -y                  | yarn init -y            |
| npm install react --save     | yarn add react          |
| npm uninstall react --save   | yarn remove react       |
| npm install react --save-dev | yarn add react --dev    |
| npm update --save            | yarn upgrade            |
| npm install -g nodemon       | yarn global add nodemon |

**yarn 全局安装后，命令不生效**

背景：

1. 执行 `yarn global add nodemon 后，重启 `bash......`， vue 命令依然不生效
2. 而 npm 全局安装（npm install -g nodemon）后，命令生效

解决办法：

1.执行如下命令，得出 yarn 全局安装的命令所处的安装目录

```shell
yarn global bin 
```

2.复制安装目录至电脑的环境变量中
![](F:\0001my\Notes\NodeJS.assets\2018110718150477.png)

3.重新启动终端，发现全局命令行可以生效了



### package.json

我们发现使用yarn和npm，都要先把项目初始化，而初始化的结果就是生成一个package.json文件。这个文件到底有什么用？

1. 记录了你这个项目的主要信息
2. 可以明确项目的依赖，将来即使把node_modules删除了，也可以通过这个文件找回
3. 声明简短的命令，来代替复杂的命令
4. ...



> 小结：
>
> 1. 包管理工具是我们在后面的学习，以后的工具中一定会用到的，所以一定要会使用
> 2. 每个项目一定要检查有没有 package.json ，如果没有，一定要先 init
> 3. node_modules文件夹里面就是我们下载的第三方模块，在传输代码的时候要记得排除这部分
> 4. 将来在工作中，yarn或者npm都可能会使用，要熟悉对应的命令



# NodeJS课程讲义-express服务器框架

## Express

为了提高开发效率，我们在开发过程中，都会尽量使用别人已经开发好的第三方模块，而我们想要快速实现服务器端的开发，推荐一个当下比较流行的框架：Express

[Express](http://www.expressjs.com.cn/) 作为开发框架，因为它是目前最稳定、使用最广泛，而且 Node.js 官方推荐的唯一一个 Web 开发框架。除了为 http 模块提供了更高层的接口外，还实现了许多功能，其中包括：

- 静态文件服务；
- 路由控制；
- 模板解析支持；
- 动态视图；
- 用户会话；
- 错误控制器；
- 插件支持。

官网：<http://www.expressjs.com.cn/> 

express 是一个基于`内置核心 http 模块`的，一个`第三方的包`，专注于 `web 服务器`的构建。   



### 基本使用

- 首先创建一个名为 myapp 的目录，在命令行输入并运行 **yarn init -y** （或者 npm init -y）。 
- 使用 **yarn add express ** （或者 npm install express ）安装 Express 包；
- 其次在 myapp 目录中，创建一个名为 app.js 的文件，并复制下面示例中的代码。

```js
// 1、引入express模块并创建express对象
const express = require('express');
const app = express();

// 2、书写处理请求的方法，来响应请求
app.get('/', (req, res) => {
    // 这里的代码在浏览器以get请求/的时候执行，  
    // 这个函数就是用来处理浏览器的 对于/的get请求 的
    // 第一个参数req是请求头对象，里面包含请求头信息
    // 第二个参数res用来做响应
    console.log(req);    
    res.send('Hello World!');
});

// 3、监听端口
app.listen(3000, () => {
    //这里的代码服务器刚启动的时候执行1次
    console.log('Example app listening on port 3000!')
});
```

使用 node app.js 启动应用，访问 http://localhost:3000/ 就可以看到效果。

### 处理静态资源

exprss中已经帮我们封装好了判断指定url开头，并指定对应文件夹的方法

```js
const express = require('express');
const app = express();
app.listen(3000)
// app.use(url以什么开头,express.static(去哪个路径下获取))
// 如： url以views开头， 让请求去 views目录里面读取资源
app.use('/views',express.static('views'))
```

### 处理get请求

在express里面也已经封装好了监听get请求的方法，如果我们希望浏览器以get方式请求数据，操作方法如下：

```js
const express = require('express');
const app = express();
app.listen(3000)
app.use('/views',express.static('views'))
// 使用app.get监听浏览器的get请求
app.get('/getArticles',(req,res)=>{
  // req , res 和我们之前写原生node一样，也是请求对象和响应对象
  // 通过 req.query 得到请求带回的数据
  console.log(req.query)
  // 通过res.send()返回数据
  res.send({
    code:200,msg:'ok',
    data : [ {id:1,title:'标题1'},{id:2,title:'标题2'},{id:3,title:'标题3'}, ]
  })
})
```

此时我们只需在views目录里面有一个articles.html，并通过 http://127.0.0.1:3000/views/articles.html访问就可以在里面使用ajax发请求并得到数据。

```html
<h1>
  artilces页面
</h1>
<script src="jquery.js"></script>
<script>
	$.ajax({
    url:'http://127.0.0.1:8080/getArticles',
    // 带数据回服务器
    data : {pageIndex:1,pageSize:10},
    success(res){
      console.log(res)
    }
  })
</script>
```



### 处理post请求

express里面同样封装好了监听post请求的方法，也是学会如何使用就行了。post监听也很简单，只是对于得到数据的处理会稍微有点和get不同

```js
const express = require('express');
const app = express();
app.listen(3000)
app.use('/views',express.static('views'))
// post请求带回的数据有多种格式，所以我们要先决定好能解决哪种格式
app.use(express.urlencoded({extened:true})) // 这是解析 key=value&key=value格式的
// 使用app.post监听浏览器的post请求
app.get('/login',(req,res)=>{
  // 通过 req.body 得到请求带回的数据,一定是有了上面的app.use才能得到数据
  console.log(req.body)
  // 通过res.send()返回数据
  res.send({
    code:200,msg:'ok',
    data : {
      token: 'apsdiufpsaugipwerkmcasd034lijsdf...'
    }
  })
})
```

> 小结： express快速完成服务器开发
>
> 1. 使用 express.static 处理静态资源
> 2. 使用 app.get 监听get请求，通过 req.query 得到数据
> 3. 使用 app.post 监听 post 请求，通过 express.urlencoded 解析数据，使用 req.body 得到数据

### 服务器端渲染(了解)

#### 概念

我们现在所掌握的开发模式都是前后端分离的，但是在开发中还会有一种情况也是大家必须知道的，这个方式就是**服务器端渲染**，简称**SSR**

SSR（server side render）指的是把页面数据在服务器端的时候就先把动态数据写入返回数据里面，不需要再使用ajax请求回来再渲染。

这样做的好处有：

1. 减少浏览器请求服务器的次数
2. 利于SEO

但是相对的也会增加服务器的压力，同时增加了开发成本，所以大家要明白做ssr的主要目的是为了SEO，如果没必要SEO的网站，是没必要做ssr的。

需要SEO的网站：

* 电商
* 门户
* 社区
* ...

不需要SEO的网站

* 企业内部系统
* 网站后台
* ...



#### express中的ssr

express中使模板引擎来实现ssr，而模板也只是已经封装好的第三方模块，我们只要大概结合使用。

express官方推荐使用pug模板引擎来实现ssr，所以我们要先下载

```js
npm i pug   或者  yarn add pug
```

然后要设置pug为默认的渲染视图引擎

```js
app.set('view engine', 'pug')
```

然后我们在views里面写一个index.pug,输入下面的代码

```
html
  head
    title= title
  body
    h1= message
```

这是pug模板我有的语法，左边是对应的标签，等号后面是对应的js变量，然后我们在请求的时候把数据传入模板引擎，进行渲染

```js
app.get('/', function (req, res) {
  // 参数1是指要去views里面找index.pug
  // 参数2是要传入pug里面解析的数据
  res.render('index', { title: 'Hey', message: 'Hello there!' })
})
```

此时只要访问http://127.0.0.1:3000/就能看到数据。

如果要继续实现更加复杂的效果，就要继续学习pug的特殊用法，如果有兴趣请点击[【pug官方文档】](https://pugjs.org/api/getting-started.html)

当然express也还可以结合其它的模板引擎,[查看](https://www.expressjs.com.cn/guide/using-template-engines.html)



# NodeJS课程讲义-数据库和跨域处理

## 数据库

到目前为止，我们的服务器代码已经能够实现动态请求响应数据了，可是事实上我们的数据还是在js代码里面写死的，不是真正的动态。真正的动态数据是在数据库里面的，所以接下来我们要学习的就是对于数据库的操作了。但是其实对于前端来说，数据库是不需要我们操作的，所以我们只需要了解一下就行。

### 概念

![image-20210317184327015](F:\0001my\Notes\NodeJS.assets\image-20210317184327015.png)

数据库其实只是一个用来管理数据的软件，市面上成熟的数据库软件也有很多，而我们只给大家演示mysql的操作。首先还是要先下载安装，但是mysql数据库的安装还是比较麻烦的，所以我们使用一个集成环境来给大家演示一下就好了

### 相关软件安装

下载并安装phpstudy，[phpstudy官网](https://www.xp.cn/)，phpstudy的安装非常简单，只需要安装在没有中文、特殊字符、空格的目录下就行，如果安装好后报错，基本可以确定你的路径有中文或者空格等，就重新安装吧。

<img src="F:\0001my\Notes\NodeJS.assets\image-20210317184922588.png" alt="image-20210317184922588" style="zoom:50%;" />

但是这个时候我们并没有看到里面的数据，所以我们还需要一个能查看数据的软件 ———— 数据库管理工具。同样这样的软件也有很多，我们课程中使用的是`navicat for mysql` , 安装过程也很简单，想换安装目录就就换，不想换的直接下一步就行了。

之后打开navicat，对数据库进行连接

<img src="F:\0001my\Notes\NodeJS.assets\image-20210317185650287.png" alt="image-20210317185650287" style="zoom:50%;" />

正常每个网站都有自己独立的数据库，所以我们新建一个自己数据库

<img src="F:\0001my\Notes\NodeJS.assets\image-20210317190038768.png" alt="image-20210317190038768" style="zoom:50%;" />

然后创建数据表格。

<img src="F:\0001my\Notes\NodeJS.assets\image-20210317190348675.png" alt="image-20210317190348675" style="zoom:50%;" />

之后只要把表格保存为student，就可以记录数据了。

### sql

在mysql数据库里，使用一种特殊的语言操作数据，这种语言我们称为： **sql**

查数据

```sql
select 字段,... from 表格
如：
select id,name,birthday from student
```

新增数据

```sql
insert into 表格 set 字段=数据,字段=数据,...
如：
insert into student set name='狗蛋',birthday='1999-09-09'
```

修改数据

```sql
update 表格 set 字段=数据,字段=数据,... where 条件
如：
update student set name='李狗蛋' where id = 1
```

删除数据

```sql
delete from 表格 where 条件
如：
delete from student where id = 1
```

### 使用Node操作数据库

我们真正会在node服务器里面写好了代码后，再操作数据库的数据，所以我们将要学习如何使用node操作数据库。

我们要使用的是一个叫mysql的第三方模块，所以先下载

```shell
npm i mysql   或者  yarn add mysql
```

[官方文档](https://www.npmjs.com/package/mysql) 里面会教我们如何使用这个第三方模块

```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : '127.0.0.1', // 服务器ip
  user     : 'root',  		// 用户名
  password : 'root',			// 密码
  database : 'db_test'    // 数据库名称
});
// 执行sql语句操作数据
connection.query('select * from student', function (error, results, fields) {
  if (error) throw error;
  console.log(result);
});
```

> 注：数据库这块不要求大家掌握，只要能大概知道如何操作数据就行。

## 跨域

### 同源策略

跨域，是指**浏览器不能执行其他网站的脚本**。它是**由浏览器的同源策略造成**的，是浏览器对JavaScript实施的安全限制。

所谓同源是指，域名、协议、端口均为相同，只要任意一个不同，就是非同源，就会形成跨域。

比如在我们自己的网站，向百度发送了一个请求，当百度的服务器返回了数据，浏览器会发现这个数据的来源不是自己的网站的，而是一个陌生人给它的，它就会信不过这个响应回来的数据，就会限制很多里面的操作。

但是我们在平时是有时候需要跨域发出请求的。比如：1、自身业务是出现很多端(前后端分离开发)   2、和第三方合作， 以及面试也会经常问这块的东西。所以我们有必要解决一下跨域带来的问题。

### 跨域解决

跨域问题是个非常经典的开发场景，市面上也有非常多的解决方案，我们今天主要学习几个大家比较容易理解的。

#### jsonp解决跨域

jsonp的原理是复用 src 这种能自带跨域能力的属性进行请求，然后要求服务器把数据放在一个函数调用的格式里面返回，最终我们在前端准备一个函数，进行数据的处理

```html
<script>
  // 在前端准备一个函数，用于接收并处理数据
	function receive(data){
    console.log(data)
  }
</script>
// 使用src发起请求，带上前端用于接收数据的函数名
<script src="http://127.0.0.1:8080/jsonp?callback=receive" ></script>
```

```js
const express = require('expredd')
const app = express()
app.listen(8080)
app.get('/jsonp',(req,res)=>{
  // 得到前端用于接收数据的函数名
  let {callback} = req.query
  let data = JSON.stringiry({code : 200,msg:'ok'})
  // 以 函数名(数据) 的形式把数据响应回浏览器
  res.send(`${callback}(${data})`)
})
```

这个方式确实可以解决跨域，但是要求前后端要紧密配合，否则无法实现。

#### 服务器设置响应头

另一个方式是我们直接在服务器设置允许跨域的响应头，这样就完全在服务器就解决了跨域的问题。

```js
const express = require('expredd')
const app = express()
app.listen(8080)
app.get('/corsdata',(req,res)=>{
  // 直接设置允许跨域的响应头
  // 这个键是http里面约定好的，不能写错
  res.setHeader('Access-Control-Allow-Origin','*')
  res.send({code:200,msg:'ok'})
})
```

然后我们直接在浏览器里面发起跨域的请求，也能正常获取了。

#### 设置代理服务器

设置代理服务器的原理其实也比较简单，浏览器向代理服务器发送请求，代理服务器是设置了允许跨域的，然后再由代理服务器向真正的服务器发起请求，再把数据转发回浏览器

![image-20210318101924881](F:\0001my\Notes\NodeJS.assets\image-20210318101924881.png)

先准备好真正处理请求的服务器

```js
const express = require('express')
const app = express()
app.listen(8080)
// 监听一个get请求
app.get('/proxydata',(req,res)=>{
    res.send({code:200,msg:'ok'})
})
```

然后准备代理服务器

```js
const http = require('http')
const server = http.createServer()
server.on('request',(req,res)=>{
	  // 在代理服务器里面设置允许跨域
    //设置允许跨域的域名，*代表允许任意域名跨域
    res.setHeader("Access-Control-Allow-Origin","*");
    //允许的header类型
    res.setHeader("Access-Control-Allow-Headers","content-type");
    //跨域允许的请求方式 
    res.setHeader("Access-Control-Allow-Methods","DELETE,PUT,POST,GET,OPTIONS");
		
  // 监听浏览器的请求
    if(req.url === '/proxydemo'){
      // 请求真正的数据服务器
        http.get('http://127.0.0.1:8080/proxydata',(result)=>{
            let data = ''
            result.on('data',chunk=>data += chunk)
            result.on('end',()=>{
              	// 转发响应的数据回到浏览器
                res.end(data)
            })
        })
    }
})
server.listen(8081)
```

在html中请求代理服务器

```html
<body>
    <script>
        let xhr = new XMLHttpRequest()
        // 请求代理服务器
        xhr.open('get','http://127.0.0.1:8081/proxydemo')
        xhr.send()
        xhr.onreadystatechange = function(){
            console.log(xhr.responseText)
        }
    </script>
</body>
```

> 注：我们后期使用最多的是代理服务器的方式，只不过我们将来都有对应的构建工具来快速实现，大家只需要知道代理服务器的原理即可。

；
