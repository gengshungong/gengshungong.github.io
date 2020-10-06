---
layout: post
title: 知识在于不断积累，查漏补缺实乃王道！
permalink: /question/
---

- content
{:toc}

### 2019 面试题

##### 网上面试题

> 一卷

- 1、快速排序和冒泡排序
- 2、BFC 概念，BFC 怎样形成的
- 3、AMD 和 CMD 的概念
- 4、import 和 export
- 5、rem 的适配方案
- 6、git 或 svn 常用命令
- 7、闭包，构造函数，继承
- 8、flex 布局和 fle 兼容性问题
- 9、浏览器从 url 输入到渲染成页面经历了哪些过程
- 10、ES6 语法
- 11、grunt 和 gulp 原理及应用
- 12、本地 localstorage 和 session 的区别
- 13、nodejs 是干什么用的
- 14、http https 的概念，为什么 http 不能访问 https
- 15、npm 包管理机制，package.json
- 16、html 语义化和 H5 标签
- 17、页面性能优化
- 18、前端 SEO
- 19、IE8 的兼容问题，hack
- 20、在改变 url 时页面不刷新的办法

> 二卷

<p>JavaScript 基础</p>
+ 1、列举 JavaScript 中所有假值
+ 2、请写出一个函数`initArray`，接受两个参数 m 和 n，返回一个数组，它的长度是 m，每个值都是 n
+ 3、请写出一个函数`yesterday`，接受一个 Date 类型参数 date，返回一个 Date，正好是 date 的前一天
+ 4、现有二个字段：id，Number 类型； name，String 类型。取值自定义，请写出相应的 json。
+ 5、完成`extname`函数，它会接受一个文件名作为参数，你需要返回它的扩展名。例如，输入`emoji.png`，返回`.png`
+ 6、请写出以下代码的执行结果
var name = 'World!';
(() => {
if (typeof name === 'undefined') {
var name = 'Jack';
console.log('Goodbye ' + name);
} else {
console.log('Hello ' + name);
}
})();
+ 1、列举 HTML 中标签常用的全局属性，并描述其作用
+ 2、列举 HTML 中常用的块级元素，并描述其作用
+ 3、列举 HTML 中常用的行内元素，并描述其作用
+ 4、列举 HTML5 中 input 标签的新增 type 属性值，并描述其作用
+ 5、列举 form 标签的 method 属性和 enctype 属性值，并描述其作用
+ 6、列举 button 标签的 type 属性值，并描述其作用
+ 7、定义一个 a 标签，在浏览器新窗口中打开<http://www.baidu.com>
+ 8、列举常用 HTTP 状态码及其含义
 <p>CSS</p>
+ 1、 有一个`div#wrapper`元素，高、宽度都未知。它其中有一个宽高都为 100px 的`div#box`元素，请你完成 CSS，使得`div#box`在`div#wrapper`内水平、垂直方向居中。
+ 2、韩梅梅拒绝了李雷，李雷伤心地问韩梅梅，你到底喜欢怎么样的男生。韩梅梅说，她喜欢又高、又富、又帅的男生。假设现在页面上有很多个 div 元素代表不同的男生，类名表示他们具有的特性，例如 tall 表示高，wealthy 表示富，handsome 表示帅。请你完成 CSS， 给韩梅梅喜欢的男生加上红色的边框（ 1px solid red ）。

> 三卷

##### react 面试题汇总

> <p>React 中 keys 的作用是什么？</p>

Keys 是 React 用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识。

```js
render () {
  return (
    <ul>
      {this.state.todoItems.map(({item, key}) => {
        return <li key={key}>{item}</li>
      })}
    </ul>
  )
}
```

在开发过程中，我们需要保证某个元素的 key 在其同级元素中具有唯一性。在 React Diff 算法中 React 会借助元素的 Key 值来判断该元素是新近创建的还是被移动而来的元素，从而减少不必要的元素重渲染。此外，React 还需要借助 Key 值来判断元素与本地状态的关联关系，因此我们绝不可忽视转换函数中 Key 的重要性。

> <p>调用 setState 之后发生了什么？</p>

在代码中调用 setState 函数之后，React 会将传入的参数对象与组件当前的状态合并，然后触发所谓的调和过程（Reconciliation）。经过调和过程，React 会以相对高效的方式根据新的状态构建 React 元素树并且着手重新渲染整个 UI 界面。在 React 得到元素树之后，React 会自动计算出新的树与老树的节点差异，然后根据差异对界面进行最小化重渲染。在差异计算算法中，React 能够相对精确地知道哪些位置发生了改变以及应该如何改变，这就保证了按需更新，而不是全部重新渲染。

> <p>react 生命周期函数</p>

初始化阶段：

getDefaultProps:获取实例的默认属性
getInitialState:获取每个实例的初始化状态
componentWillMount：组件即将被装载、渲染到页面上
render:组件在这里生成虚拟的 DOM 节点
componentDidMount:组件真正在被装载之后
运行中状态：

componentWillReceiveProps:组件将要接收到属性的时候调用
shouldComponentUpdate:组件接受到新属性或者新状态的时候（可以返回 false，接收数据后不更新，阻止 render 调用，后面的函数不会被继续执行了）
componentWillUpdate:组件即将更新不能修改属性和状态
render:组件重新描绘
componentDidUpdate:组件已经更新
销毁阶段：

componentWillUnmount:组件即将销毁
shouldComponentUpdate 是做什么的，（react 性能优化是哪个周期函数？）
shouldComponentUpdate 这个方法用来判断是否需要调用 render 方法重新描绘 dom。因为 dom 的描绘非常消耗性能，如果我们能在 shouldComponentUpdate 方法中能够写出更优化的 dom diff 算法，可以极大的提高性能。

> 参考 react <a href="https://segmentfault.com/a/1190000016259872" target="blank">性能优化-sf</a>

> <p>为什么虚拟 dom 会提高性能?(必考)</p>

虚拟 dom 相当于在 js 和真实 dom 中间加了一个缓存，利用 dom diff 算法避免了没有必要的 dom 操作，从而提高性能。

用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异把 2 所记录的差异应用到步骤 1 所构建的真正的 DOM 树上，视图就更新了。

> 参考 <a href="https://www.zhihu.com/question/29504639?sort=created" target="_blank">如何理解虚拟 DOM?-zhihu</a>

> <p>react diff 原理（常考，大厂必考）</p>

把树形结构按照层级分解，只比较同级元素。
给列表结构的每个单元添加唯一的 key 属性，方便比较。
React 只会匹配相同 class 的 component（这里面的 class 指的是组件的名字）
合并操作，调用 component 的 setState 方法的时候, React 将其标记为 dirty.到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制.
选择性子树渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。
参考：React 的 diff 算法

> <p>React 中 refs 的作用是什么？</p>

Refs 是 React 提供给我们的安全访问 DOM 元素或者某个组件实例的句柄。我们可以为元素添加 ref 属性然后在回调函数中接受该元素在 DOM 树中的句柄，该值会作为回调函数的第一个参数返回：

```js
class CustomForm extends Component {
  handleSubmit = () => {
    console.log('Input Value: ', this.input.value)
  }
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text" ref={input => (this.input = input)} />
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

上述代码中的 input 域包含了一个 ref 属性，该属性声明的回调函数会接收 input 对应的 DOM 元素，我们将其绑定到 this 指针以便在其他的类函数中使用。另外值得一提的是，refs 并不是类组件的专属，函数式组件同样能够利用闭包暂存其值：

```js
function CustomForm({ handleSubmit }) {
  let inputElement
  return (
    <form onSubmit={() => handleSubmit(inputElement.value)}>
      <input type="text" ref={input => (inputElement = input)} />
      <button type="submit">Submit</button>
    </form>
  )
}
```

> <p>如果你创建了类似于下面的 Twitter 元素，那么它相关的类定义是啥样子的？</p>

```js
<Twitter username="tylermcginnis33">
  {user => (user === null ? <Loading /> : <Badge info={user} />)}
</Twitter>
```

```js
import React, { Component, PropTypes } from 'react'
import fetchUser from 'twitter'
// fetchUser take in a username returns a promise
// which will resolve with that username's data.
class Twitter extends Component {
  // finish this
}
```

如果你还不熟悉回调渲染模式（Render Callback Pattern），这个代码可能看起来有点怪。这种模式中，组件会接收某个函数作为其子组件，然后在渲染函数中以 props.children 进行调用：

```js
import React, { Component, PropTypes } from 'react'
import fetchUser from 'twitter'
class Twitter extends Component {
  state = {
    user: null
  }
  static propTypes = {
    username: PropTypes.string.isRequired
  }
  componentDidMount() {
    fetchUser(this.props.username).then(user => this.setState({ user }))
  }
  render() {
    return this.props.children(this.state.user)
  }
}
```

这种模式的优势在于将父组件与子组件解耦和，父组件可以直接访问子组件的内部状态而不需要再通过 Props 传递，这样父组件能够更为方便地控制子组件展示的 UI 界面。譬如产品经理让我们将原本展示的 Badge 替换为 Profile，我们可以轻易地修改下回调函数即可：

```js
<Twitter username="tylermcginnis33">
  {user => (user === null ? <Loading /> : <Profile info={user} />)}
</Twitter>
```

> <p>展示组件(Presentational component)和容器组件(Container component)之间有何不同</p>

展示组件关心组件看起来是什么。展示专门通过 props 接受数据和回调，并且几乎不会有自身的状态，但当展示组件拥有自身的状态时，通常也只关心 UI 状态而不是数据的状态。
容器组件则更关心组件是如何运作的。容器组件会为展示组件或者其它容器组件提供数据和行为(behavior)，它们会调用 Flux actions，并将其作为回调提供给展示组件。容器组件经常是有状态的，因为它们是(其它组件的)数据源。
类组件(Class component)和函数式组件(Functional component)之间有何不同
类组件不仅允许你使用更多额外的功能，如组件自身的状态和生命周期钩子，也能使组件直接访问 store 并维持状态
当组件仅是接收 props，并将组件自身渲染到页面时，该组件就是一个 '无状态组件(stateless component)'，可以使用一个纯函数来创建这样的组件。这种组件也被称为哑组件(dumb components)或展示组件
(组件的)状态(state)和属性(props)之间有何不同
State 是一种数据结构，用于组件挂载时所需数据的默认值。State 可能会随着时间的推移而发生突变，但多数时候是作为用户事件行为的结果。
Props(properties 的简写)则是组件的配置。props 由父组件传递给子组件，并且就子组件而言，props 是不可变的(immutable)。组件不能改变自身的 props，但是可以把其子组件的 props 放在一起(统一管理)。Props 也不仅仅是数据--回调函数也可以通过 props 传递。

> <p>何为受控组件(controlled component)</p>

在 HTML 中，类似 `<input>, <textarea> 和 <select>` 这样的表单元素会维护自身的状态，并基于用户的输入来更新。当用户提交表单时，前面提到的元素的值将随表单一起被发送。但在 React 中会有些不同，包含表单元素的组件将会在 state 中追踪输入的值，并且每次调用回调函数时，如 onChange 会更新 state，重新渲染组件。一个输入表单元素，它的值通过 React 的这种方式来控制，这样的元素就被称为"受控元素"。

> <p>何为高阶组件(higher order component)</p>

高阶组件是一个以组件为参数并返回一个新组件的函数。HOC 运行你重用代码、逻辑和引导抽象。最常见的可能是 Redux 的 connect 函数。除了简单分享工具库和简单的组合，HOC 最好的方式是共享 React 组件之间的行为。如果你发现你在不同的地方写了大量代码来做同一件事时，就应该考虑将代码重构为可重用的 HOC。

> <p>为什么建议传递给 setState 的参数是一个 callback 而不是一个对象</p>

因为 this.props 和 this.state 的更新可能是异步的，不能依赖它们的值去计算下一个 state。

> <p>除了在构造函数中绑定 this，还有其它方式吗</p>

你可以使用属性初始值设定项(property initializers)来正确绑定回调，create-react-app 也是默认支持的。在回调中你可以使用箭头函数，但问题是每次组件渲染时都会创建一个新的回调。

> <p>(在构造函数中)调用 super(props) 的目的是什么</p>

在 super() 被调用之前，子类是不能使用 this 的，在 ES2015 中，子类必须在 constructor 中调用 super()。传递 props 给 super() 的原因则是便于(在子类中)能在 constructor 访问 this.props。

> <p>应该在 React 组件的何处发起 Ajax 请求</p>

在 React 组件中，应该在 componentDidMount 中发起网络请求。这个方法会在组件第一次“挂载”(被添加到 DOM)时执行，在组件的生命周期中仅会执行一次。更重要的是，你不能保证在组件挂载之前 Ajax 请求已经完成，如果是这样，也就意味着你将尝试在一个未挂载的组件上调用 setState，这将不起作用。在 componentDidMount 中发起网络请求将保证这有一个组件可以更新了。

> <p>描述事件在 React 中的处理方式。</p>

为了解决跨浏览器兼容性问题，您的 React 中的事件处理程序将传递 SyntheticEvent 的实例，它是 React 的浏览器本机事件的跨浏览器包装器。

这些 SyntheticEvent 与您习惯的原生事件具有相同的接口，除了它们在所有浏览器中都兼容。有趣的是，React 实际上并没有将事件附加到子节点本身。React 将使用单个事件监听器监听顶层的所有事件。这对于性能是有好处的，这也意味着在更新 DOM 时，React 不需要担心跟踪事件监听器。

> <p>createElement 和 cloneElement 有什么区别？</p>

React.createElement():JSX 语法就是用 React.createElement()来构建 React 元素的。它接受三个参数，第一个参数可以是一个标签名。如 div、span，或者 React 组件。第二个参数为传入的属性。第三个以及之后的参数，皆作为组件的子组件。

```js
React.createElement(type, [props], [...children])
```

React.cloneElement()与 React.createElement()相似，不同的是它传入的第一个参数是一个 React 元素，而不是标签名或组件。新添加的属性会并入原有的属性，传入到返回的新元素中，而就的子元素奖杯替换。

```js
React.cloneElement(element, [props], [...children])
```

> <p>React 中有三种构建组件的方式</p>

React.createClass()、ES6 class 和无状态函数。

> <p>react 组件的划分业务组件技术组件？</p>

根据组件的职责通常把组件分为 UI 组件和容器组件。
UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑。
两者通过 React-Redux 提供 connect 方法联系起来。

> <p>简述 flux 思想</p>

Flux 的最大特点，就是数据的"单向流动"。
用户访问 View
View 发出用户的 Action
Dispatcher 收到 Action，要求 Store 进行相应的更新
Store 更新后，发出一个"change"事件
View 收到"change"事件后，更新页面
React 项目用过什么脚手架（本题是开放性题目）
creat-react-app Yeoman 等

> <p>了解 redux 么，说一下 redux </p>

redux 是一个应用数据流框架，主要是解决了组件间状态共享的问题，原理是集中式管理，主要有三个核心方法，action，store，reducer，工作流程是 view 调用 store 的 dispatch 接收 action 传入 store，reducer 进行 state 操作，view 通过 store 提供的 getState 获取最新的数据，flux 也是用来进行数据操作的，有四个组成部分 action，dispatch，view，store，工作流程是 view 发出一个 action，派发器接收 action，让 store 进行数据更新，更新完成以后 store 发出 change，view 接受 change 更新视图。Redux 和 Flux 很像。主要区别在于 Flux 有多个可以改变应用状态的 store，在 Flux 中 dispatcher 被用来传递数据到注册的回调事件，但是在 redux 中只能定义一个可更新状态的 store，redux 把 store 和 Dispatcher 合并,结构更加简单清晰
新增 state,对状态的管理更加明确，通过 redux，流程更加规范了，减少手动编码量，提高了编码效率，同时缺点时当数据更新时有时候组件不需要，但是也要重新绘制，有些影响效率。一般情况下，我们在构建多交互，多数据流的复杂项目应用时才会使用它们

> <p>redux 有什么缺点</p>

一个组件所需要的数据，必须由父组件传过来，而不能像 flux 中直接从 store 取。
当一个组件相关数据更新时，即使父组件不需要用到这个组件，父组件还是会重新 render，可能会有效率影响，或者需要写复杂的 shouldComponentUpdate 进行判断。

##### es6 面试题汇总

> 聊聊 promise

promise 是一个异步函数，主要是为了解决异步处理回调地狱(也就是循环嵌套的问题)而产生的，有 3 种状态，Fulfilled 为成功的状态， Rejected 为失败的状态，Pending 既不是 Fulfilld 也不是 Rejected 的状态，可以理解为 Promise 对象实例创建时候的初始状态，要会写 promise 这个方法。

> ES6 特性你了解多少？如果遇到一个东西不知道是 ES6 还是 ES5，你改如何区分？

常用的 es6 新特性：let && const；let 命令也用于声明对象，但是作用域为局部；iterable 类型。为了统一集合类型，ES6 标准引入了新的 iterable 类型，Array、Map 和 Set 都属于 iterable 类型，具有 iterable 类型的集合可以通过新的 for … of 循环来遍历。es6 比 es5 增加了很多特殊的方法，如果你遇到了这些特殊的方法， 你就可以确定它是 es6。如果你的代码中没有引用这些特殊的方法，那我们就可以认为他是 es5 的。所以前提你需要了解 es6 的语法才能做判断，高频使用的特性有箭头函数、解构赋值、let、const。

> ES6 的继承和 ES5 的继承有什么区别

es5 的继承是通过原型或者是构造函数机制来实现，es6 用过 class 关键字定义类，里面有构造方法，类之间通过 extends 关键字实现，子类必须在 constructor 方法中调用 super 方法。

> let 和 const 的优点？

let 和 const 有了块级作用域，相比于 var 变量声明不会提升。

> ES6 generator 是什么，async / await 实现原理？

generator 函数就是一个封装的异步任务，也就是异步任务的容器，执行 Generator 函数会返回一个遍历器对象,async 函数的实现， 就是将 Generator 函数和自动执行器，包装在一个函数里。
