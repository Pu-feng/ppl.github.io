# React全家桶笔记

## 一、认识React

> 小节目标：
>
> 1.了解react的特点。
>
> 2.根据自己的能力给自己一个学习react的目标。

### 1.关于React

![image-20220618121500125](F:\next\react\day01\笔记\day01.assets\image-20220618121500125.png)

**React官方中文网站：** https://react.docschina.org/

**React**是Facebook公司的一个内部项目，最初用于自己构造Facebook网站，后来于2013年5月开源。由于拥有较高的性能，且代码逻辑非常简单，越来越多的人已开始关注和使用它。

**React**是一个用于构建用户界面的 JavaScript 库,具有如下特点：

**a、声明式设计**

 react是面向数据编程，不需要直接去控制dom，你只要把数据操作好，react自己会去帮你操作dom，可以节省很多操作dom的代码。这就是声明式开发。

**b、使用JSX语法**

 JSX 是 JavaScript 语法的扩展。React 开发大部分使用 JSX 语法（在JSX中可以将HTML于JS混写）。

**c、灵活**

 react所控制的dom就是id为root的dom，页面上的其他dom元素你页可以使用jq等其他框架 。可以和其他库并存。

**d、使用虚拟DOM、高效**

 虚拟DOM其实质是一个JavaScript对象，当数据和状态发生了变化，都会被自动高效的同步到虚拟DOM中，最后再将仅变化的部分同步到DOM中（不需要整个DOM树重新渲染）。

**e、组件化开发**

 通过 React 构建组件，使得代码更加容易得到复用和维护，能够很好的应用在大项目的开发中。

**f、单向数据流**

 react是单向数据流，父组件传递给子组件的数据，子组件能够使用，但是不能直接通过this.props修改。 这样让数据清晰代码容易维护。

------

> React相对于vue来说入门难度会相对高，不具有大量的语法糖来简化开发者操作，但是也具有更大的开放性和可定义性。

 

### 2.课程定位

目前对于国内的前端开发大环境来说，React主要是一些大公司在用，中小型公司主要还是以使用vue为主，其余框架为辅的模式。所以这个课程对于不同同学的意义如下：

a.学的比较好的同学：React可以增强优势，在学习了这门课程后，有机会冲击大公司，或者冲击更高的薪资。在之后可以自己找几个项目自己练习，也可以把React写入简历里面。

b.学的比较一般的同学：了解一下React和vue之前的区别，具有入门级的React开发能力，在面试中可以有一定的加分。

c.学的不够好的同学：可以完全放弃React的学习，也可以稍微看看，建议随便了解一下，上课期间完全可以自己回顾或者练习vue的内容。

 

## 二、React的基本使用

> 小节目标：
>
> 1.使用脚手架创建项目。
>
> 2.掌握react入口文件的基本写法。

### 1.使用 `create-react-app` 脚手架创建项目

```
npx create-react-app 项目名  或者  yarn create react-app 项目名
```

> npx 是一个临时使用第三方模块的命令，会临时下载这个包，使用完毕就删除了
>
> 使用脚手架尽量使用比较新的node版本，至少使用 v12.13.1以上的版本，推荐使用v14版本(其实正常来说都是使用当前的稳定版本)。

### 2.项目结构

我们创建好了项目，可以看到项目里面基本结构如下：

![image-20220618121441721](F:\next\react\day01\笔记\day01.assets\image-20220618121441721.png)

打开index.js,我们可以看到如下代码：

```jsx
import React from 'react'; // react项目基本环境，是核心库，一定要引入
import ReactDOM from 'react-dom'; // react用于渲染的库
import './index.css'; // 导入全局样式
import App from './App'; // 导入app组件
import reportWebVitals from './reportWebVitals'; // 暂时无用
// 调用渲染的方法，把一个结构渲染到 id为root的div上
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root') // 这个id为 root 的div在index.html里面
);
reportWebVitals();
```

### 3.启动项目

在package.json里面的scripts字段中

```
{
    ...
    "scripts": {
        "start": "react-scripts start",
        "build": "react-scripts build",
        "test": "react-scripts test",
        "eject": "react-scripts eject"
    }
    ...
}
```

正常start就是启动项目，build是打包项目，test是以测试方式打包，eject是react独有的解包操作。

所以我们只需要在项目根目录下使用 npm start 或者 yarn start 就可以启动项目。

### 4.精简项目

我们一开始学习的时候，不需要这么多内容，所以我们直接把src目标下的所有内容直接删除，然后自己新建一个index.js就够了。

然后在index.js里面输入下面的代码：

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

ReactDOM.render((
  <h1>Hello World</h1>
),
  document.getElementById('root')
)
```

但是其实在react18里面已经不推荐使用ReactDOM.render()的方式来渲染了，虽然还能用，也许会在将来就慢慢废弃并过渡到新写法。但是我们新旧的写法都要会。

react18的createRoot的用法。

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
const rootEl = document.getElementById('root')
const root = ReactDOM.createRoot(rootEl)
root.render(<h1>Hello World</h1>)
```

 

 

## 三、JSX语法

> 小节目标：
>
> 1.掌握jsx语法(如何写html，如何写js)。
>
> 2.了解react项目中的可能文件后缀。

### 1.了解JSX

JSX其实就是在JS里面写XML(HTML),在React里面使用JSX来代替常规的JS。

我们不需要一定使用 JSX，但它有以下优点：

- JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
- 它是类型安全的，在编译过程中就能发现错误。
- 使用 JSX 编写模板更加简单快速。

通常来说，在React项目里面，无论是.js文件还是.jsx文件，都可以写JSX语法。也就是说无论是.js还是.jsx都是React的组件，所以当我们创建一个组件文件时，写.js或者.jsx都是可以的。但是推荐使用.jsx，这样可以更加明确这是一个jsx的组件。

 

### 2.在js里面写HTML

JSX语法允许我们直接在js里面写HTML代码

```jsx
ReactDOM.render(
  <div>HTML</div>,
  document.getElementById('root')
)
```

但是在jsx里面推荐使用一个小括号来把HTML结构包起来

```jsx
ReactDOM.render(
  (
    <div>HTML</div>
  ),
  document.getElementById('root')
)
```

这样区分度高，并且可以在编译的时候避免一些复杂的结构造成的编译问题。

 

### 3.在HTML里面写JS

JSX除了允许在js里面写HTML外，还可以在HTML里面写js，只是要求一定要在html里面加上一对大括号，然后在大括号里面写js。

jsx的大括号里面可以写你想要的表达式，可以可以写对应要渲染的变量之类的。最终会被作为js执行并渲染到页面上。

```jsx
const person = { name:'狗蛋' };
ReactDOM.render((
  <div>{ person.name }今年{ Math.floor(Math.random() * 100) }岁了</div>
),
  document.getElementById('root')
)
```

html里面的大括号，相当于给html内部开辟了一个执行js的空间。

### 4.后缀

react里面默认支持的可以写jsx语法的后缀有： `.js`/`.jsx` 后期我们学习了typescript后还可以写成 `.tsx`。这只是一个小常识，大家一定要有这样的认知。

### - 小结：

> 1.在jsx里面可以html和js混写
>
> 2.在js里面写html要加小括号
>
> 3.在html里面写js要加大括号
>
> 4.js/jsx/tsx文件里面都可以写jsx语法

## 四、组件化开发

> 小节目标：
>
> 1.掌握react的组件化用法。

组件化开发已经是现在前端开发的标配，也为了我们后续的课程比较好讲解，我们先来简单地学习一下react里面的组件化开发。

### 1.class组件

在早期的react用法里面，主要是class组件，但是因为这种方式量级比较重，以及使用起来比较繁琐，后期维护难度比较高，所以在后期的项目中已经基本不使用了。但是我们还是要知道这种写法。

定义一个class组件的基本格式如下。

```jsx
import { Component } from "react";

export default class ComClass extends Component {
  render() {
    return <div>ComClass</div>;
  }
}

```

class组件需要我们继承自react提供的一个Component类，并在里面提供一个render方法，来返回一个jsx结构。

### 2.函数式组件

react16.8开始，因为hook的推出，极大地提升了函数式组件的实用性，所以基本在外面的项目中，都全面转型到了 `FC + Hook` 的用法。也就是说函数式组件是我们学习的重点。

定义一个函数组件的基本格式如下：

```jsx
export default function ComFun() {
  return <div>ComFun</div>;
}
```

对比可以看出，函数式组件只有一个函数，需要返回一个jsx结构。相比于class组件而言，非常地轻量。它的好处不止于此，我们在后期的学习过程中慢慢来发现。

## 五、小案例：Tab栏

> 小节目标：
>
> 1.掌握react中如何使用样式。
>
> 2.掌握react中如何循环渲染内容。
>
> 3.掌握react中如何使用事件(注意this指向问题)。
>
> 4.掌握class组件的响应式数据使用。

接下来我们通过一个tab栏小案例来学习一下react里面的`样式操作`,`列表渲染`,`事件操作`,`响应式数据操作`等基础知识。

![tab-eff](F:\next\react\day01\笔记\day01.assets\tab-eff.gif)



### 1.样式操作

在react里面同样支持行内样式和外链样式。

#### a.外链样式

其中外链样式最简单，只需要在组件里面引入对应的外部样式就行。

```jsx
import React, { Component } from "react";
import "./tab.css";

export default class Tab extends Component {
  render() {
    return <div>Tab</div>;
  }
}
```

#### b.行内样式

当然也支持行内样式。但是注意，react里面只支持使用对象的方式声明行内样式。

```jsx
export default class Tab extends Component {
  render() {
    return (
      <div
        style={{
          width: "400px",
          minHeight: "400px",
          border: "1px solid #ccc",
          margin: "0 auto",
        }}
      >
        Tab
      </div>
    );
  }
}
```

> 值得注意的是，style的后面我们写了两对大括号。最外面的一对是指我们要在html里面开启js执行环境，里面的一对是我们写的对象语法的括号。

#### c.className

当然我们也可以使用类名的方式控制样式。但是要注意，因为class属性与es6的class关键字会产生冲突，所以在react里面使用了className代替了class属性。

```
export default class Tab extends Component {
  render() {
    return (
      <div>
        <div className="tab-out tab-b">Tab</div>
        <div className={"tab-out"}>Tab</div> {/* 其实这种写法和不写大括号几乎没有区别 */}
        <div className={["tab-out", "tab-b"].join(" ")}>Tab</div>
      </div>
    );
  }
}
```

> 在react里面还有一个html属性也是和js的关键字冲突的。label标签有一个for属性，也是和js的for是冲突的，所以在react里面使用labelFor来代替(了解)。

### 2.列表渲染

正常来说我们的页面很多数据都是动态渲染的，我们一般根据一个数组来进行动态渲染。在react里面没有类似vue的指令，所以我们必须自己手动循环生成。

在react里面我们一般采用map方法对数组进行循环，因为map方法可以返回我们想要渲染的jsx结构。

```jsx
const tabItems = ["首页", "新闻", "购物", "其它"];
const tabContent = [
  "欢迎您，狗蛋先生",
  "今日，全球首富狗蛋先生和翠花女士结为夫妇",
  "没钱，买什么买",
  "...",
];

export default class Tab extends Component {
  render() {
    return (
      <div className="tab-out">
        <ul className="flex">
          {tabItems.map((item, key) => (
            <li key={key}>{item}</li>
          ))}
        </ul>
        <div className="content">
          {tabContent.map((item, key) => (
            <section key={key}>{item}</section>
          ))}
        </div>
      </div>
    );
  }
}
```

在react里面，为了保证diff算法对于dom对象的重用处理，也需要给每个循环生成的结构添加一个key属性。

 

### 3.事件处理

事件是我们常用的处理用户交互的方式，那么在react里面如何处理事件呢？react里面处理事件的固定格式是

```jsx
<element on事件={处理函数}>some thing</element>
// 例如
<button onClick={()=>{console.log('点击事件')}}>按钮</button>
```

所以我们需要给每个tab-item添加事件，只需要：

```jsx
<ul className="flex">
    {tabItems.map((item, key) => (
        <li
            key={key}
            onMouseEnter={(e) => {
                console.log(e.target);
            }}
            >
            {item}
        </li>
    ))}
</ul>
```

但是我们通常需要将处理函数写到render函数的外面，因为我们的事件处理函数里面的代码可能非常复杂，直接写在jsx里面会非常难以维护。

```jsx
export default class Tab extends Component {
  onItemMouseEnter(e) {
    console.log(e.target);
  }
  render() {
    return (
      <div className="tab-out">
        <ul className="flex">
          {tabItems.map((item, key) => (
            <li key={key} onMouseEnter={this.onItemMouseEnter}>
              {item}
            </li>
          ))}
        </ul>
        <div className="content">
          {tabContent.map((item, key) => (
            <section key={key}>{item}</section>
          ))}
        </div>
      </div>
    );
  }
}
```

但是这样写会存在this丢失的问题，如果我们需要在一个事件处理函数里面调用class里面的另一个方法，就会报错。

```jsx
export default class Tab extends Component {
    testFn() {
        console.log("testFn");
    }
    onItemMouseEnter() {
        // 在事件处理函数里面调用另一个方法
        this.testFn();
    }
    render() {
        return (
            <div className="tab-out">
                <ul className="flex">
                    {tabItems.map((item, key) => (
                        <li key={key} onMouseEnter={this.onItemMouseEnter}>
                            {item}
                        </li>
                    ))}
                </ul>
                );
      }
}
```

我们可以看到在浏览器的控制台里面报错了。

![image-20220618121927528](F:\next\react\day01\笔记\day01.assets\image-20220618121927528.png)

所以我们需要在写事件处理函数的时候给该函数绑定this。

#### a.方式1

```jsx
<li key={key} onMouseEnter={this.onItemMouseEnter.bind(this)}>
```

b.方式2

```jsx
// 1. 在constructor里面给方法绑定this，使用一个别名保存
constructor(props) {
    super(props);
    this.mouseEnterHandler = this.onItemMouseEnter.bind(this);
}
// 2. 直接在事件里面使用别名
<li key={key} onMouseEnter={this.mouseEnterHandler}>
```

 

### 4.state&setState

在tab栏这个案例里面，我们需要一个索引值表示当前是第几个tab-item是激活的，并且可以在事件里面对这个索引进行修改。这就要使用到react里面的响应式数据。

在react里面我们需要使用一些响应式的数据，需要使用react的state属性。其基本用法如下：

```jsx
constructor(props) {
    // props是我们后面做父子数据传递用的，先这么写
    super(props);
    // 1. 定义一个state属性(只能是这个属性名)
    // 2. 并且只能在costructor函数里面定义并直接赋值。
    this.state = {
        currentIndex: 0,
    };
}
```

然后我们在组件中就可以使用这个state了。

```jsx
<li
    key={key}
    className={key === this.state.currentIndex ? "active" : ""}
    onMouseEnter={this.onItemMouseEnter.bind(this)}
    >
```

然后我们需要在事件里面对这个state进行修改，在react里面必须使用setState方法来进行响应式数据的修改。其基本使用方式如下：

```jsx
this.setState({
    propName:propValue,
    ...
})
```

我们的需求应该是在鼠标移入tab-item的时候，把当前的索引设置给state里面的索引，所以我们需要先从事件处理程序里面拿到这个索引。

```jsx
// 在事件处理函数里面添加一个当前索引
onMouseEnter={this.onItemMouseEnter.bind(this, key)}
```

然后我们在事件处理函数里面对state里面的数据进行修改。

```jsx
onItemMouseEnter(index) {
    this.setState({
        // 属性名要和state里面的属性名要相同
        currentIndex: index,
    });
}
```

剩下的tab栏部分大家就可以使用同样的原理完成了。

> 函数组件一般都要配合Hook一起使用，所以我们前面的课程暂时以class组件的方式先把基础知识点给大家过一遍，后期再专门学习Hook。

## 六、小案例：TodoList

> 小节目标：
>
> 1.能使用受控组件。
>
> 2.掌握父子组件之间的数据传递。
>
> 3.掌握context进行多级组件的数据传递。

接下来我们继续通过一个小案例来了解在react里面的组件传值的用法

![todo-eff](F:\next\react\day01\笔记\day01.assets\todo-eff.gif)

 

### 1.受控组件和非受控组件

在react里面，受控组件指的是组件里面的数据是和state关联的，非受控组件则刚好相反。

#### a.受控组件的状态管理

在TodoList案例里面，我们会有一个用于输入的输入框，这个输入框可以以受控组件的方式实现。

```jsx
export default class TodoHeader extends Component {
  constructor(props) {
    super(props);
    // 1. 在state里面准备一个和表单元素对应的数据
    this.state = {
      value: "",
    };
  }
  onValueChange(e) {
    this.setState({
      value: e.target.value,
    });
  }
  render() {
    return (
      <div className="flex todo-header">
        <input
          type="text"
          // 2. 将表单元素的value和state关联
          value={this.state.value}
          // 3. 添加控制state值的事件
          onChange={this.onValueChange.bind(this)}
        />
        <button>添加</button>
      </div>
    );
  }
}
```

#### b.非受控组件的数据管理

受控组件是推荐使用的，当然也可以使用非受控组件的方式来获取的操作数据，但是不推荐。

非受控组件指的是数据不受state管理的组件，比如：

```jsx
<input type="text"/>
```

此时如果我们需要得到非受控组件的数据，我们需要使用ref的方式获取到这个元素，然后使用原生js的方式操作。

```jsx
import React, { Component, createRef } from "react";

export default class TodoHeader extends Component {
  constructor(props) {
    super(props);
    // 1. 使用createRef方法创建ref数据
    this.inputRef = createRef();
  }
  onButtonClick() {
    // 3. 手动获取表单元素的value
    console.log(this.inputRef.current.value);
  }
  render() {
    return (
      <div className="flex todo-header">
        {/* 2.使用ref属性来关联ref数据 */}
        <input type="text" ref={this.inputRef} />
        <button onClick={this.onButtonClick.bind(this)}>添加</button>
      </div>
    );
  }
}
```

> 上面我们其实使用到了react里面获取一个dom元素或者Class组件实例的方法 createRef(),后期如果我们想获取的时候也可以使用。

### 2.父组件向子组件传递数据

react里面父组件向子组件传递数据比较简单，只需要给子组件一个自定义属性传递就行。

```jsx
<div className="todo">
    {/* 1. 使用一个自定义属性向子组件传递数据 */}
    <TodoList title="正在进行"/>
</div>
```

然后我们在子组件里面使用this.props进行接收

```jsx
export default class TodoList extends Component {
  render() {
    return (
      <div className="list">
        <h2>{this.props.title}</h2>
      </div>
    );
  }
}
```

### 3.子组件向父组件传递数据

react里面子组件不能直接修改父组件里面的数据，只能通过调用父组件的方法来实现，也就是子组件向父组件传递数据的过程。

```jsx
export default class Todo extends Component {
  // 1. 在父组件里面准备一个用于操作数据的方法
  addSome(value) {
    console.log(value);
  }
  render() {
    return (
      <div className="todo">
        {/* 2. 在子组件上直接传递操作数据的方法 */}
        <TodoHeader add={this.addSome.bind(this)} />
      </div>
    );
  }
}
export default class TodoHeader extends Component {
  onButtonClick() {
    // 3. 在子组件里面通过this.props获取并调用父组操作改数据的方法
    this.props.add(this.state.value);
  }
  render() {
    return (
      <div className="flex todo-header">
        <button onClick={this.onButtonClick.bind(this)}>添加</button>
      </div>
    );
  }
}
```

> 到目前为止我们就已经可以实现TodoList的添加功能了，快去试试吧。

 

### 4.多级组件传递数据

在react里面，多级组件之间传递使用得不多，但是我们还是需要掌握。

在react里面我们使用context的方式进行多级传递。其具体使用过程如下：

#### a.首先调用createContext方法创建一个“全局”context对象。

```jsx
import { createContext } from "react"
// 声明一个defaultValue用来声明context的数据结构
export const defaultValue = { count:0 , add(val){} }
// 创建context对象
export const TodoContext = createContext(defaultValue)
```

#### b.在“最高级”的外层组件使用 `Provider` 组件提供context对象

```jsx
import React, { Component } from "react";
import { MyContext } from "./context";
import Child from "./Child";

export default class Parent extends Component {
  constructor(props) {
    super(props);
    // 声明一个state，用于共享数据，结构和context的defaultValue保持一致
    this.state = {
      count,
      // 这是一个用于修改state数据的方法
      add: this.addFn.bind(this),
    };
  }
  addFn(val) {
    const count = (this.state.count += val);
    this.setState({ count });
  }
  render() {
    return (
        // 使用value属性来给Provider包着的组件提供数据，所有被它包着的组件都可以得到这这些数据
        <Provider value={this.state}>
            <Child />
        </Provider>
    );
  }
}

```

#### c.在需要使用“全局”数据的地方使用Consumer组件获取并操作数据

```jsx
import React, { Component } from "react";
import { MyContext } from "./context";

export default class Child extends Component {
  render() {
    return (
      // Consumer组件可能帮我们得到对应的context里面的数据，Consumer组件里面必须使用一个函数返回jsx结构
      <MyContext.Consumer>
        {/* 这个函数的value参数就是Provider的value属性*/}
        {(value) => (
          <div>
            {/* 获取数据 */}
            <div>{value.count}</div>
            <button
              // 操作数据
              onClick={() => {
                value.add(1);
              }}
            >
              ++
            </button>
          </div>
        )}
      </MyContext.Consumer>
    );
  }
}
```

至此我们就可以完全实现TodoList的所有功能了。

> context其实还有一个旧版的用法，只是太久远了，现在一般不使用了，想要了解的同学自己看看相同目录下的[《React补充》](http://110.40.134.6:9690/react/02.html)
>
> 并且我们context的使用其实不会太多，更多的我们会使用react-redux来进行全局数据管理。后面我们主要学习和使用它。

## 七、生命周期(面试用)

> 小节目标：
>
> 1. 能说出class组件里面的9个生命周期函数。

生命周期：就是指一个对象的生老病死。 React的生命周期指从组件被创建到销毁的过程。掌握了组件的生命周期，就可以在适当的时候去做一些事情。

React生命周期可以分成三个阶段：

1、实例化(挂载阶段)：对象创建到完全渲染

2、存在期(更新期)：组件状态的改变

3、销毁/清除期：组件使用完毕后，或者不需要存在与页面中，那么将组件移除，执行销毁。

![008eGmZEgy1gpmw1zwnuxj30uc0r00tt](F:\next\react\day01\笔记\day01.assets\008eGmZEgy1gpmw1zwnuxj30uc0r00tt.jpg)



### 1、实例化/挂载阶段

constructor()

componentWillMount()

render()

componentDidMount()

```jsx
export default class App3 extends Component {
    // 生命周期第一个阶段： 挂载/初始化阶段
    constructor(props){
        console.log("1.1 constructor: 构造初始化")
    }

    UNSAFE_componentWillMount(){
        console.log("1.2 componentWillMount")
        //做一些准备性的工作，比如提示正在加载
    }

    componentDidMount() {
        console.log("1.4 componentDidMount")
        //异步加载数据
    }
    render() {
        console.log("1.3 render")
        return (
            <div>
                <p>这是一个展示生命周期的组件</p>
            </div>
        )
    }
}    
```

### 2、存在期/更新期

存在期:且件已经渲染好并且用户可以与它进行交互。通常是通过一次鼠标点击、手指点按者键盘事件来触发一个事件处理器。随着用户改变了组件或者整个应用的state，便会有新的state流入组件树，并且我们将会获得操控它的机会。

componentWillReceiveProps()

shouldComponentUpdate()

componentWillUpdate()

render()

componentDidUpdate()

在上面的组建中继续书写生命周期函数：

```jsx
constructor(){
    this.state = {
        num:0
    }
}
render() {
    console.log("1.3/2.4 render")
    return (
        <div>
            <p onClick={this.handleClick.bind(this)}>这是一个展示生命周期的组件{this.state.num}</p>
        </div>
    )
}
handleClick(){
    this.setState({
        num:22
    })
}
// 生命周期第二个阶段  存在期/更新期
componentWillReceiveProps(){
    console.log("2.1 componentWillReceiveProps")
}
shouldComponentUpdate(nextProps, nextState) {
    console.log("2.2 shouldComponentUpdate 可以判断修改前后的值是不是一样，不一样才去执行render。减少不必要的render，优化更新性能")
    console.log("旧的值：", this.state.num)
    console.log("新的值：", nextState.num)
    // return true   则执行render
    // return false   则不执行render
    //这里返回值是布尔值，但不应该写死，
    //而是判断新旧两个值是不是不相等，不相等就要执行render(就要返回true)
    return this.state.num !== nextState.num
}
componentWillUpdate(nextProps, nextState) {
    console.log("2.3 componentWillUpdate 更新前的生命周期回调")
}
componentDidUpdate(prevProps, prevState) {
    console.log("2.5 componentDidUpdate 更新后的生命周期回调")
}
```

 

以上执行的是组件内部state数据更新前后的生命周期函数，

其实，**对于组件的props属性值发生改变的时候，同样需要更新视图，执行render**

**componentWillReceiveProps() 这个方法是将要接收新的props值的时候执行**，而props属性值从父组件而来，所以需要定义父组件：

```jsx
class App3 extends Component {

    //生命周期第二个阶段  存在期/更新期
    UNSAFE_componentWillReceiveProps(nextProps){
        console.log("2.1 componentWillReceiveProps 这个方法props属性值更新的时候才会执行，更新state数据则不会执行这个方法")        
        console.log(nextProps)
    }
    shouldComponentUpdate(nextProps, nextState) {
        console.log("2.2 shouldComponentUpdate 可以判断修改前后的值是不是一样，不一样才去执行render。减少不必要的render，优化更新性能")
        //而是判断新旧两个值是不是不相等，不相等就要执行render(就要返回true)
        return (this.state.num !== nextState.num || this.props.fatherNum !== nextProps.fatherNum)  //不仅仅是state数据跟新时候需要执行render，props属性的值更新的时候也要执行render，所以要多加一个判断条件
    }
}
export default class Father extends Component{
    constructor(props){
        // 调用父类构造方法
        super(props)
        // 初始化状态数据
        this.state = {
            fatherNum:0
        }
    }
    componentDidMount() {
        setTimeout(() => {
            this.setState({
                fatherNum:10
            })
        }, 2000);
    }
    render(){
        return(
            <App3 fatherNum={this.state.fatherNum}/>
        )
    }
}
```

### 3、销毁期

componentWillUnmount() 销毁组件前做一些回收的操作

```jsx
componentDidMount() {
    console.log("1.4 componentDidMount")
    document.addEventListener("click", this.closeMenu);
}
closeMenu(){
    console.log("click事件 closeMenu")
}
// 生命周期第三个阶段  卸载期/销毁期
componentWillUnmount() {
    console.log("3.1 componentWillUnmount 做一些回收的操作")
    document.removeEventListener("click", this.closeMenu);
}
```

index.js中3秒后重新渲染页面,就能触发组件的回收。

```jsx
setTimeout(() => {
    ReactDOM.render(
        <div>hello world</div>
        , document.getElementById('root'));
}, 3000);
```

### 4、生命周期小结

React组件的生命周期 3大阶段10个方法 1、初始化期（执行1次） 2、存在期 （执行N次） 3、销毁期 （执行1次）

> componentDidMount ： 发送ajax异步请求
>
> shouldComponentUpdate ： 判断props或者state是否改变，目的：优化更新性能

 

## 八、Hooks(非常重要)

> 小节目标：
>
> 1.能使用useState实现函数式组件的响应式数据。
>
> 2.能使用useContext实现多级组件间的数据传递。
>
> 3.能使用useEffect模拟生命周期。
>
> 4.能使用useRef获取DOM元素的引用。
>
> 5.能使用useReducer实现响应式数据操作。

### 1.什么是Hook --> [【戳这】](https://zh-hans.reactjs.org/docs/hooks-intro.html)

![image-20220618122110300](F:\next\react\day01\笔记\day01.assets\image-20220618122110300.png)

Hook本质是人家封装好的大量实现react类组件特性的函数，是我们后期做react开发一定要用的东西，所以大家一定要掌握。

### 2.StateHook

这是一个react提供好的用于实现state响应式特性的hook，使用如下：

```jsx
export default function StateHook() {
  // 调用useState得到一个数组，顺便解构出来两个东西，一个是数据，一个是用于操作数据的函数
  const [count, setCount] = useState(0);
  const onClick = () => {
    // 调用对应的方法操作数据
    setCount(count + 1);
  };
  return (
    <div>
      {/* 直接渲染对应的数据 */}
      <p>Count:{count}</p>
      <button onClick={onClick}>增加</button>
    </div>
  );
}
```

> 值得注意的是，hook只能使用在函数的最外层，任何别的位置都会报错。

### 3.自定义hook

使用hook可以让我们的数据的操作数据的逻辑放在一起，并且可以实现封装，把代码整理地更加易于维护。

如果在操作数据的过程中有一些比较复杂的逻辑，我们就可以采用自定义hook的方式把这部分逻辑分离出来。

```jsx
export default function StateHook() {
  const [count, setCount] = useState(0);
  const onClick = () => {
    // 如果有更加复杂的逻辑(假装很复杂)
    let val = 0;
    if (count > 0) {
      val = count - 1;
    } else {
      val = count + Math.floor(Math.random() * 10);
    }
    setCount(val);
  };
  return (
    <div>
      <p>Count:{count}</p>
      <button onClick={onClick}>增加</button>
    </div>
  );
}
```

如果我们在页面里面有大量的复杂逻辑，这样同样会使代码变得非常杂乱，后期难以维护，于是我们可以这样写。

```jsx
// 自定义hook要求以use开头
function useCount(initValue = 0) {
  const [count, setCount] = useState(initValue);
  const fn = () => {
    let val = 0;
    if (count > 0) {
      val = count - 1;
    } else {
      val = count + Math.floor(Math.random() * 10);
    }
    setCount(val);
  };
  return [count, fn];
}
export default function StateHook() {
  // 调用我们自定义的hook ， 把复杂的逻辑全抽离到自定义hook，这样在我们的组件里面就尽可能简洁了
  const [count, setCount] = useCount();
  const onClick = () => {
    setCount();
  };
  return (
    <div>
      <p>Count:{count}</p>
      <button onClick={onClick}>增加</button>
    </div>
  );
}
```

### 4.ContextHook

ContextHook是用来解决多级组件之间数据传递的问题的。首先必须明确的是，函数式组件之间的父子数据传递数据，几乎和class组件是一样的。

```jsx
export default function ParentFC() {
  const [count, setCount] = useState(0);
  const addFn = (val) => {
    setCount(count + val);
  };
  return (
    <div>
      <div>ParentFC</div>
      {/* 在子组件上通过自自定义属性传递数据 */}
      <ChildFC data={count} add={addFn} />
    </div>
  );
}
// 使用props参数接收父组件传递过来的数据
function ChildFC(props) {
  const {data,add} = props
  const onButtonClick = () => {
    // 调用从父组件传递过来的方法进行子传父
    add(1);
  };
  return (
    <div>
      <div>ChildFC</div>
      <div>Count From Parent:{data}</div>
      <button onClick={onButtonClick}>Add</button>
    </div>
  );
}
```

并且之前在class组件里面使用的多级组件传递数据的方式在函数组件其实也是可用的，只是比较复杂，我们不太推荐，而更加推荐使用ContextHook;

ContextHook基本使用步骤如下：

#### a.调用createContext创建一个Context对象

```jsx
const MyContext = createContext();
```

#### b.使用Provider组件提供一个“全局”数据

```jsx
export default function ContextHook() {
  const [count, setCount] = useState(10);
  const add = (val) => {
    setCount(count + val);
  };
  return (
    <MyContext.Provider value={{ count, add }}>
      <Parent />
    </MyContext.Provider>
  );
}
```

#### c.在后代组件里面使用useContext方法获取Context对象

```jsx
function Parent() {
  return (
    <div>
      <Child />
    </div>
  );
}
function Child() {
  const context = useContext(MyContext);
  return (
    <div>
      {/* context对象就是之前的Provider里面的value属性 */}
      <p>count from ancestors：{context.count}</p>
      <button onClick={() => context.add(1)}>Add</button>
    </div>
  );
}
```

> 小练习：可以使用上面介绍的几种hook来实现tab栏和TodoList案例了。

### 5.EffectHook

函数组件里面没有生命周期，我们可以使用EffectHook来模拟，这也是我们在今后最经常使用的方式。

useEffect的基本用法如下：

```jsx
useEffect(当依赖发生变化时调用的函数, [依赖的数据]);
```

例如：

```jsx
import React, { useEffect, useState } from "react";
export default function EffectHook() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    console.log("EffectHook调用了");
  },[count]);
  const onClick = () => {
    setCount(count + 1);
  };
  return (
    <div>
      <p>Count:{count}</p>
      <p>Double:{double}</p>
      <button onClick={onClick}>++</button>
    </div>
  );
}
```

这里我们设置的是count作为EffectHook的依赖，所以只要count发生了变化，就会触发这个回调的调用。

#### 使用EffectHook模拟生命周期：

##### a.模拟componentDidMount

```jsx
useEffect(() => {
    console.log("这是用来模拟挂载期的");
}, []);
```

##### b.模拟componentDidUpdate

```jsx
useEffect(() => {
    console.log("这是用来模拟更新期的");
}, [deps]);
```

##### c.模拟componentWillUnmount

```jsx
useEffect(() => {
    return ()=>{
        // 在这里面写卸载期的代码
        console.log("这是用来模拟卸载期的");
    }
}, []);
```

> 注意：
>
> 同个useEffect下，在检测销毁和检测字段更新之间，只能二选一。留下空数组，可以检测到return中的销毁。数组非空时，视图更新会带动return返回值，因此如果要检测字段更新，就无法检测销毁。

### 6.RefHook

在函数组件里面我们可以使用userRef这个Hook获取一个元素或者组件的引用

```jsx
import React, { useEffect, useRef } from "react";

export default function RefHook() {
  const btn = useRef();
  // 在componentDidMount后获取
  useEffect(() => {
    console.log(btn.current);
  }, []);
  return (
    <div>
      <button ref={btn}>Button</button>
    </div>
  );
}
```

### 7.ReducerHook

useReducer是useState的替代方案，当useState里面的逻辑相对复杂的时候，我们可以使用useReducer来代替。

useRducer的基本使用步骤如下：

#### a.准备一个初始state数据和操作state的方法

```jsx
// 初始state
const state = {
  count: 0,
};
// 操作state的方法reducer
// aciont里面一般是type和pyload两个属性用来判断不同的复杂逻辑
const reducer = (st = state, action) => {
  const state = JSON.parse(JSON.stringify(st));
  // 通过判断不同的action来处理不同的逻辑
  switch (action.type) {
    case "add":
      state.count += action.pyload;
      break;
    case "reduce":
      state.count -= action.pyload;
      break;
  }
  // reducer一定要返回一个新的state
  return state;
};
```

#### b.调用useReducer这个Hook来得到state和dispatch

```jsx
export default function ReducerHook() {
  // state就是我们需要维护的数据，dispatch是一个方法，用来调用reducer的
  const [state, dispatch] = useReducer(reducer, initState);
  return (
    <div>
      <div>ReducerHook</div>
      <div>state's count : {state.count}</div>
      {/* dispatch方法传入一个action来激活reducer里面对应的操作 */}
      <button onClick={() => dispatch({ type: "add", pyload: 1 })}>Add</button>
      <button onClick={() => dispatch({ type: "reduce", pyload: 1 })}>
        reduce
      </button>
    </div>
  );
}
```

 

### 8.其它Hook

上述讲解到的已经是我们平时比较常用的hook，当然hook不是只有这些，如果想了解，[戳这里](https://zh-hans.reactjs.org/docs/hooks-reference.html)

 

## 九、路由

> 小节目标：
>
> 1.能使用react-router-dom进行组件的切换。
>
> 2.能使用Outlet组件并配置子路由
>
> 3.能使用useNavagate进行手动跳转。
>
> 4.能使用路由进行数据传递(三种方式)。

正常的项目里面基本都会选择使用路由进行组件的切换，react也有它自己专门的路由。

[【官方文档】](https://reactrouter.com/)

其使用主要有三大版本：

`v3.x~v4.x` 用法基本相同 ， `v5.x` 用法与旧版相比相关较大，与新版相比比较接近 ， `v6.x` 是目前最新的版本，也是我们学习的主要版本。只要掌握了`v6.x`的，需要使用别的版本的时候再自己学习就好。

### 1.下载安装

```jsx
npm i --save  react-router-dom@6
```

或者

```jsx
yarn add react-router-dom@6 --save
```

### 2.基本使用

```jsx
// 1. 导入 reactrouter提供的组件
// import { BrowserRouter, Routes, Route } from "react-router-dom";
// 技巧：这样切换路由时下面标签就不用动 BrowserRouter 历史模式  HashRouter 哈希模式
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
export default function BasicRouter() {
  return (
    // 2.确定使用的是哪种路由模式(history/hash)
    <Router>
      {/* 3.配置路由表 */}
      <Routes>
        {/* 4.配置每个路由path对应的组件 */}
        <Route path="/" element={<Index />}></Route>
        <Route path="/list" element={<List />}></Route>
        <Route path="/about" element={<About />}></Route>
      </Routes>
    </Router>
  );
}
```

### 3.配置子路由

a.直接在父路由里面配置子路由

```jsx
<BrowserRouter>
    <Routes>
        <Route path="/" element={<Index />}>
            {/* 直接在父 Route下面配置子Route */}
            <Route path="list" element={<List />}></Route>
            <Route path="about" element={<About />}></Route>
        </Route>
    </Routes>
</BrowserRouter>
```

b.在作为父路由对应的组件里面使用 `Outlet` 组件来展示子路由对应的组件

```jsx
function Index() {
  return (
    <div>
      <div>Index</div>
      <Outlet />
    </div>
  );
}
```

### 4.使用Link作为跳转方式

a.路由配置

```jsx
<BrowserRouter>
    <Routes>
        <Route path="/" element={<Index />}>
            <Route path="list" element={<List />} />
            <Route path="about" element={<About />} />
        </Route>
    </Routes>
</BrowserRouter>
```

b.在父组件里面配置Link和Outlet

```jsx
import { Link, Outlet } from "react-router-dom";
function Index() {
  return (
    <div>
      <ul>
        <li><Link to="/list">List</Link></li>
        <li><Link to="/about">About</Link></li>
      </ul>
      <Outlet />
    </div>
  );
}
```

### 5.编程式导航

`ReactRouter` `v6.x`  使用useNavigate这个hook来进行跳转。

```jsx
function Index() {
  // 1. 在组件里面使用 useNavigate 得到 navigate 函数
  const nav = useNavigate();
  return (
    <div>
      <div>Index</div>
      {/* 2. 在需要跳转的位置调用 navigate 函数跳转，直接传入一个path、数字或者路由配置对象 */}
      {/* 如果 navigate 函数接收的是一个数字， 负数表示后退,正数表示前进 */}
      <button onClick={() => nav("/state")}>
        about
      </button>
    </div>
  );
}
```

### 6.路由传参

#### a.动态路由形式

首先进行路由表配置

```jsx
 <BrowserRouter>
    <Routes>
        <Route path="list/:id" element={<List />}></Route>
    </Routes>
</BrowserRouter>
```

然后在对应的组件里面使用useParams这个hook进行数据获取

```jsx
import { useParams } from "react-router-dom";
function List() {
  const params = useParams();
  console.log(params); // {id:xxx}
  return <div>List</div>;
}
```

#### b.query参数

如果有下面这样一个url

```
http://www.domain.com/list?id=10&type=3
```

如果想获取到 `?` 之后的参数，我们需要使用 useSearchParams 这个hook进行操作

```jsx
import { useSearchParams } from "react-router-dom";
function About(){
    // 调用 useSearchParams 得到query参数
    let [searchParams, setSearchParams] = useSearchParams();
    // 调用 searchParams 对象的 get 方法得到对应的数据
    console.log(searchParams.get('id')) // 10
    console.log(searchParams.get('type')) // 3
    return <div>About</div>
}
```

#### c.state传参

state传递数据的方式需要使用navigate手动跳转的时候传递。

首先在A组件里面。

```jsx
function Index() {
  const nav = useNavigate();
  return (
    <div>
      <div>Index</div>
      {/* navigate 函数的第二个参数可以传递state数据 */}
      <button onClick={() => nav("/state", { state: { id: 456 } })}>go to state page</button>
    </div>
  );
}
```

然后在B组件里面使用location对象获取。

```jsx
function State() {
  const location = useLocation();
  console.log(location.state); // { id:456 }
  return <div>State</div>;
}
```

 

## 十、ReactRedux

> 小节目标:
>
> 1.能使用react-redux进行全局数据共享(Provider,userSelector,useDisaptch)。

`ReactRedux`是一套React专用的全局状态管理工具，在大型项目中也非常常用。

### 1.安装

react-redux是基于redux这个包的，所以我们需要在安装react-redux的时候，把redux一起安装

```jsx
npm i redux react-redux 或者 yarn add redux react-redux
```

### 2.基本使用

#### a.使用redux提供的createStore方法创建一个store对象

```jsx
import { createStore } from 'redux'
const defState = {
  count: 100
}
const reducer = (state = defState, action) => {
  state = JSON.parse(JSON.stringify(state))
  switch (action.type) {
    case 'add':
      state.count += action.pyload;
      break;
  }
  return state
}
// 创建store对象，createStore方法需要一个reducer函数
const store = createStore(reducer)
export default store;
```

#### b.使用react-redux提供的Provider组件全局提供数据

```jsx
import store from "./store.js";
import { Provider } from "react-redux";

export default function BasicStore() {
  return (
    // Provider 需要一个store属性，这个store属性就是我们的store对象
    <Provider store={store}>
      <div>BasicStore</div>
      <Child />
    </Provider>
  );
}
```

c.在Provider包着的后代组件里面使用 userSelector 和 useDisaptch 对store里面的数据进行操作

```jsx
import { useDispatch, useSelector } from "react-redux";
function Child() {
  // useSelector方法可以根据一个函数得到state里面的数据
  const count = useSelector((state) => state.count);
  // dispatch 是一个函数，用来触发 在 recuder 里面的 action 来操作数据
  const dispatch = useDispatch();
  return (
    <div>
      <div>Child</div>
      <div>{count}</div>
      {/* 直接调用 dispatch 触发 reducer 里面对应的 action */}
      <button onClick={() => dispatch({ type: "add", pyload: 2 })}>Add</button>
    </div>
  );
}
```

#### 3.connect组件使用redux

```jsx
function Ch(props) {
  return (
    <div>
      <div>Child</div>
      {/* 直接使用props访问store里面的数据 */}
      <div>{props.count}</div>
      {/* 直接使用props访问store里面的方法 */}
      <button onClick={props.add}>Add</button>
    </div>
  );
}
// 这个函数用于将store的数据映射到组件的props上
const mapStateToProps = (state) => ({ count: state.count });
// 这个函数用于将store的dispatch映射到组件的props上
const mapDispatchToProps = (dispatch) => ({
  add() {
    dispatch({ type: "add", pyload: 2 });
  },
});
// 使用react-redux提供的 connect 方法将组件进行加工，将数据映射到props上
const Child = connect(mapStateToProps, mapDispatchToProps)(Ch);
```

> 其实这种方式还算比较复杂，已经不推荐使用，但是如果是在class组件里面，因为我们没法使用hook，所以需要了解一下这些用法。

 

 

 

 

 