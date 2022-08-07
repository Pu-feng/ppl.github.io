# 报错大全

## 编程

###  $ is not defined

> 没有引入jQuery的Js文件

### 绑定元素是集合时

> 要用this获取当前的 再找其子或父级进行修改。
>
> 如下面的不能是直接$('p').hide(); 这样去修改

```js
<li>
    <p>怎样在不为人知的情况 15.10元</p>
	<img src="images/img.jpg" alt="">
</li>

$('li').mouseenter(function () {
    $(this).children('p').hide();
    $(this).children('img').show();
})
```



### 事件源后面报错

> 基本就是事件源没有获取成功



### (intermediate value)(...) is not a function

```js
 //通过函数构造器定义
function beverage_treat(){
 
} // 这里不用加分号
//通过函数表达式定义, 此时我们认为该函数是一个变量
var beverage_treat = function(){
 
}; // 这里一定要加分号，不然在后面紧跟一个如下形式的函数封装时会报错(intermediate value)(...) is not a function
```

```js
// 前面要加分号，后面也要加，这里和上边都忘记分号时报错
;(function(){
 
})();
```



## 系统方面



## npm相关

安装时出错

> This version of npm is compatible with lockfileVersion@1, but package-lock.json was generated for lockfileVersion@2. I'll try to do my best with it!
>
> 网上案例：
>
> 首先想到的就是npm版本跟你引入的包版本不同，
> 需要升级 或 降级，看依赖的包是低版本还是高版本，
> 从我的报错可以看出npm适合于lockfileVersion@1的，但是package-lock.json是源于lockfileVersion@2的。因为代码中使用的某个包只能用特定版本的npm下载，所以会报错导致npm install失败。这时就需要升级一下npm。
> 我自己遇到的：
>
> 是因为node版本太低，和我之前构建项目的node的版本不一致构成的，这时候可以切换会之前的node版本尝试，这时候就可以了。





Vue

安装vuex后使用报错

```
Uncaught TypeError: vue__WEBPACK_IMPORTED_MODULE_20__.reactive is not a function
```

> 此错误的原因是vuex版本不匹配问题，项目中创建用的是vue2,而如果直接输入
> npm i vuex -S
> 会自动给你安装高版本的vuex,比如4.0.6.而高版本的vuex和vue2不兼容，所以会导致以上问题
>
>
> 解决
> 1：首先卸载之前安装的vuex
> npm uninstall vuex
> 2: 然后下载固定版本的vuex
>
> npm i vuex@3.6.2 -S
> 其中：@3.6.2 就是指定的版本号，也可选择其他版本号。
> 3：记得重新运行前端，然后再去查看页面。
> ————————————————
> 版权声明：本文为CSDN博主「Mr.指尖舞者」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/qq_56989560/article/details/124673924





## Vue

### 点击同个路由报错问题

在新版本的vue-router中，重复点击同一个路由会出现以下报错：

![1604585178027](F:\0001my\Notes\error.assets\1604585178027.png)

解决方案如下：

方案1、vue-router降级处理(但不推荐)

```shell
npm i vue-router@3.0.7
```

方案2、直接在push方法最后添加异常捕获，例如：

```vue
<van-search v-model="SearchVal" shape="round" placeholder="请输入搜索关键词" disabled @click="$router.push('/home/searchPopup').catch(err=>{})"/>
```

方案3、直接修改原型方法push(推荐)

```js
// 把这段代码直接粘贴到router/index.js中的Vue.use(VueRouter)之前
const originalPush = VueRouter.prototype.push;
VueRouter.prototype.push = function(location) {
  return originalPush.call(this, location).catch(err => {})
};
```



### 使用localStorage时问题

```
SyntaxError: Unexpected token u in JSON at position 0
```

> 当时是用到了刷新浏览器或关闭时执行那个事件才出的错，后面用了事件监听解决了

```js
// 事件监听的就行
    window.addEventListener('beforeunload', () => {
      localStorage.setItem('goodslist', JSON.stringify(this.goodslist));
    });
    // window.onbeforeunload = function () {
		// 会报错
    //   localStorage.setItem('goodslist', JSON.stringify(this.goodslist));
    // };
```



### // 解决Vue-Router升级导致的Uncaught(in promise) navigation guard问题	

*const* originalPush = VueRouter.prototype.push;

VueRouter.prototype.push = *function* push(*location*, *onResolve*, *onReject*) {

 if (*onResolve* || *onReject*) return originalPush.call(this, *location*, *onResolve*, *onReject*);

 return originalPush.call(this, *location*).catch(*err* *=>* *err*);

};





### vue -(问题系列) TypeError: routes.forEach is not a function

订阅专栏

![img](https://img-blog.csdnimg.cn/20190308082255573.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2phY2tfYm9i,size_16,color_FFFFFF,t_70)问题原因：

![img](https://img-blog.csdnimg.cn/2019030808233629.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2phY2tfYm9i,size_16,color_FFFFFF,t_70)

来源线索：https://ask.csdn.net/questions/710037 用户：[qq_37744644](https://my.csdn.net/qq_37744644) 的评论

总结：添加一个符合routes的选项要求的[数组](https://so.csdn.net/so/search?q=数组&spm=1001.2101.3001.7020)。

 
